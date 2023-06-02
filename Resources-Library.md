
 - Current RAW version of Resources can be found in [scriptlets.js file ↪](https://github.com/gorhill/uBlock/blob/master/assets/resources/scriptlets.js) and [web_accessible_resources directory ↪](https://github.com/gorhill/uBlock/tree/master/src/web_accessible_resources)
 - [General purpose scriptlets](#general-purpose-scriptlets)
 - [Defuser scriptlets](#defuser-scriptlets)
 - [Empty redirect resources](#empty-redirect-resources)
 - [URL-specific sanitized redirect resources](#url-specific-sanitized-redirect-resources-surrogates)
 - [Other](#other)
 - [Glossary](#glossary)



***


## Available general purpose scriptlets

- [abort-current-inline-script](#abort-current-inline-scriptjs-) _(acis)_
- [abort-on-property-read](#abort-on-property-readjs-) _(aopr)_
- [abort-on-property-write](#abort-on-property-writejs-) _(aopw)_
- [abort-on-stack-trace](#abort-on-stack-tracejs-) _(aost)_
- [addEventListener-defuser](#addeventlistener-defuserjs-) _(aeld)_
- [~addEventListener-logger~](#addeventlistener-loggerjs-) _(~aell~)_
- [set-constant](#set-constantjs-) _(set)_
- [trusted-set-constant](#trusted-set-constantjs-) _(trusted-set)_ [Trusted]
- [call-nothrow](#call-nothrowjs-)
- [no-setInterval-if](#no-setinterval-ifjs-) _(nosiif)_
- [no-setTimeout-if](#no-settimeout-ifjs-) _(nostif)_
- [nano-setInterval-booster](#nano-setinterval-boosterjs-) _(nano-sib)_
- [nano-setTimeout-booster](#nano-settimeout-boosterjs-) _(nano-stb)_
- [no-fetch-if](#no-fetch-ifjs-)
- [no-xhr-if](#no-xhr-ifjs-)
- [remove-attr](#remove-attrjs-) _(ra)_
- [remove-class](#remove-classjs-) _(rc)_
- [replace-node-text](#replace-node-textjs-) _(rpnt)_ [Trusted]
- [remove-node-text](#remove-node-textjs-) _(rmnt)_
- [spoof-css](#spoof-cssjs-)
- [href-sanitizer](#href-sanitizerjs-)
- [cookie-remover](#cookie-removerjs-)
- [disable-newtab-links](#disable-newtab-linksjs-)
- [window-close-if](#window-close-ifjs-)
- [window.open-defuser](#windowopen-defuserjs-) _(nowoif)_
- [json-prune](#json-prunejs-)
- [evaldata-prune](#evaldata-prunejs-)
- [xml-prune](#xml-prunejs-)
- [m3u-prune](#m3u-prunejs-)
- [noeval](#noevaljs-)
- [noeval-silent](#noeval-silentjs-)
- [noeval-if](#noeval-ifjs-)
- [no-floc](#no-flocjs-)
- [no-requestAnimationFrame-if](#no-requestanimationframe-ifjs-) _(norafif)_
- [nowebrtc](#nowebrtcjs-)
- [webrtc-if](#webrtc-ifjs-)
- [window.name-defuser](#windowname-defuser-)
- [refresh-defuser](#refresh-defuserjs-)
- [overlay-buster](#overlay-busterjs-)
- [alert-buster](#alert-busterjs-)

***

## Available defuser scriptlets

- [ampproject_v0](#ampproject_v0js-)
- [fingerprint2](#fingerprint2js-)
- [fingerprint3](#fingerprint3js-)
- [nobab](#nobabjs-) <sup>_(BlockAdblock)_</sup>
- [nobab2](#nobab2js-) <sup>_(BlockAdblock 4.2b)_</sup>
- [nofab](#nofabjs-) <sup>_(FuckAdblock)_</sup>
- [popads-dummy](#popads-dummyjs-)
- [popads](#popadsjs-)
- [prebid-ads](#prebid-adsjs-)
- [adfly-defuser](#adfly-defuserjs-)

***

## Available empty redirect resources

- `1x1.gif`
- `2x2.png`
- `3x2.png`
- `32x32.png`
- `noop.css`
- `noop.html` (`noopframe`)
- `noop.js`
- `noop.txt`
- `noop-0.1s.mp3`
- `noop-0.5s.mp3`
- `noop-1s.mp4`
- `none`
- `click2load.html`

***

## Available URL-specific sanitized redirect resources (surrogates)

- [addthis_widget.js](#addthis_widgetjs-)
- [amazon_ads.js](#amazon_adsjs-)
- [amazon_apstag.js](#amazon_apstagjs-)
- [monkeybroker.js](#monkeybrokerjs-)
- [doubleclick_instream_ad_status](#doubleclick_instream_ad_statusjs-)
- [google-analytics_ga.js](#google-analytics_gajs-)
- [google-analytics_analytics.js](#google-analytics_analyticsjs-)
- [google-analytics_inpage_linkid.js](#google-analytics_inpage_linkidjs-)
- [google-analytics_cx_api.js](#google-analytics_cx_apijs-)
- [google-ima.js](#google-imajs-)
- [googletagservices_gpt.js](#googletagservices_gptjs-)
- [googletagmanager_gtm.js](#googletagmanager_gtmjs-)
- [googlesyndication_adsbygoogle.js](#googlesyndication_adsbygooglejs-)
- [scorecardresearch_beacon.js](#scorecardresearch_beaconjs-)
- [outbrain-widget.js](#outbrain-widgetjs-)
- [hd-main.js](#hd-mainjs-)

***


## General purpose scriptlets
 - Most scriptlet relies on `Object` _properties_ ([_methods_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#Methods_of_the_Object_constructor)), altering them may not be the best idea (you should know what you are doing).
 - Some properties related more to browser APIs rather than JS language built-ins can behave in unexpected way. For example browser can override them without scriptlet noticing this. Keep this in mind when using them in scriptlet injection filers.
 - "Optional" for "string/_regular expression_" parameter defaults to "catch all" (`/.?/`) if not specified.
 - "String" parameter means plain character(s)/word(s), quotes will be taken literally, commas [must be escaped](https://github.com/uBlockOrigin/uAssets/commit/2bec415a9bc4f81b29be3bf083ef1a20552f39db#commitcomment-29327114) in regex literals: `/foo\x2cbar\u002cbaz/`, after [1.22.0](https://github.com/gorhill/uBlock/commit/d67340f14db6ce5b446ef0ff4586b5e4d31f1086#diff-b03ba512faa0934947e57d28dc99b43bL242) commas can be escaped by backslash character (`foo\,bar`).
 - "Regular expression" parameter means JavaScript [regular expression literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Writing_a_regular_expression_pattern).
 - Mime type is `application/javascript` if not present.
 - You can use the short alias form when available for scriptlet name.
 - You should omit the `.js` from the scriptlet name in scriptlet injection filters (eventually in some future this will be the official way to do this).
     - Do **not** skip `.js` when the scriptlet is used with `redirect=`, only when used in `+js(...)`.
 - Crossed out resources are deprecated/removed.
 - Starting with [1.46.1b17](https://github.com/gorhill/uBlock/commit/81498474d6d440b032681aa9952d593749b39efb) support for regex-based values as target domain has been added. Use sparingly, when no other solution is practical from a maintenance point of view -- keeping in mind that uBO has to iterate through all the regex-based values, unlike plain hostname or entity-based values which are mere lookups. Related discussion: [uBlockOrigin/uBlock-issues#2234](https://github.com/uBlockOrigin/uBlock-issues/discussions/2234). Example: `/img[a-z]{3,5}\.buzz/##+js(nowoif)`.
 - The usage of named arguments is optional, positional arguments are still supported as documented. Named arguments is required to use "log" and/or "debug" arguments.
 - The logging/debugging capabilities work only in the **dev build** of uBO or if the advanced setting `filterAuthorMode` is set to `true`.
- The only filter lists deemed from a "trusted source" are uBO-specific filter lists (i.e. "uBlock filters -- ..."), and the user's own filters from "My filters".

***

### acs.js /
### abort-current-script.js /
### acis.js /
### abort-current-inline-script.js [↪](https://github.com/gorhill/uBlock/blob/784ebb09050cb6617bd857f7c6a4311ac9649ce9/assets/resources/scriptlets.js#L35)
Aborts execution of inline script (_throws_ `ReferenceError`) when attempts to access specified _property_ when text content or `src` attribute value (new in [1.37.0](https://github.com/gorhill/uBlock/commit/ebc42ae21e7900fafeaf1041038b94488b1d50e5)) of `<script>` _element_ matches specified text or _regular expression_.

Note that `acis.js` and `abort-current-inline-script.js` aliases are deprecated and can be removed in the future.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object accessed inside `<script>` tag we want to break
 - optional, string/_regular expression_ matching in `<script>` _element_ content
 - optional, new in [1.37.0](https://github.com/gorhill/uBlock/commit/ebc42ae21e7900fafeaf1041038b94488b1d50e5), string/_regular expression_ matching in the decoded value of the `src` attribute of the `<script>` tag, when the attribute content is not a remote network address, but the actual inline script URL-encoded or base64-endcoded as a `data:` URI

Examples:
 - `weristdeinfreund.de##+js(acis, Number.isNaN)`
 - `tichyseinblick.de##+js(acis, Math, /\}\s*\(.*?\b(self|this|window)\b.*?\)/)`


Starting with [1.48.5b4](https://github.com/gorhill/uBlock/commit/edbe96a4010cff59a37c2aa2ec0fb89c48c913f9), you can use the logging abilites.

To enable logging, use the JSON approach to pass parameters to `acs` scriptlet. Example:
```adb
example.com##+js(acs, { "target": "document.oncontextmenu", "log": true })
```

Whereas "target", "needle", and "context" correspond to their respective positional argument. Using JSON form to pass parameters allows to specify extra paramters to facilitate debugging of that scriptlet:

- `"log": true` => output useful information at the dev console.
- `"debug": true` => break at key locations in the scriptlet.


***

### aopr.js /
### abort-on-property-read.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L96)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to read specified _property_. Writes are ignored.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object

Examples:
 - `tagesspiegel.de##+js(aopr, Notification)`


***

### aopw.js /
### abort-on-property-write.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L150)
Aborts execution of script (_throws_ `ReferenceError`) when attempts to write specified _property_.

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object that will be overwritten

Examples:
 - `yggtorrent.*##+js(aopw, Fingerprint2)`

***


### aost.js /
### abort-on-stack-trace.js [↪](https://github.com/gorhill/uBlock/blob/793e2c78963ba86c8d36b950807ce952f7199c1f/assets/resources/scriptlets.js#L194)

#### _Experimental, under development_

New in [1.29.3rc9](https://github.com/gorhill/uBlock/commit/b735ac6b6abab7d5f45e15bbba3b4ba6cbf43935)

Aborts execution of script (_throws_ `ReferenceError`) when attempts to access specified _property_ when _stack trace_ matches specified text or _regular expression_. <sub>[Internal discussion](https://github.com/orgs/uBlockOrigin/teams/ublock-issues-volunteers/discussions/237?from_comment=59)</sub>

Parameters:
 - required, _property_ (chain of properties joined by `.`) to trap in order to launch the stack trace matching code, ex. `Math.random`.
 - optional, string/_regular expression_, the needle to match against the stack trace. If the empty string, always match.
 - optional, whether to log, and if so how:
     - Empty string: do not log
     - `1`: log stack trace for all access to trapped property
     - `2`: log stack trace for defused access to trapped property
     - `3`: log stack trace for non-defused access to trapped property

Stack trace is normalized, but there still can be differences (Chromium vs Firefox) because of different format of stack trace.

There is a special string which can be used to match inline script context - `inlineScript`.

Though the stack trace is rendered in the console using new line to separate the stack trace lines, internally `\t` is used. The reason is to be more easily be able to create regex-based needle when using regex `.` character class.

The stack trace is prepended with `stackDepth:...` in order to allow to filter on stack depth, however higher depth values can likely differ between Chromium and Firefox.

Firefox often reports `injectedScript`, attempt has been made to convert entries in Chromium which seems to correspond to this, so that both browser families will report `injectedScript`.

The column value is normalized to 1, however there is too much discrepancy between browser families for that value to be of any use.

Filtering according to reported line numbers (`...:1234:1`), will not be reliable for inline scripts, since the line at which those inline scripts are located will vary from one page to another. It should be reliable for when the stack trace entry is for code in a JS file.

***

### aeld.js /
### addEventListener-defuser.js [↪](https://github.com/gorhill/uBlock/blob/07d3c96261656e44f674550fbde50da8f6a15acc/assets/resources/scriptlets.js#L308)
Prevents attaching event listeners.

Parameters (when using positional arguments):
 - optional, string/_regular expression_, name of the event listener to defuse
 - optional, string/_regular expression_ matching in stringified handler function, narrows down defusing to specific handler

Examples:
 - `vev.io##+js(aeld, adb.updated)`
 - `newser.com##+js(aeld, load, Object)`
 - `vivo.sx##+js(aeld, , preventDefault)`
 - `vidto.me##+js(aeld, /^(?:click|mousedown|mousemove|touchstart|touchend|touchmove)$/, system.popunder)`

Parameters (when using named arguments) <sup>([New in 1.48.1b3](https://github.com/gorhill/uBlock/commit/439951824af608bd445ec458f837fa39f366d75f))</sup>:
 - "type": the event type to match (such as [`load`, `mousedown`, `contextmenu`](https://developer.mozilla.org/en-US/docs/Web/Events#event_listing)). Default to '', i.e. _match-all_.
 - "pattern": the pattern to match against the handler argument. Default to '', i.e. _match-all_.
 - "runAt": when this parameter is present, uBO will take it into account to possibly defer defusing the event listener <sup>([New in 1.49.3b4](https://github.com/gorhill/uBlock/commit/3c12173dfe4eea7c4b6758c556ed2dd5fcdbdd99))</sup>:
     - end: execute scriptlet at `DOMContentLoaded` event ("interactive")
     - idle: execute scriptlet at `load` event ("complete")
 - "log": an integer value telling when to log:
     - 1: log only when both type and pattern matches, i.e. when a call to `addEventListener()` is defused
     - 2: log when either the type or pattern matches
     - 3: log all calls to `addEventListener()`
 - "debug": an integer value telling when to break into the debugger, useful to inspect the debugger's call stack.
     - 1: break into the debugger when both type and pattern match, so effectively when defusing is taking place.
     - 2: break into the debugger when either type or pattern matches.

Examples:
 - `wikipedia.org##+js(aeld, { "type": "/mouse/", "pattern": "/.^/", "log": 2 })`
 - `wikipedia.org##+js(aeld, { "type": "/.^/", "log": 2 })`
 - `wikipedia.org##+js(aeld, { "log": 1 })`
 - `jpvhub.com##+js(aeld, { "type": "click", "pattern": "popMagic", "runAt": "idle" })`

The first filter will log calls to `addEventListener()` which have the pattern "mouse" in the event type (so "mouseover", "mouseout", etc.) **without defusing any of them** (because pattern can't match _anything_).

The second filter will log all calls **without defusing any of them** (because type can't match _anything_).

The third filter will log and defuse _all_ calls to `addEventListener()`.

***

### ~aell.js~ /
### ~addEventListener-logger.js~ [↪](https://github.com/gorhill/uBlock/blob/07d3c96261656e44f674550fbde50da8f6a15acc/assets/resources/scriptlets.js#L352)
Removed in [1.48.1b3](https://github.com/gorhill/uBlock/commit/439951824af608bd445ec458f837fa39f366d75f).

Logs to the console event listeners created on page.

The logging or debugging of `addEventListener()` calls can now be done with the [`addEventListenerDefuser`](#addeventlistener-defuserjs-) scriptlet, which now supports named arguments.

***

### cookie-remover.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L942)
Removes current page cookies specified by name. For current domain, wildcard (dot) subdomain(s), after [1.28.0](https://github.com/gorhill/uBlock/commit/c4d39d37632fbee4d513116641a282ed2a48c89d) also for domain one level above `www`, current and `/` path, script accessible (HttpOnly=false), on load and before unload.

Caveats: cookies set for higher level domain will not be removed. For example, if current page domain is `page.example.com`, cookies set for `example.com` will not be removed. One exception is `www` subdomain, which will work after [1.28.0](https://github.com/gorhill/uBlock/commit/c4d39d37632fbee4d513116641a282ed2a48c89d).

Parameters:
 - optional, string/_regular expression_, matching in the name of the cookie

Examples:
 - `subdivx.com##+js(cookie-remover, ref_cookie)`


***

### ~csp.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1849)
Removed. Deprecated by `$csp` network filter option.  
Applies content security policy by inserting `<meta http-equiv=Content-Security-Policy content="*directive*">` tag to html `<head>` _element_.
Read more at https://www.w3.org/TR/CSP2/#delivery-html-meta-element  
[Content Security Policy Quick Reference Guide](https://content-security-policy.com/)

Parameters:
 - required, valid Content Security Policy directive


***

### call-nothrow.js [↪](https://github.com/gorhill/uBlock/blob/e93117cbb607472a830e1c0653dfbddde4c965fc/assets/resources/scriptlets.js#L1984)

New in [1.48.1b0](https://github.com/gorhill/uBlock/commit/e93117cbb607472a830e1c0653dfbddde4c965fc).

Prevents a call to an existing function from throwing an exception.
It encloses existing functions in this block and ignores the exception:
```js
try {
 [existing function]
}
catch() {
 [ignore when throws]
}

```

It will return `undefined` because returning variable is never set.


The exception will be caught by the scriptlet and neutralized. The first argument must be a reference to a function call. At the moment, the function call must exist at the time the scriptlet is called.

Parameters:
 - required, _a reference to a function call_

Examples:
 - `example.com##+js(call-nothrow, Object.defineProperty)`

***

### disable-newtab-links.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L869)
Prevents creating new tabs/windows by deactivating links with `target` attribute.

Parameters:
 - none

Examples:
 - `there.to##+js(disable-newtab-links)`

To prevent new tabs/windows by specifying the location URL, see: [`window-close-if.js`](https://github.com/uBlockOrigin/uBlock-issues/wiki/Resources-Library#window-close-ifjs-)

***

### evaldata-prune.js [↪](https://github.com/gorhill/uBlock/blob/f3b720d532c7a42a6ad5167e3b6f860004b4c2b6/assets/resources/scriptlets.js#L1039)

New in [1.49.3rc15](https://github.com/gorhill/uBlock/commit/c8de9041917b61035171e454df886706f27fc4f3)

Intercepts calls to `eval()` and will work only if what is passed to `eval` can be parsed as JSON.

For parameters, see: [json-prune](#json-prunejs-)

When no "prune paths" argument (first parameter) is provided, the scriptlet is used for logging purpose and the "needle paths" argument (second parameter) is used to filter logging output.

Examples:
 - `m.nivod4.tv##+js(evaldata-prune, entity.commercial)`


***

### json-prune.js [↪](https://github.com/gorhill/uBlock/blob/d338e4c4b6caf339873a60c9d48fde58e9a495ce/assets/resources/scriptlets.js#L365)

New in [1.23.0](https://github.com/gorhill/uBlock/commit/2fd86a66fcc2665e5672cc5862e24b3782ee7504)

Intercepts calls to `JSON.parse()` and `Response.json()`<sup>[New in 1.31.0](https://github.com/gorhill/uBlock/commit/13f92756befaa9a8d3ba1615bd7abc7075758c67)</sup>. If the result of the parsing is an Object, remove specified properties from the result before returning to the caller.

Parameters:
 - optional, string, a list of space-separated properties to remove 
 - optional,
     - string, a list of space-separated properties which must be all present for the pruning to occur; OR
     - string/_regular expression_, for logging purposes, matching in stringified JSON payloads (New in [1.27.0](https://github.com/gorhill/uBlock/commit/578594bbd7c545b62f18267d640a605f8e07a53a))

A property in a list of properties can be a chain of properties, example: `adpath.url.first`.

After [1.28.0](https://github.com/gorhill/uBlock/commit/f433932d8602230539d3408e9946d4d70b40306c), two special _"wildcard tokens"_ have been added:

- `[]` - will iterate in all elements in an array. To deal with cases where the
property to remove is an element in an array.
    To remove `adserver` object properties from array in following JSON payload:

        {"playlist": [{"adserver": "first"},{"adserver": "second"}]}

    Use:

        +js(json-prune, playlist.[].adserver)

- `*` - will iterate through all own properties of an object. For example, to deal with hard to predict random-named properties.
    To remove `adserver` object properties from inside _randomly named_ objects in following JSON payload:

        {"playlist": {"random1": {"adserver": "first"}, "randomB": {"adserver": "second"}}}

    Use:

       +js(json-prune, playlist.*.adserver)

When used without parameters, will log current hostname + json payload to the console.  
New in [1.27.0](https://github.com/gorhill/uBlock/commit/578594bbd7c545b62f18267d640a605f8e07a53a) - second parameter can be used to limit logging to JSON payloads which stringified content match specified string or _regular expression_.

Examples:
 - `youthhealthmag.com##+js(json-prune, unit_list)`
 - `winfuture.de##+js(json-prune, adtagparameter, enabled)`
 - `imgsen.com##+js(json-prune, *, showTrkURL)` - will remove everything when needle matches, new in [1.35](https://github.com/gorhill/uBlock/commit/d338e4c4b6caf339873a60c9d48fde58e9a495ce)

If the site uses `eval` in lieu of `JSON.parse`, see: [evaldata-prune](#evaldata-prunejs-)

***

### xml-prune.js [↪](https://github.com/gorhill/uBlock/blob/bf690145c493acd86e578d7a860da238f0af72d4/assets/resources/scriptlets.js#L1672)
Removes an element from the specified XML.

New in [1.44.5b3](https://github.com/gorhill/uBlock/commit/bf690145c493acd86e578d7a860da238f0af72d4)

Parameters:
 - required, the selector of elements which are to be removed.
 - optional, a selector or xpath <sup>(New in [1.49.3rc15](https://github.com/gorhill/uBlock/commit/8ed78cfb234d3b9c615ee1deebea0ff0439ea7f3)</sup> that must have a match in the document for the pruning to occur. No selector means the pruning can be performed regardless.
 - optional, a URL which must be a match for the pruning to occur. If left blank, the pruning can be performed regardless.

Examples:
 - `cbs.com##+js(xml-prune, Period[id*="-roll-"][id*="-ad-"], , pubads.g.doubleclick.net/ondemand)`
 - `play.max.com##+js(xml-prune, xpath(//*[name()="Period"][not(.//*[name()="SegmentTimeline"])]), , .mpd)`

***

### m3u-prune.js [↪](https://github.com/gorhill/uBlock/blob/115f7bb68704c4fede763cbc2d07f1caf041274f/assets/resources/scriptlets.js#L1743)

New in [1.44.5b6](https://github.com/gorhill/uBlock/commit/115f7bb68704c4fede763cbc2d07f1caf041274f#diff-30b28769623e5478a0f68519eda037164484cfb444cb5a8e48518fa7bb32e658)

Sometimes sites serve real video content and video ads all in one place inside `.m3u8` files.
You can use `m3u-prune` to remove those ad segments.

Examples:
  - `player.theplatform.com##+js(m3u-prune, tvessaiprod.nbcuni.com, /theplatform\.com\/.*?\.m3u8/)`
  - `mephimtv.cc##+js(m3u-prune, /#EXT-X-DISCONTINUITY(.|\n){1\,100}#EXT-X-DISCONTINUITY/gm, mixed.m3u8)`

If the first argument is a regex with multine flag set, the scriptlet will execute the regex against the whole text, and remove matching text from the whole text (New in [1.47.5b10](https://github.com/gorhill/uBlock/commit/b3821e6869d45b5697c44922ee7242e35e11a29d)).

If the matching text does not contain whole lines, the text won't be removed, i.e. it is not allowed to remove only part of a line.

***

### noeval.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noeval.js)
Prevent web pages from using _`eval()`_, and report attempts to console. This should not be used as a generic filter due to the fact that it breaks many websites, including those using Cloudflare's DDoS protection.

Examples:
 - `solowarez.org##+js(noeval)`


***

### noeval-silent.js /
### ~silent-noeval.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noeval-silent.js)
Prevent web pages from using _`eval()`_. 


***

### noeval-if.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L340)
Prevent web pages from using _`eval()`_ on specific matching payloads.

Parameters:
 - optional, string/_regular expression_, matching in payload string.

Examples:
 - `orgyxxxhub.com##+js(noeval-if, replace)`

***

### ~no-floc.js~ [↪](https://github.com/gorhill/uBlock/blob/bfdc81e9e400f7b78b2abc97576c3d7bf3a11a0b/assets/resources/scriptlets.js#L668)

Obsolete: [FLoC ended its experiment in July of 2021](https://github.com/uBlockOrigin/uBlock-issues/issues/1553#issuecomment-1021680848).

New in [1.35.0](https://github.com/gorhill/uBlock/commit/bfdc81e9e400f7b78b2abc97576c3d7bf3a11a0b).

Defuses Google FLoC ("Federated Learning of Cohorts") tracking. Read more on https://amifloced.org/

uBlock Origin (uBO) ensures FLoC is opt-in. The generic filter `*##+js(no-floc)` in "uBlock filters -- Privacy" ensures the feature is disabled when using default settings/lists.

Users can opt-in to FLoC by adding a generic exception filter to their custom filters, `#@#+js(no-floc)`; or they can opt-in only for a specific set of websites through a more specific exception filter:

    example.com,shopping.example#@#+js(no-floc)

Solves [uBlockOrigin/uBlock-issues#1553](https://github.com/uBlockOrigin/uBlock-issues/issues/1553).

***

### no-fetch-if.js [↪](https://github.com/gorhill/uBlock/blob/b6ed83bc5c840431ed03cddaed1daeb395db3b0e/assets/resources/scriptlets.js#L586)

New in [1.31.3b9](https://github.com/gorhill/uBlock/commit/ba11a700139bbc648e4ae5b2bc7af90ef03db5df).

Defuses calls to `fetch()` by returning a promise which always resolve to an empty response.

Parameters:
 - optional, space-separated list of conditions which must be ALL fulfilled in order for the defusing to take place:
     - string/_regular expression_ matching in URL passed to `fetch()` call
     - colon-separated `name:value` pairs of [`init` option name](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters) and string/_regular expression_ matching in value of that option passed to `fetch()` call.

When used without parameters, the parameters passed to `no-fetch-if` will be logged to the console, as `uBO: fetch([...list of arguments...])`.

Examples:
 - `example.com##+js(no-fetch-if, method:HEAD)`
 - `example.com##+js(no-fetch-if, adsbygoogle.js)`
 - `example.com##+js(no-fetch-if, adsbygoogle.js method:HEAD)`
 - `example.com##+js(no-fetch-if, /adsbygoogle.js$/ method:/HEAD|POST/)`

***

### norafif.js /
### no-requestAnimationFrame-if.js [↪](https://github.com/gorhill/uBlock/blob/1de0e820b87fdd3717b9f2653baaa7a934075055/assets/resources/scriptlets.js#L522)

New in [1.27.0](https://github.com/gorhill/uBlock/commit/1de0e820b87fdd3717b9f2653baaa7a934075055).

**Defuses** calls to _`requestAnimationFrame()`_ function when parameter:
- **is not prefixed** with `!` and **matches** the stringified _callback_ argument to _`requestAnimationFrame()`_; OR
- **is prefixed** with `!` and  **does not match** the stringified _callback_ argument to _`requestAnimationFrame()`_.

Parameters:
 - optional, string/_regular expression_, matching in the stringified _callback_ argument passed to
requestAnimationFrame.

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`requestAnimationFrame()`_ to the console.

Examples:
 - `bloomberg.com##+js(norafif, paywall-inline-tout)`

***

### nosiif.js /
### no-setInterval-if.js [↪](https://github.com/gorhill/uBlock/blob/8f3d8cde7a9de45695d2706087701df59553c01b/assets/resources/scriptlets.js#L701)

New in [1.23.0](https://github.com/gorhill/uBlock/commit/9367a6015b8cbb6b49347b00a105aab8f24df861)

**Defuses** calls to _`setInterval()`_ function when parameters:
- **are not prefixed** with `!` and **match** the _`setInterval()`_ argument; OR
- **are prefixed** with `!` and **do not match** the _`setInterval()`_ argument.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer or literal `NaN` ("not a number", new in [1.28.2](https://github.com/gorhill/uBlock/commit/8f3d8cde7a9de45695d2706087701df59553c01b)), matching _interval_

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`setInterval()`_ to the console.

Examples:
 - `jpidols.tv##+js(nosiif)`
 - `finanzen.*##+js(nosiif, nrWrapper)`
 - `yachtrevue.at##+js(nosiif, text/css, 10)`


***

### nostif.js /
### no-setTimeout-if.js [↪](https://github.com/gorhill/uBlock/blob/8f3d8cde7a9de45695d2706087701df59553c01b/assets/resources/scriptlets.js#L776)

New in [1.23.0](https://github.com/gorhill/uBlock/commit/9367a6015b8cbb6b49347b00a105aab8f24df861)

**Defuses** calls to _`setTimeout()`_ function when parameters:
- **are not prefixed** with `!` and **match** the _`setTimeout()`_ argument; OR
- **are prefixed** with `!` and **do not match** the _`setTimeout()`_ argument.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer or literal `NaN` ("not a number", new in [1.28.2](https://github.com/gorhill/uBlock/commit/8f3d8cde7a9de45695d2706087701df59553c01b)), matching _delay_

Use with `/^/` parameter to defuse all calls unconditionally.

When used without parameters, will log calls to _`setTimeout()`_ to the console.

<sub>Test page: https://gorhill.github.io/uBlock/tests/scriptlet-injection-filters-1.html</sub>

Examples:
 - `computerbild.de##+js(nostif, ())return)`
 - `lablue.*##+js(nostif, push, 500)`

In [1.31.3b11](https://github.com/gorhill/uBlock/commit/ba11a700139bbc648e4ae5b2bc7af90ef03db5df) aliased as `setTimeout-defuser.js` for backward compatibility.

***

### nowebrtc.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L721)
Disables WebRTC by preventing web pages from using [_`RTCPeerConnection()`_](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). Report attempts in console.

Examples:
 - `x1337x.*##+js(nowebrtc)`

***

### no-xhr-if.js [↪](https://github.com/gorhill/uBlock/blob/745fbd1c02b7179052ba97f51c54f7cb000636f0/assets/resources/scriptlets.js#L1171)

New in [1.38.0](https://github.com/gorhill/uBlock/commit/745fbd1c02b7179052ba97f51c54f7cb000636f0).

Defuses [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest) network requests by returning empty response. Based on [`no-fetch-if.js`](#no-fetch-ifjs-).

Parameters:
 - optional, space-separated list of conditions which must be ALL fulfilled in order for the defusing to take place:
     - string/_regular expression_ matching in URL passed to XMLHttpRequest `open()` call
     - colon-separated `name:value` pairs of [XMLHttpRequest method `open()`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open#parameters) parameter names  (only `method` and `url` currently supported) and string/_regular expression_ matching in value of passed argument.

When used without parameters, the parameters passed to `no-xhr-if` will be logged to the console, as `uBO: xhr.open(...list of arguments...)`.

Examples:
 - `example.com##+js(no-xhr-if, method:HEAD)`
 - `example.com##+js(no-xhr-if, adsbygoogle.js)`
 - `example.com##+js(no-xhr-if, adsbygoogle.js method:HEAD)`
 - `example.com##+js(no-xhr-if, /adsbygoogle.js$/ method:/HEAD|POST/)`

***

### ~ra.js~ /
### ~remove-attr.js [↪](https://github.com/gorhill/uBlock/blob/0f330c7359567587df6c35e9108b75c339533a56/assets/resources/scriptlets.js#L658)~

Deprecated by [`:remove-attr()`](./Static-filter-syntax#subjectremove-attrarg-subjectremove-classarg)

**Filter authors must use the new operator instead of the `+js()` counterpart.**

Removes attribute(s) from DOM tree node(s). By default will run only once when the initial HTML document has been completely loaded and parsed but sub-resources such as scripts, images, stylesheets and frames are still loading.

Parameters:
 - required, attribute or list of attributes joined by `|`
 - optional, _CSS selector_, specifies nodes from which attributes will be removed
 - optional, new in [1.33](https://github.com/gorhill/uBlock/commit/0f330c7359567587df6c35e9108b75c339533a56), one or more space-separated tokens dictating the behavior of the scriptlet
    - `asap`: added in [1.36.1b2](https://github.com/gorhill/uBlock/commit/35d7406214e39fa5ad5c73cfab3eecb0eb7c8b7f), execute as soon as possible, do not wait for DOM to become available.
    - `stay`: This tells the scriplet to stay active and act on document changes.
    - `complete`: This tells the scriplet to start acting only when the document is complete, i.e. once all secondary resources have been loaded.

Examples:
 - `userscloud.com##+js(ra, onclick, .btn-icon-stacked)`
 - `magesy.*,majesy.*##+js(ra, oncontextmenu)`
 - `zerodot1.gitlab.io##+js(ra, oncontextmenu|onselectstart|ondragstart)`
 - `example.com##+js(remove-attr, class, .j-mini-player, stay)`


***

### ~rc.js~ /
### ~remove-class.js~ [↪](https://github.com/gorhill/uBlock/blob/3160bc8ccdab2b7dbc906ea213b29a4c04120be1/assets/resources/scriptlets.js#L757)

Deprecated by [`:remove-class()`](./Static-filter-syntax#subjectremove-attrarg-subjectremove-classarg)

**Filter authors must use the new operator instead of the `+js()` counterpart.**

New in [1.26.0](https://github.com/gorhill/uBlock/commit/49d9929191461cc8534ebf5707d94a5970945bde).

Removes classes from DOM tree node(s). By default will run only once after page load. Syntax based on [`remove-attr.js`](#remove-attrjs-)

Parameters:
 - required, class name or list of class names joined by `|`
 - optional, _CSS selector_, specifies nodes from which classes should be removed
 - optional, new in [1.36](https://github.com/gorhill/uBlock/commit/2de24a11843df653173e50b9e952052361c64147), one or more space-separated tokens dictating the behavior of the scriptlet
    - `stay`: This tells the scriplet to stay and act on DOM changes, while the default behavior is to act only once when the document becomes interactive.
    - `complete`: This tells the scriplet to start acting only when the document is complete, i.e. once all secondary resources have been loaded, while the default is to start acting when the document is interactive - which is earlier than when the document is complete.

Examples:
- `danskebank.fi##+js(rc, cookie-consent-banner-open, html)` [Picture of the element](https://images2.imgbox.com/68/2b/tdWI9hBG_o.png)


***

### rpnt.js /
### replace-node-text.js [↪](https://github.com/gorhill/uBlock/blob/f3b720d532c7a42a6ad5167e3b6f860004b4c2b6/assets/resources/scriptlets.js#L2570)

#### _Trusted scriptlet_

New in [1.49.3b16](https://github.com/gorhill/uBlock/commit/41876336db48292de06707adfa5e97dab74297d2)

Replace text instance(s) with another text instance inside specific DOM nodes.

By default, the scriptlet will bail out when the document itself has been fully loaded, i.e. when `DOMContentLoaded` event is fired.

The mutation observer of this scriptlet can be a significant overhead for pages with dynamically updated DOM, and in most cases the scriptlet is useful only for DOM changes occurring before the `DOMContentLoaded` event, so the default is to quit out when that event is received ("quit out" means discarding the mutation observer and having the scriptlet garbage-collected by the JS engine).

Parameters:
 - required, the name of the node for which the text content must be substituted. Valid node names can be found at:
https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeName
 - required, A string or regex to find in the text content of the node as the target of substitution
 - optional, the replacement text. Can be omitted if the goal is to delete the text which
matches the pattern. Cannot be omitted if extra pairs of parameters have to be used (see below)

Optionally, extra pairs of parameters (tokens) can be used to modify the behavior of the scriptlet.

Tokens:
 - `condition, pattern`: A string or regex which must be found in the text content of the node
in order for the substitution to occur
 - `sedCount, n`: This will cause the scriptlet to stop after `n` instances of substitution. Since a mutation oberver is used by the scriptlet, it's advised to stop it whenever it becomes pointless. Default to zero, which means the scriptlet never stops
 - `stay, 1`: Force the scriptlet to stay at work forever
 - `quitAfter, ms`: This tells the scriptlet to quit `ms` milliseconds after the page has been loaded, i.e. after the `DOMContentLoaded` event has been fired
 - `log, 1`: This will cause the scriptlet to output information at the console, useful as a debugging tool for filter authors

Examples:
 - `example.com##+js(rpnt, #text, /^Advertisement$/)`
 - `example.com##+js(rpnt, #text, Example Domain, Changed, condition, Example, stay, 1)`
 - `example.com##+js(rpnt, script, /devtoolsDetector\.launch\(\)\;/, , sedCount, 1)`

Also see: [remove-node-text](#remove-node-textjs-)

***

### rmnt.js /
### remove-node-text.js [↪](https://github.com/gorhill/uBlock/blob/f3b720d532c7a42a6ad5167e3b6f860004b4c2b6/assets/resources/scriptlets.js#L2531)

New in [1.49.3rc15](https://github.com/gorhill/uBlock/commit/2bb446797a12086f2eebc0c8635b671b8b90c477)

Remove the *whole* text of a DOM node.

By default, the scriptlet will bail out when the document itself has been fully loaded, i.e. when `DOMContentLoaded` event is fired.

The mutation observer of this scriptlet can be a significant overhead for pages with dynamically updated DOM, and in most cases the scriptlet is useful only for DOM changes occurring before the `DOMContentLoaded` event, so the default is to quit out when that event is received ("quit out" means discarding the mutation observer and having the scriptlet garbage-collected by the JS engine).

Parameters:
 - required, the name of the node for which the text content must be removed. Valid node names can be found at:
https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeName
 - required, A string or regex to find in the text content of the node as the target of removing

Optionally, extra pairs of parameters (tokens) can be used to modify the behavior of the scriptlet.

Tokens:
 - `condition, pattern`: A string or regex which must be found in the text content of the node
in order for the removing to occur
 - `sedCount, n`: This will cause the scriptlet to stop after `n` instances of removing. Since a mutation oberver is used by the scriptlet, it's advised to stop it whenever it becomes pointless. Default to zero, which means the scriptlet never stops
 - `stay, 1`: Force the scriptlet to stay at work forever
 - `quitAfter, ms`: This tells the scriptlet to quit `ms` milliseconds after the page has been loaded, i.e. after the `DOMContentLoaded` event has been fired
 - `log, 1`: This will cause the scriptlet to output information at the console, useful as a debugging tool for filter authors

Examples:
 - `example.com##+js(rmnt, #text, Example)`
 - `example.com##+js(rmnt, #text, Example, condition, Exa)`
 - `example.com##+js(rmnt, script, timeLeft)`

Also see: [replace-node-text](#replace-node-textjs-)

***

### href-sanitizer.js [↪](https://github.com/gorhill/uBlock/blob/d7b7dea7faaf17486d5c54454852c4a117f50fd1/assets/resources/scriptlets.js#L1845)

#### _Experimental_

New in [1.47.5b4](https://github.com/gorhill/uBlock/commit/e123256eaf64be19f81eba123970db07b45eb0ae)

Parameters:
 - required, a CSS selector which matches the elements for which the scriptlet should replace the `href` attribute with the text content of the element, if ALL the following conditions are met:
     - The element is a link (`<a>`) element
     - The link element has an existing `href` attribute
     - The text content of the element is a valid `https`-based URL
 - optional, the attribute from which to extract the text to be used for the `href` attribute of the link, otherwise the text content of the element will be used.
     - If the second parameter starts with `?`, the scriptlet will look up the value of the search parameter which name is what comes after the `?`. (<sup>New in [1.49.3rc15](https://github.com/gorhill/uBlock/commit/56e1d92dbd65e6168620053b1fec4c21c03d664e)</sup>)

Examples:
 - `vk.com##+js(href-sanitizer, a[href^="/go?to="][title], [title])`
 - `vk.com##+js(href-sanitizer, a[href^="/away.php?to="][title], ?to)`
 - `<a href="https://app.adjust.com/2uo1qc?redirect=https%3A%2F%2Fplay.google.com%2Fstore%2Fapps%2Fdetails%3Fid%3Dorg.mozilla.firefox&amp;campaign=www.mozilla.org&amp;adgroup=mobile-android-page">Text</a>`:
   `mozilla.org##+js(href-sanitizer, a[href^="https://app.adjust.com/"][href*="?redirect="], ?redirect)`

Solves [uBlockOrigin/uBlock-issues#2531](https://github.com/uBlockOrigin/uBlock-issues/issues/2531).

***

### refresh-defuser.js [↪](https://github.com/gorhill/uBlock/blob/c0a43b0d32e38aa3858644db20fc69a7b0c85e82/assets/resources/scriptlets.js#L726)

New in [1.38.7b3](https://github.com/gorhill/uBlock/commit/c0a43b0d32e38aa3858644db20fc69a7b0c85e82)

Attempts to defuse reloading of a document through a [meta "refresh" tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#attr-http-equiv). Will stop navigation (call [`window.stop()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/stop)) at specified delay.

Parameters:
 - optional, number (float), number of seconds until the page will be reloaded / when defuser should run. Will be derived from source tag when not specified.

***

### set.js /
### set-constant.js [↪](https://github.com/gorhill/uBlock/blob/a9e6f9c72c920d68a6e5b01b844ad39e6f2e02b0/assets/resources/scriptlets.js#L878)
Creates _property_ and initializes it with a value from a predefined set.

Scriptlet will succeed only when:
 - original _property_ is `undefined` (scriptlet is called early enough) or `null`<sup>[1.25.0](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **OR**
 - new _property_ written by `set.js` is `undefined` or `null`<sup>[1.25.0](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **OR**
 - type of original _property_ is equal to type of new _property_

Value set by scriptlet can be overwritten by page script when:
 - current _property_ was not set to `undefined` or `null`<sup>[1.25.0](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **AND**
 - new _property_ is not `undefined` or `null`<sup>[1.25.0](https://github.com/gorhill/uBlock/commit/c7dc65fe33ed58ff2bad10ce4a8848b97c8591ce)</sup> **AND**
 - type of original _property_ is different than type of new _property_ 

Parameters:
 - required, _property_ (chain of properties joined by `.`) attached to window object
 - required, possible values:
     - positive decimal integer, no sign, with maximum value of 0x7FFF (32767)
     - one value from set of predefined constants:
         - `undefined`
         - `false`
         - `true`
         - `null`<sup>[2018-11-24](https://github.com/uBlockOrigin/uAssets/commit/8fd3f7e3a344e5fc29344f1ba914e82457eb1d13#diff-8809d5783978a0b5b88f93d7dab99de0)</sup>
         - `noopFunc` - function with empty body
         - `trueFunc` - function returning true
         - `falseFunc` - function returning false
         - `''` - empty string<sup>[2019-01-06](https://github.com/uBlockOrigin/uAssets/commit/5051610f0e2374955a03c54be42bbbe9115f05c7#diff-8809d5783978a0b5b88f93d7dab99de0R2132)</sup>
         - `[]` - empty array<sup>[1.36](https://github.com/gorhill/uBlock/commit/ce801b952b5777775385efc00479405af54edbc9)</sup>
         - `{}` - empty object<sup>[1.36](https://github.com/gorhill/uBlock/commit/ce801b952b5777775385efc00479405af54edbc9)</sup>
 - optional, to defer execution of `set-constent` , possible values:
     - _not present_: execute immediately
     - 1: execute immediately
     - `interactive`, `end`, `2`: set the constant when the event `DOMContentInteractive` is fired
     - `complete`, `idle`, `3`: set the constant when the event `load` is fired


3rd parameter and beyond are tokens which modify the behavior of `set-constant`.

Tokens:
 - New in [1.49.3b4](https://github.com/gorhill/uBlock/commit/e1500ee88d2524da0c93e85b8855d0671a3c6cdb), solves [uBlockOrigin/uAssets#7320](https://github.com/uBlockOrigin/uAssets/issues/7320):
     - `interactive`, `end`, `2`: set the constant when the event `DOMContentInteractive` is fired
     - `complete`, `idle`, `3`: set the constant when the event `load` is fired
 - New in [1.49.3b13](https://github.com/gorhill/uBlock/releases/tag/1.49.3b13), solves [uBlockOrigin/uBlock-issues#2615](https://github.com/uBlockOrigin/uBlock-issues/issues/2615):
     - `asFunction`: the constant will be a function returning the specified value
     - `asCallback`: the constant will be a function returning a function returning the specified value
     - `asResolved`: the constant will be a promise resolving to the specified value
     - `asRejected`: the constant will be a promise failing with the specified value. 

Examples:
 - `kompetent.de##+js(set, Object.keys, trueFunc)`
 - `t-online.de##+js(set, abp, false)`
 - `identi.li##+js(set, t_spoiler, 0)`
 - `joysound.com##+js(set, document.body.oncopy, null, 3)`


<details>
<summary>Parameters (when using named arguments)</summary>

New in [1.49.3b4](https://github.com/gorhill/uBlock/commit/e1500ee88d2524da0c93e85b8855d0671a3c6cdb)

 - "prop"
 - "value"
 - "runAt"

Examples:
 - `example.com##+js(set, {"prop": "x", "value": "true", "runAt": 1})`

</details>

Also see: [trusted-set-constant](#trusted-set-constantjs-)

***


### trusted-set.js /
### trusted-set-constant.js [↪](https://github.com/gorhill/uBlock/blob/f3b720d532c7a42a6ad5167e3b6f860004b4c2b6/assets/resources/scriptlets.js#L2605)

#### _Trusted scriptlet_

Behaves exactly like [set-constant](#set-constantjs-), except that any arbitrary JSON-compatible value can be set.

By default the value is treated as a string, which can be anything.

If the value starts with `{` and ends with `}`, the value will be JSON-parsed, and the `value` property of the resulting object will be used.

Solves: https://github.com/uBlockOrigin/uAssets/discussions/18185#discussioncomment-5977456

Examples:
 - `example.com##+js(trusted-set, prop, { value: 100000 })`
 - `example.com##+js(trusted-set, prop, { value: "yes" })`
 - `example.com##+js(trusted-set, prop, { value: [ "one", "two", 3 ]})`
 - `example.com##+js(trusted-set, prop, { value: { url: "about:blank" }})`

Also see: [set-constant](#set-constantjs-)

***

### ~sil.js~ /
### ~setInterval-logger.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L500)

Deprecated by [`no-setInterval-if.js`](#no-setinterval-ifjs-)

Removed in [1.22.0](https://github.com/gorhill/uBlock/commit/c5536577b29cd0bcd401f7ecd143a921acdb4eb6).

Logs to the console calls to _`setInterval()`_ function.


***

### ~std.js~ /
### ~setTimeout-defuser.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L515)

Deprecated by [`no-setTimeout-if.js`](#no-settimeout-ifjs-)

Defuses calls to _`setTimeout()`_ function for specified matching callbacks and delays by setting callback function to noop.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional, decimal integer, matching _delay_


***

### nano-sib.js /
### nano-setInterval-booster.js [↪](https://github.com/gorhill/uBlock/blob/001f5a650084ffa4842f9361bc975ca724bd69ba/assets/resources/scriptlets.js#L463)
Adjusts interval for specified _`setInterval()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching interval. New in [1.33.0](https://github.com/gorhill/uBlock/commit/001f5a650084ffa4842f9361bc975ca724bd69ba): `*` will match any interval.
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, interval multiplier

Examples:
 - `identi.li##+js(nano-sib, , ,0.02)`
 - `platinmods.*##+js(nano-sib)`
 - `1ink.cc##+js(nano-sib, mSec, 1050)`


***

### spoof-css.js [↪](https://github.com/gorhill/uBlock/blob/f3b720d532c7a42a6ad5167e3b6f860004b4c2b6/assets/resources/scriptlets.js#L2443)
Spoof the CSS property value when `getComputedStyle()` or `getBoundingClientRect()` are used.

Parameters:
 - required, a valid CSS selector which matches the elements for which the spoofing must apply
 - required, a CSS property name (can be dashed- or camel-cased)
 - required, the value to return regardless of the currently computed value

Examples:
 - `example.com##+js(spoof-css, .ad, clip-path, none)`

There can be any number of selectors, all separated by escaped commas:

 - `example.com##+js(spoof-css, a[href="x.com"]\, .ads\, .bottom, clip-path, none)`

There can be any number of property-name/property-value pairs, all separated by commas:

 - `example.com##+js(spoof-css, .ad, clip-path, none, display, block)`

A special property-name/property-value pair `debug/1` can be used to force the browser to break when `getComputedStyle()` or `getBoundingClientrect()` is called, useful to help pinpoint usage of those calls in the page's source code:

 - `example.com##+js(spoof-css, .ad, debug, 1)`

Solves [uBlockOrigin/uBlock-issues#2618](https://github.com/uBlockOrigin/uBlock-issues/issues/2618).

***

### nano-stb.js /
### nano-setTimeout-booster.js [↪](https://github.com/gorhill/uBlock/blob/001f5a650084ffa4842f9361bc975ca724bd69ba/assets/resources/scriptlets.js#L513)
Adjusts delay for specified _`setTimeout()`_ callbacks.

Parameters:
 - optional, string/_regular expression_, matching in stringified callback function
 - optional - defaults to 1000, decimal integer, matching delay. New in [1.33.0](https://github.com/gorhill/uBlock/commit/001f5a650084ffa4842f9361bc975ca724bd69ba): `*` will match any delay.
 - optional - default to 0.05 (20x faster), float, capped at 50 times for up and down, delay multiplier

Examples:
 - `bdupload.*##+js(nano-stb)`
 - `imgrock.*##+js(nano-stb, /.?/, 4000)`


***

### ~sharedWorker-defuser.js~ [↪](https://github.com/uBlockOrigin/uAssets/blob/2c68a4f5456e4677cec76f2784d2c1d7abc36efb/filters/resources.txt#L1822)
Removed. Deprecated by `$csp` filter option.  
Defuses sharedWorker by passing empty worker file (Blob URL) for specified worker URLs

Parameters:
 - optional, string/_regular expression_, matching in worker URL


***

### webrtc-if.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L556)
Allows opening RTC connections to matching [RTCIceServer](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceServer) only.

Parameters:
 - required, string/_regular expression_, matching in `RTCIceServer` `urls`, `username` or `credential`.


***

### window-close-if.js [↪](https://github.com/gorhill/uBlock/blob/8d7469afcfae7dabefe819eb513a0ba026ed9dd7/assets/resources/scriptlets.js#L1273)

New in [1.39.3b10](https://github.com/gorhill/uBlock/commit/c198b9a748265c0e1ce7f5bad4528d5bf6ce8161).

Closes fresh browser tabs of the specified page. Can also be used to close tabs which have been opened from other applications. Can be narrowed down to specific path by parameter. Whole browser window will be closed if it's the last/only tab (depends on browser configuration).

Improvements:
- [1.44.3b11](https://github.com/gorhill/uBlock/commit/65a056107210796426033ebe2eebb89a98c93a23), If the argument to the `window-close-if` scriptlet is a regex, the
match will be against _the whole location URL_, otherwise the
match will be against the part+query part of the location URL.

Parameters:

 - optional, string, matching in the path and query part of the web page address or _regular expression_, matching in the whole location URL. 

Examples:

 - `acestream.com##+js(window-close-if, /plan/select?popup=noads)`
 - `example.com##+js(window-close-if, /^/)` - will close all new tabs going to `example.com` on _any_ site.
 - `hostdl.com##+js(window-close-if, /^https?://(www\.)?hostdl\.com/)` - will close all new tabs matching either only base domain or www one (i.e. **not** `login.hostdl.com`).

***

### nowoif.js /
### window.open-defuser.js [↪](https://github.com/gorhill/uBlock/blob/b98b2fc52becce75b858b0a6040328e291fdae29/src/web_accessible_resources/window.open-defuser.js)
Prevent opening new windows by [_`window.open()`_](https://developer.mozilla.org/en-US/docs/Web/API/Window/open) when URL positively or negatively matches to specific string.

Improvements:

- [1.29.2](https://github.com/gorhill/uBlock/commit/d544543ab580930733c4def8817fbff251ad10ce), third parameter can now configure behavior of the scriptlet.
- [1.27.0](https://github.com/gorhill/uBlock/commit/6259f88598b2d3e044679d6fe0fdb6eb16f6c479), `nowoif.js` alias is now available.
- 1.26.0 ([one](https://github.com/gorhill/uBlock/commit/b27848a060eee961e2403192097448467b3bc7b5), [two](https://github.com/gorhill/uBlock/commit/0f33f2386d147e4930b402a07418da670524e43f)),  
if second argument is present and a valid integer value, the defuser will return a valid window object even though no popup window is opened. The returned window object will cease to be valid after the specified number of seconds. If not present, no window will be opened and the scriptlet will return `null`.

Use third parameter (set it to `log`) to log `window.open()` parameters, and log access to attributes of returned `window` object.

Parameters:
 - optional, string/_regular expression_, prefixed by `!` for negation, matching in URL parameter passed to _`window.open()`_,
 - optional, positive decimal integer, number of seconds after returned `window` object will be invalidated.
 - optional, space-separated tokens,
    - `log`:  
    Cause the scriptlet to log information regarding how `window.open()` is used by the page on which the scriptlet is used. Useful only to filter creators.
    - `obj`:  
    Use an `object` element instead of `iframe` element (default) as a decoy to be used in place of a popup window, when the page requires a valid `window` instance to be returned.
    - before [1.29.2](https://github.com/gorhill/uBlock/commit/d544543ab580930733c4def8817fbff251ad10ce) any value (for example `-`) was turning on logging.

Parameters syntax deprecated after 1.26.0:
 - optional - defaults to "matching", nothing or `1` for "matching", `0` for "not matching",
 - optional, string/_regular expression_, matching/not matching in URL parameter passed to _`window.open()`_

Examples:
 - `file-up.org##+js(window.open-defuser)`


***

### window.name-defuser [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L624)
Clears `window.name` _property_ which can be misused for tracking purposes.

Parameters:
 - none


***

### overlay-buster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L633)
Experimental, gets rid of overlay dialogs, works for ~30s after page load. Preferred way to handle overlays is to use standard cosmetic filters and optionally [style injection](./Static-filter-syntax#style).


***

### alert-buster.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L691)
Disables [_`alert()`_](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) dialog boxes by redirecting messages to console.


***

## Defuser scriptlets



### ampproject_v0.js /
### ~ampproject.org/v0.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/ampproject_v0.js)
Removes animation (artificial 8s delay) added to desktop pages supporting AMP, when ampproject.org scripts are blocked.

### fingerprint2.js [↪](https://github.com/gorhill/uBlock/blob/master/src/web_accessible_resources/fingerprint2.js)
Fingerprintjs2 shim.

### fingerprint3.js [↪](https://github.com/gorhill/uBlock/blob/master/src/web_accessible_resources/fingerprint3.js)
FingerprintJS v3 shim.

### nobab.js /
### ~bab-defuser.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/nobab.js)
Defuses BlockAdblock. Prevents executing of _`eval()`_ on sets of predefined payloads.

### nobab2.js [↪](https://github.com/gorhill/uBlock/blob/d17d634b7c95261c376b42c0fb0a65fc9eff32ae/src/web_accessible_resources/nobab2.js)
Redirect resource. Defuses BAB 4.2b.

### nofab.js /
### ~fuckadblock.js-3.2.0~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/nofab.js)
Convenience, Sanitize `FuckAdBlock`, `BlockAdBlock`, `SniffAdBlock`, `fuckAdBlock`, `blockAdBlock`, `sniffAdBlock` properties.
Often used as redirect in network filters. TODO: copy to redirect?

### popads-dummy.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/popads-dummy.js)
Convenience, sets static properties (`PopAds`, `popns`)

### popads.js /
### ~popads.net.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/popads.js)
Convenience, abort-on-property-write.js (`PopAds`, `popns`), _throws_ "`magic`"

### prebid-ads.js [↪](https://github.com/gorhill/uBlock/blob/master/src/web_accessible_resources/prebid-ads.js)
New in 1.41.0

Prebid-ads shim. `canRunAds`/`isAdBlockActive`?

### adfly-defuser.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L805)
Defuses anti-blocker on adfly shortened links.

***

## Empty redirect resources
These are smallest/shortest/fastest to execute files. Should be used in network filters as a parameter to `$redirect` option.
They purpose is to mislead page to think that real files have been served.

### Available resources
 - Images
	- `1x1.gif` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/1x1.gif)
	- `2x2.png` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/2x2.png)
	- `3x2.png` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/3x2.png)
	- `32x32.png` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/32x32.png)
 - Source code
	- `noop.css` [↪](https://github.com/gorhill/uBlock/blob/4564e3a9b8d3cb2afb70ebd2161271f6b9b969bc/src/web_accessible_resources/noop.css)
	- `noop.html` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.html)
	- `noop.js` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.js)
	- `noop.txt` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop.txt)
 - Media files
	- `noop-0.1s.mp3` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop-0.1s.mp3)
	- `noop-0.5s.mp3` [↪](https://github.com/gorhill/uBlock/blob/c521479ef9d9676e08fcd6751fde7330dce189e7/src/web_accessible_resources/noop-0.5s.mp3)
	- `noop-1s.mp4` [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/noop-1s.mp4)
 - Special purpose
    - `none`

        reserved token, can be used to disable specific redirect filters. Starting with [1.31.0](https://github.com/gorhill/uBlock/commit/157cef6034a8ec926c1e59c7e77f0a1fcbef473c), classic exception filters and `badfilter` option can be used.
    - `click2load.html`

        for embedded `<iframe>` elements. New in [1.31.0](https://github.com/gorhill/uBlock/commit/59169209850c54c31d94990f0c956281fe43eb03) (also [2e5d32e9](https://github.com/gorhill/uBlock/commit/2e5d32e96798dd55f3fae66d7091645ff7ad3784), [46d7f8a7](https://github.com/gorhill/uBlock/commit/46d7f8a70c937441545db9c53df2647081ee9d12)). Frames redirected to this resource will not be collapsed, instead, widget with clickable and selectable frame source link will be displayed. Clicking the icon next to source link will open frame content in new tab. Clicking the widget content will unblock and load original frame content.

Example rule:

`||ad.server.com/$script,redirect=noop.js,domain=www.google.com`

***

## URL-specific sanitized redirect resources (surrogates)



### addthis_widget.js /
### ~addthis.com/addthis_widget.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/addthis_widget.js)

### amazon_ads.js /
### ~amazon-adsystem.com/aax2/amzn_ads.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/amazon_ads.js)

### amazon_apstag.js [↪](https://github.com/gorhill/uBlock/blob/f842ab6d3c1cf0394f95d27092bf59627262da40/src/web_accessible_resources/amazon_apstag.js)
New in [1.27.0](https://github.com/gorhill/uBlock/commit/f842ab6d3c1cf0394f95d27092bf59627262da40).

### monkeybroker.js /
### ~d3pkae9owd2lcf.cloudfront.net/mb105.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/monkeybroker.js)

### doubleclick_instream_ad_status.js /
### ~doubleclick.net/instream/ad_status.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/doubleclick_instream_ad_status.js)

### google-analytics_ga.js /
### ~google-analytics.com/ga.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_ga.js)

### google-analytics_analytics.js /
### ~google-analytics.com/analytics.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_analytics.js)

### google-analytics_inpage_linkid.js /
### ~google-analytics.com/inpage_linkid.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_inpage_linkid.js)

### google-analytics_cx_api.js /
### ~google-analytics.com/cx/api.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/google-analytics_cx_api.js)

### google-ima.js [↪](https://github.com/gorhill/uBlock/blob/93e5133783301c0329b3ce8f9e6079badd06d62d/src/web_accessible_resources/google-ima.js)

### googletagservices_gpt.js /
### ~googletagservices.com/gpt.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googletagservices_gpt.js)

### googletagmanager_gtm.js /
### ~googletagmanager.com/gtm.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googletagmanager_gtm.js)

### googlesyndication_adsbygoogle.js /
### ~googlesyndication.com/adsbygoogle.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/googlesyndication_adsbygoogle.js)

### scorecardresearch_beacon.js /
### ~scorecardresearch.com/beacon.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/scorecardresearch_beacon.js)

### outbrain-widget.js /
### ~widgets.outbrain.com/outbrain.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/outbrain-widget.js)

### hd-main.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/hd-main.js)

### ~disqus_forums_embed.js AND disqus_embed.js~ /
### ~disqus.com/forums/*/embed.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/disqus_forums_embed.js) AND ~disqus.com/embed.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/disqus_embed.js)

Removed in [1.29.0](https://github.com/gorhill/uBlock/commit/7c22a312945a2bff41a2b5696a7e54f1c4c01cf2).

***

## Other
Deprecated by general purpose scriptlets / outdated (please move to proper section if still used).

***

### golem.de.js [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/assets/resources/scriptlets.js#L756)
Deprecated, addEventListener-defuser

***

### chartbeat.js /
### ~static.chartbeat.com/chartbeat.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/chartbeat.js)
Deprecated, sets static properties (`pSUPERFLY.activity`, `pSUPERFLY.virtualPage`)

### ligatus_angular-tag.js /
### ~ligatus.com/*/angular-tag.js~ [↪](https://github.com/gorhill/uBlock/blob/a94df7f3b27080ae2dcb3b914ace39c0c294d2f6/src/web_accessible_resources/ligatus_angular-tag.js)
Deprecated, sets static properties (`adProtect`, `uabpdl`, `uabDetect`)


***

## Glossary



 - `throw`:            https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/throw
 - `eval()`:           https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval
 - `setInterval()`     https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setInterval
 - `setTimeout()`      https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/setTimeout)
 - regular expression: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Writing_a_regular_expression_pattern
 - element:            https://developer.mozilla.org/en-US/docs/Web/HTML/Element
 - property:           https://developer.mozilla.org/en-US/docs/Glossary/property/JavaScript
 - method:             https://developer.mozilla.org/en-US/docs/Glossary/Method
 - CSS selector:       https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
