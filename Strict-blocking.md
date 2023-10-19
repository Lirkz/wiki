[[Back to Wiki home|Home]]

***
In uBlock Origin (uBO), _strict blocking_ is the blocking of a whole page, i.e. the _root_ document is blocked, so that not a single connection is made to the remote server hosting the web page.

By default, strict blocking is enabled in uBO for domain-only filters (this reduces false-positive matches). To force it on any other pattern matching filter, use [`document`](./Static-filter-syntax#document) or [`all`](./Static-filter-syntax#all) static filter option.

This feature is not supported by other blockers, like Adblock Plus (ABP), which only blocks secondary resources (see [web pages _themselves_ are **never** filtered](https://forum.adblockplus.org/viewtopic.php?t=18774#p85439)).

So if you were to create a filter such as `||example.com^`, and then navigate to <https://example.com>, ABP would not prevent you from connecting and loading the web page itself served at `https://example.com`, though all secondary resources pulled by that web page would be subject to filtering.

uBO respected that semantic until version 0.9.3.0. With version 0.9.3.0, uBO will subject web pages themselves to filtering.

This means that using the same test case above, **uBO will block the web page** served by a server found in one of the malware list (unlike ABP):

![Page was fully blocked](https://user-images.githubusercontent.com/585534/189539077-9e2c8e46-7de0-42c0-9e1d-34b9a31a39a5.png)

Why the change? Because [issue #1013](https://github.com/chrisaljoudi/uBlock/issues/1013) brought forth why it is desirable sometimes to completely block a website, as opposed to what the EasyList syntax-based filtering semantic dictates.

In the end, the chosen solution is to now have web page themselves subject to filtering, just like all secondary resources.

In the figure above, the user will be given the choice to go back to the previous webpage, or proceed to the currently blocked webpage by disabling strict blocking either:

- Temporarily: Click _Proceed_ to disable strict-blocking for a limited time (60 seconds, after [1.17.4](https://github.com/gorhill/uBlock/releases/tag/1.17.4) 120 seconds - [configurable](./Advanced-settings#strictblockingbypassduration)).
- Permanently: Check _Dont warn me again about this site_, then click _Proceed_.

This will prevent the web page _proper_ for the site from being blocked by uBO in the future: the filtering of the site will be done exactly as per EasyList syntax-based filtering semantic, and just like with uBO pre-0.9.3.0.

There are many benefits to strict blocking. For example, there is no good reason one should want to connect _at all_ to any of the sites present in any one of the malware domain lists. Strict blocking will prevent this from happening.

**Important note:** Keep in mind that when the above warning occurs, it doesn't necessarily mean the site is harmful, it just means that there is a matching filter in the selected filter lists. You decide whether the site is safe, and whether disabling strict blocking permanently for the site is appropriate.

**Tip:** If you wish, you may entirely disable strict blocking everywhere by adding the rule `no-strict-blocking: * true` to the _My rules_ pane in the dashboard (don't forget to click _Commit_ to make the rule stick).

### Ability to parse the strict-blocked URL

Sometimes, the strict-blocked URL contains a [query string component](https://en.wikipedia.org/wiki/Query_string) which uBO can parse and decompose into detailed query parameters. Oftentimes, once decomposed, the query parameters will show you information which can be useful.

A top example of this is when a redirection URL is strict blocked, you will often find in the query parameters the destination URL which you intended to visit when you clicked a link, which makes it possible to bypass the redirection URL -- typically used for tracking purpose -- and navigate directly to the intended destination URL by just clicking on it.

Example:

![a](https://user-images.githubusercontent.com/585534/189539478-5b9d454b-67aa-4e85-9a2f-e8eb3f0accc7.png)

In the example above, a link to _BestBuy_ site was clicked (from DuckDuckGo search page), but doing so caused the browser to navigate to a strict-blocked redirection link instead of navigating directly to the _BestBuy_ site. By expanding the query strings into components, we can see our actual destination URL -- just click on it and you will finally reach your intended destination without having to go through the `clickserve.dartsearch.net` server which was strict-blocked by an entry in StevenBlack/hosts list.
