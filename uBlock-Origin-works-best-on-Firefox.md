This document explains why uBO works best in Firefox.

### CNAME-uncloaking

Ability to uncloak 3rd-party servers disguised as 1st-party through [CNAME record](https://en.wikipedia.org/wiki/CNAME_record). The effect of this is to make uBO on Firefox the most efficient at blocking 3rd-party trackers relative to other browser/blocker pairs:

![c](https://user-images.githubusercontent.com/585534/103416937-b623c400-4b56-11eb-8e94-b4851a2248b7.png)

The dark green/red bars are uBO before/after it gained the ability to uncloak CNAMEs on Firefox.

Source: [_"Characterizing CNAME Cloaking-Based Tracking on the Web"_](https://blog.apnic.net/2020/08/04/characterizing-cname-cloaking-based-tracking/) at [Asia Pacific Network Information Centre](https://www.apnic.net/about-apnic/), August 2020.

### HTML filtering

[HTML filtering](https://github.com/gorhill/uBlock/wiki/Static-filter-syntax#html-filters) is the ability to filter the response body of HTML documents _before_before parsing them by the browser.

For example, this allows the removal of specific tags in HTML documents before they are parsed and executed by the browser, something not possible in a reliable manner in other browsers. This feature requires the [`webRequest.filterResponseData()`](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/webRequest/filterResponseData) API, currently only available in Firefox.

### Browser launch

Firefox will wait for uBO to be ready before sending network requests from already opened tab(s) at browser launch.

In Chromium-based browsers, this is not the case. Tracker/advertisement payloads may find their way into already opened tabs before uBO is ready, while Firefox will properly filter these.

Reliably blocking at browser launch is especially important for whoever uses default-deny mode for 3rd-party resources or JavaScript.

A [setting](https://github.com/gorhill/uBlock/wiki/Dashboard:-Filter-lists#suspend-network-activity-until-all-filter-lists-are-loaded) is available, disabled by default, to mitigate this issue in Chromium-based browsers. This setting does not cover 100% of all use cases, and some exceptions may apply.

### Pre-fetching

Pre-fetching, disabled by default in uBO, is reliably prevented in Firefox, while this is not the case in Chromium-based browsers.

Chromium-based browsers give precedence to websites over user settings when it comes to deciding whether pre-fetching is disabled or not.

Reference: [Disable prefetching](https://github.com/gorhill/uBlock/wiki/Dashboard:-Settings#disable-prefetching)

### WebAssembly

The Firefox version of uBO uses WebAssembly code for core filtering code paths. With Chromium-based browsers, this is not the case because this would require an extra permission in the extension manifest that could cause friction when publishing the extension in the Chrome Web Store.

More Information: https://github.com/WebAssembly/content-security-policy/issues/7#issuecomment-441259729

### Storage compression

The Firefox version of uBO uses LZ4 compression by default to store raw filter lists, compiled list data, and memory snapshots to disk storage.

LZ4 compression requires the use of [`IndexedDB`](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API), which is problematic with Chromium-based browsers in the incognito mode where instances of `IndexedDB` get reset, causing uBO to launch inefficiently and with out-of-date filter lists (see [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399)). `IndexedDB` is required because it supports storing [`Blob`](https://developer.mozilla.org/en-US/docs/Web/API/Blob)-based data, a capability unavailable to [`browser.storage.local` API](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/storage/local).