Back to [Static filter syntax](./Static-filter-syntax).

***

- [Caveats](#caveats)
- [Overview](#overview)
- [Concrete examples of usefulness](#concrete-examples-of-usefulness)

***

#### Caveats

Script tag filters do not work in all browsers, due to browser API limitations:

- Not supported in Chromium-based browser.
    - Starring the [related Chromium issue](https://bugs.chromium.org/p/chromium/issues/detail?id=168175) may help motivate Chromium devs to implement support.
    - Falling back on wholesale blocking of all inline script tags may work.<sup>[1]</sup>
- Not supported in Firefox's WebExtensions version of uBO when...
    - Firefox 56 and less is used;
    - uBO version 1.14.23b2 and less used.

<sub>[1] Through the use of the `inline-script` static filter option (`||example.com^$inline-script`), or through the use of a dynamic filtering block rule for _inline scripts_.</sub>

***

#### Overview

There are many ways to block script tags from executing in uBlock Origin:

- Block external script resources: these are taken care by network filtering.
- Block all inline script tags embedded in a page at once.<sup>[1]</sup>

Inline script tags are those blocks of JavaScript code which are embedded in the main page: they can not be blocked from downloading unless the whole page itself is blocked, which is not very useful. Here is a example of a web page's HTML code with two inline script tags:

```html
<html>
<head>
<meta name="referrer" content="origin">
<link rel="stylesheet" href="main.css" />
<script type="text/javascript">
    function usefulCode() {
        ...
    }
    ...
</script>
<title>lorem ipsum</title>
</head>
<body>
<h1>lorem ipsum</h1>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
<script type="text/javascript">
    function nuisanceCode() {
        ...
    }
    ...
</script>
</body>
```

In this example, blocking inline script tags wholesale would not be a good solution because both script tags would be blocked and we would lose the `usefulCode` function as well.

uBlock Origin 1.15.0 introduces [HTML filtering](./Static-filter-syntax#html-filters), which can be used to remove specific inline script tags from a web page _before_ the browser parses the HTML response from the server:

    example.com##^script:has-text(...)

Where the value inside the parenthesis in `has-text(...)` can be a plain string or a literal JavaScript regular expression (`/.../`).

So we can use HTML filtering for our above example to specifically remove one of the script tags (assuming the page's URL is `https://foo.example/bar.html`):

    foo.example##^script:has-text(nuisanceCode)

This filter means: for any web pages from the `foo.example` web site, remove all inline script tags which contains the string `nuisanceCode`.

In the cat and mouse game between web sites and blockers, the new script tag filter is a welcomed new tool on the user side, to foil attempt by site to work around blockers.

The big advantage of this new filter is that it can fix _at the source_ many of the anti-blocker workarounds used by some web sites.

For example, the web site at `http://focus.de/` will resort to deface itself with ridiculous ads when the site detects that the user is using a blocker, and using _EasyList_ + _EasyList Germany_ does not work, as the images pulled by the page are randomly named, defeating pattern-based network filters and cosmetic filters as well.

Wholesale blocking of inline script tags does prevent the self-defacing, but possibly at the cost of disabling other possible useful functionalities on the page. However, a script tag filter to block the specific inline script tag which contains the self-defacement JavaScript code allows a more targeted approach: prevent the undesirable inline JavaScript code from executing while keeping the desirable inline JavaScript code intact. At time of writing, this script tag filter worked for the site:

    www.focus.de##^script:has-text(uabInject)

***

#### Concrete examples of usefulness

A concrete example of a site which resorts to self-defacement when it detects that a blocker is in use -- the front page of [rp-online.de](http://www.rp-online.de/):

Without inline script tag filtering:<br>
![without inline script tag filtering](https://cloud.githubusercontent.com/assets/585534/10417577/ec9bbe80-700e-11e5-8fc1-3f21358b45ee.png)

With an appropriate inline script tag filter:<br>
![with inline script tag filtering](https://cloud.githubusercontent.com/assets/585534/10417578/eeb27aba-700e-11e5-9c2e-0845cd27b404.png)

The _uBlock filters_ list, which is selected by default, already contains a couple of inline script tag filters to take care of some of these annoyances.

