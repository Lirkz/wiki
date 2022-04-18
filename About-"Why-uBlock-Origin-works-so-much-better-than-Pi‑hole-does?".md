Off the top of my head:

- Cancels network requests early within the browser
- Pattern-based filtering on the whole URL
    - example: `&act=ads_`
- Context information
    - example: `$script,third-party,domain=imgbox.com`
    - point-and-click to enable/disable blocking behavior on a per-site basis:
        - JavaScript
        - Large media elements
        - Remote fonts
        - Etc.
    - you can see what specific network requests are made by what specific page, you can fully inform yourself of what specific pages/sites are causing your browser to do
        - example: <https://twitter.com/gorhill/status/934474012377444352>
- Ability to redirect to a neutered version of a resource
    - example: `||google-analytics.com/ga.js$script,redirect=google-analytics.com/ga.js`
- Cosmetic filtering, the manipulation of DOM elements in the browser
    - example: `##.AdHeader`
- Scriptlet injection filtering, the injection of JS scriptlets to modify the behavior of a page which is effective to defuse anti-content blockers
    - example: `wallstreet-online.de##+js(nostif, userHasAdblocker)`
- HTML filtering (Tor Browser and Firefox only), the removal of DOM elements from a document before parsed by the browser
    - example: `wetteronline.de##^script:has-text(runCount)`
- Ability to deal with unwanted popups
    - example: `&link_type=offer$popup,third-party`
- Ability to remove tracking parameters from websites
    - example: `||wuzhuiso.com^$removeparam=src`
- You can easily (narrowly/broadly) override any filter from the filter lists through simple point-and-click operations to customize your filtering or to quickly fix sites broken as a result of overzealous filters

The main advantage of Pi-Hole is that it filters network traffic from all devices on your network, but filtering is blunt compared to what you can do through a browser extension.