1- Using `:upward()` instead of `:has()` can be more performant. `:upward()` is fast, it just lookup ancestors -- there is only one parent per element, `:has()` has to lookup descendants, there can be many children per elements.

```html
<div id="text-19" class="widget">
  <div class="section-heading">
    <span class="h-text">Promoted Links</span>
  </div>
  <div class="textwidget">
    <ul>
      <li>
        <a href="http://example.com" target="_blank" rel="nofollow noopener">Ad Link</a>
      </li>
    </ul>
  </div>
```
In the case above, it's better to use `##.widget .h-text:has-text(Promoted Links):upward(.widget)` instead of `##.widget:has(.h-text:has-text(Promoted Links))`.

2- For all static network filters, ensure that they have as many primary narrowing options as possible, i.e. that they are well targeted. Pure hostname-based filters (such as `||example.com^`) are most optimized memory- and cpu-wise. For non-pure hostname, i.e. pattern-based filters (such as `||example.com/path/to/file`) , ensure they are tokenizable, narrow their target with filter options and/or `domain=` if they are meant to apply only on specific site(s).

Regarding static network filters, pure hostname ones are most optimized, as they are stored in a compressed [trie](https://en.wikipedia.org/wiki/Trie), and WebAssembly code is used to look them up (in Firefox). With the trie, the number of comparisons to perform to find a hit will always be more proportional to the number of characters in the hostname to match, less to the number of filters in the list, so you could have tens of thousands of such filters with no measurable performance hit.

Pattern-based filters -- i.e. `||example.com/path/to/file^` -- may end up in a trie if uBO decides it's worth, but in any case they end up in a compact TypedArray and there again WebAssembly code is used to pattern-match (in Firefox).

A single wildcard (somewhere in the middle) will require two patterns to be stored in the TypedArray and a special matching algorithm to be used.

Two wildcards and above, uBO falls back to use a regular expression internally, so those are to be avoided if possible. Regex-based filters (should be rare) will also be regular expression internally.

Pattern-based filters are visited only when a matching token is found in the URL to pattern-match, so even if all of your list was made of filters with two or more wildcards, uBO would execute their associated internal regex if and only if a matching token is extracted from the URL, so for instance having a couple of multi-wildcard filters in a list is a complete non-issue so long as good tokens can be extracted from these filters.

So for non-pure hostname based filters, the top concern is whether the filter is tokenizable, and also whether the filter has all the necessary narrowing options so as to avoid having to visit that filter when there is no need to.

Primary narrowing options: tokenizable, `1p`, `3p`, `image`, `script`, `frame`, etc. These options can prevent a filter from being visited at all.

For example adding `3p` when using the `domain=` narrowing option will tell uBO to not even visit the filter when a network request is 1st-party. Without `3p`, uBO will visit the filter for all network requests of though it will bail out when it finds out that the `domain=` option is no match. With `3p`, the filter is never ever visited for 1st-party requests, as if the filter didn't exist. This is all conceptually, in practice there would no measurable difference between both filters all other things being equal, given we are talking about low two-digit microseconds per request.

Secondary narrowing option is `domain=`, but it's not as efficient as the previous ones. The `domain=` narrowing option does not prevent a filter from being visited, but it does prevent having to execute the more costly pattern-matching code of the filter when the domain= option is not a match.

So for example, even with what appears as a worst-case scenario, a filter from EasyList with no explicit narrowing option:

```adb
/^https?:\/\/(.+?\.)?allthingsvegas\.com\/[a-zA-Z]{7,18}\//
```

This is a regex-based filter with no explicit narrowing option. However this filter is still performant in uBO because a token can be extracted from it, `allthingsvegas`, and as a result that filter is visited only when uBO finds the token `allthingsvegas` somewhere in the URL of the network request, which is quite unlikely except probably where it's actually meant to be enforced.

Another example from EasyList:

```adb
/(https?:\/\/)\w{30,}.me\/\w{30,}\./$script,third-party
```

No token can be extracted from this filter, which is a concern (properly escaping the `.` would make it possible to extract a good token), but at least it has narrowing options, `script` and `3p`, which at least make it so that the filter will be visited only for network request of type script which are 3rd-party to the current context.

Source: 
- https://reddit.com/r/uBlockOrigin/comments/mdh9jz/order_of_complexity_for_network_filters/gsa7gd2/
- https://reddit.com/r/uBlockOrigin/comments/mdh9jz/order_of_complexity_for_network_filters/gxzxfo0/

3- To prevent a pattern-based filter to be treated as a regex-based filter, you need a trailing wildcard to remove the ambiguity.

```adb
/path/to/
```
Filter above will be treated as a regex-based filter since it starts and ends with `/`. To force it to be treated as a plain pattern, a trailing wildcard is used:
```adb
/path/to/*
```

The trailing wildcard will be dropped, but the filter is now the pattern `/path/to/`.

Source: https://reddit.com/r/uBlockOrigin/comments/mdh9jz/order_of_complexity_for_network_filters/gsfn0xl/