This document explains why uBO works best in Firefox.

### CNAME-uncloaking

Ability to uncloak 3rd-party servers disguised as 1st-party through the use of [CNAME record](https://en.wikipedia.org/wiki/CNAME_record). The effect of this is to make uBO on Firefox the most efficient at blocking 3rd-party trackers relative to other other blocker-browser pairs:

![c](https://user-images.githubusercontent.com/585534/103416937-b623c400-4b56-11eb-8e94-b4851a2248b7.png)
<br>The dark green/red bars are uBO before/after it gained ability to uncloak CNAMEs on Firefox.<br>Source: [_"Characterizing CNAME Cloaking-Based Tracking
on the Web"_](https://blog.apnic.net/2020/08/04/characterizing-cname-cloaking-based-tracking/) by [Asia Pacific Network Information Centre](https://www.apnic.net/about-apnic/)

### HTML filtering

[HTML filtering](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#html-filters) is the ability to the filter response body of HTML documents before it's parsed by the browser.

For example, this allows removing specific tags in HTML documents before they are parsed and executed by the browser, something not possible in a reliable manner in other browsers. This feature requires the [`webRequest.filterResponseData()`](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webRequest/filterResponseData) API, currently only available in Firefox.

### Browser launch

At browser launch, Firefox will wait for uBO to be up and ready before network requests are fired in already opened tab(s). This is not the case with Chromium-based browsers, i.e. tracker/advertisement payloads may find their way into already opened tabs in Chromium-based browsers, while these are properly filtered in Firefox. Reliably blocking at browser launch is especially important for whoever uses default-deny mode of blocking.

### Pre-fetching

Pre-fetching, which is disabled by default in uBO, is reliably disabled in Firefox, while this is not the case in Chromium-based browsers. Chromium-based browsers give precedence websites over user settings when it comes to decide whether pre-fetching is disabled or not. See [documentation for _"Disable pre-fetching"_ ](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-pre-fetching).

### WebAssembly

The Firefox version of uBO makes use of WebAssembly code for core filtering code paths. This is not the case with Chromium-based browsers because this would require an extra permission in the extension manifest which could cause friction when publishing the extension in the Chrome Web Store.

### Storage compression

The Firefox version of uBO can use LZ4 compression to store raw filter lists, compiled list data, and memory snapshots to disk storage.