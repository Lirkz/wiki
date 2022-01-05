[[Back to Wiki home|Home]]

***

The _"Advanced settings"_ page contains settings which are experimental, or which are of interest to advanced users who want more control over how uBO behaves internally. Some of these settings are left undocumented, on purpose -- do not open issues about these.

These advanced settings can be easily accessed only when the setting [_"I am an advanced user"_](./Advanced-user-features) in the _Settings_ pane in the dashboard is checked, but will persist and work even when the setting [_"I am an advanced user"_](./Advanced-user-features) is not checked:

![Click on the _cogs_ icon](https://cloud.githubusercontent.com/assets/585534/20042797/2800dcd4-a44e-11e6-9bc8-a5e0c960262c.png)

The advanced settings available are described below. Be aware that those settings may change or be removed in the future, or more may be added.

If you want to reset a specific setting to its default value, just delete the value, uBO will fill the missing value with the default one.

If you want to reset all settings to their default values, delete everything then press _"Apply changes"_.

**Important:** Some advanced settings are purposefully left undocumented, they are for internal use during development, or their long term availability has not yet been decided. Do not open an issue about these purposefully undocumented settings -- the issue will be closed without further comment.

***

#### `allowGenericProceduralFilters`

Default: `false`.

uBO [1.20.0](https://github.com/gorhill/uBlock/commit/1caff7429eceabc712b98b25b5c3929f430d6654) and above.

If set to `true`, generic [procedural cosmetic filters](./Procedural-cosmetic-filters) will no longer be discarded as invalid.

Whenever this setting is toggled, the user is responsible of forcing a reload of all filter lists so as to allow uBO to process differently any existing generic procedural cosmetic filters.

***

#### `assetFetchTimeout`

Default: `30` seconds.

The number of seconds after which uBO throws an error when a remote server fails to respond to a request.

***

#### `autoCommentFilterTemplate`

Default: `{{date}} {{origin}}`.

uBO 1.17.7b2 and above.

Template used to create comments in My filters, when new filter is created by Element Picker or from The Logger.

Placeholders are identified by `{{...}}`. Currently supported placeholders:

- `{{date}}`: will be replaced with current date
- `{{time}}`: will be replaced with current time
- `{{hostname}}`: will be replaced with the hostname of the URL address for which the filter(s) was created
- `{{origin}}`: will be replaced by origin part of the address for which the filter(s) was created
- `{{url}}`: new in [1.30.3b6](https://github.com/gorhill/uBlock/commit/46ec9694115d79ef3b380f366a8332ead267ef49), will be replaced by full URL of the page for which a filter is created in Element Picker. For filters added from The Logger, replaced by origin part of the URL.

If no placeholder is found in `autoCommentFilterTemplate`, this will disable auto-commenting. So one can use `-` or `none` to disable auto-commenting.

***

#### `autoUpdateAssetFetchPeriod`

Default: `120` seconds.

When the auto-updater kicks in and an asset in need of update is fetched, this is the number of seconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load on CPU and memory as a result of loading/parsing/compiling the filter lists which have been updated.

***

#### `autoUpdateDelayAfterLaunch`

Default: `180` secs.

uBO [1.20.0](https://github.com/gorhill/uBlock/commit/72d9758faa40a49f00d2a4671c9db2f519471f0d) and above.

The number of seconds to wait after launch before an auto-update session<sup>[1]</sup> is started.

<sub>[1] "Update session" means that uBO will lookup and update assets deemed out of date, if any.</sub>

***

#### `autoUpdatePeriod`

Default: `4` hours.

Before [1.32.5rc0](https://github.com/gorhill/uBlock/commit/174731851e5074099ac57d3b2122447cd1f60286): `7` hours.

The time to wait in hours between each update session. uBO will always start an update session a few minutes after launch when auto-update is enabled. Once that first update session is completed, uBO will wait `autoUpdatePeriod` hours before starting a new update session.

***

#### `benchmarkDatasetURL`

Default: `unset`.

uBO [1.25.2](https://github.com/gorhill/uBlock/commit/b784b7d5693751844bdb6e7ec7bd30368b2598a8) and above.

URL from where the _benchmark_ _dataset_ will be fetched. This allows to launch benchmark operations from within published versions of uBO, rather than from just a locally built version.

_Dataset_ is the `requests_top500.json.gz` dataset of URLs released by "whotracks.me" with their [Adblockers Performance Study](https://whotracks.me/blog/adblockers_performance_study.html).

It is recommended to download the dataset, decompress it, and use a local URL to refer to the resource so as to not abuse the bandwidth of the remote server. In Chromium-based browser, you can use a `file:///`-based URL to the local copy. On Firefox you will have to [create a simple HTTP server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/set_up_a_local_testing_server#Running_a_simple_local_HTTP_server) and create a URL such as `http://localhost:8000/[...]` to the local copy.

_Benchmark_ is one of the internal uBO benchmarks:
- [`µBlock.staticNetFilteringEngine.benchmark();`](https://github.com/gorhill/uBlock/commit/5733439f629da948cfc3cae74afa519f6cff7b7f) (initial implementation, recording of the matches was added [later](https://github.com/gorhill/uBlock/commit/92c5f17b78e5056340f462b049c1871ae0467220) for comparison/debugging purposes)
- [`µBlock.sessionFirewall.benchmark();`](https://github.com/gorhill/uBlock/commit/928ab91ab8b72be1c962370b49a36fbe1e1ded94)
- [`µBlock.cosmeticFilteringEngine.benchmark();`](https://github.com/gorhill/uBlock/commit/1e40f50eb3c1347afea251dce603f432e2199606)

Benchmarks can be executed from Browser Console in extension background context. 

~[`consoleLogLevel`](./Advanced-settings#consoleloglevel) must be set to `info` to actually print the results.~ Fixed in [1.25.1b7](https://github.com/gorhill/uBlock/commit/da71c3a499fc26acc34bb58b67b0de4494ddffcd)

***

#### `blockingProfiles`

Default: `11111/#F00 11010/#C0F 11001/#00F 00001`

Before [1.31.3b13](https://github.com/gorhill/uBlock/commit/b779f1f7c9deea32970b93e11a8d33ef7efe5db8): `11111/#F00 11011/#C0F 11001/#00F 00001` (reload action bit for 3p is set)

Before [1.22.0](https://github.com/gorhill/uBlock/compare/5e1f4d7...07c950f): `11101 11001 00001`

Introduced in [1.21.0](https://github.com/gorhill/uBlock/commit/693687fd74fe9a4645f0c9c1e6dbedb56b5fb5d7), improved after 1.22.0 to reflect blocking mode in the color of uBlock₀ icon badge.  
[1.31.3b13](https://github.com/gorhill/uBlock/commit/b779f1f7c9deea32970b93e11a8d33ef7efe5db8) will attempt to automatically reload CSS styles without reloading whole page when 3p blocking is relaxed.

Preference allows to configure cascade of the "Relax blocking mode" [keyboard shortcut](./Keyboard-shortcuts), along with corresponding badge color.

Default value contains four codes separated by space representing four [blocking modes](https://github.com/uBlockOrigin/uBlock-issues/wiki/Blocking-mode):

| [Hard mode](https://github.com/uBlockOrigin/uBlock-issues/wiki/Blocking-mode:-hard-mode) +<br>[No scripting](https://github.com/uBlockOrigin/uBlock-issues/wiki/Per-site-switches#no-scripting) | [Medium mode](https://github.com/uBlockOrigin/uBlock-issues/wiki/Blocking-mode:-medium-mode) +<br>[No scripting](https://github.com/uBlockOrigin/uBlock-issues/wiki/Per-site-switches#no-scripting) | [Medium mode](https://github.com/uBlockOrigin/uBlock-issues/wiki/Blocking-mode:-medium-mode) | [Default](https://github.com/uBlockOrigin/uBlock-issues/wiki/Blocking-mode:-easy-mode) |
| ---                      | ---                        | ---         | ---     |
| 11111/#F00               | 11011/#C0F                 | 11001/#00F  | 00001   |
|![red badge](https://user-images.githubusercontent.com/886325/64036700-1c0fce00-cb54-11e9-9fad-49f72c4fa086.png)|![purple badge](https://user-images.githubusercontent.com/886325/64036667-039fb380-cb54-11e9-8199-cf042837d481.png)|![blue badge](https://user-images.githubusercontent.com/886325/64036718-229e4580-cb54-11e9-91d3-10b6d95b6068.png)|![black badge](https://user-images.githubusercontent.com/886325/64035689-b7ec0a80-cb51-11e9-82d2-851edceae27e.png)|

Each code consist of bit field indicating status of the feature ( 1 for blocked/enabled, 0 for not blocked/disabled ) and optional separator `/` followed by CSS color value<sup>**\[1]**<sup>.

| 3p-frame | 3p-script | 3p     | no-scripting | reload action | separator | CSS color value<sup>**\[1]**</sup> |
| ---      | ---       | ---    | ---          | ---           | ---       | ---             |

Pressing "Relax blocking mode" will compare current uBO status with `blockingProfiles` codes from left to right and apply if it's different, then reload page if "reload action" is enabled, then apply color to the uBO icon badge.

**\[1]:** [The _color_ CSS data type](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value)

***

#### `cacheControlForFirefox1376932`

Default: `no-cache, no-store, must-revalidate`.

uBO 1.17.0 and above.

Configure how uBO should affect caching main document requests for the purpose of dealing with browser bug (see [#229](https://github.com/uBlockOrigin/uBlock-issues/issues/229)).

Possible values:

- `no-cache, no-store, must-revalidate`:
    - Undesirable side effect: documents themselves for which uBO has to inject CSP directives as a result of filters/ruleset won't be available offline.

- `no-cache`:
    - Undesirable side effect: One will need to explicitly cache-bypass reload a page each time uBO has to inject CSP directives as a result of filters/ruleset. Note that such cache-bypass reload does not affect only the document itself, but also all secondary resources inside that document.

- `unset`:
     - Available after [1.22.0](https://github.com/gorhill/uBlock/commit/52925ba2f9ed4351c0f5c7420773d2f59557fc7d), turns off cache header modifications.

Related Firefox issues:
- test-only patch: <https://bugzilla.mozilla.org/show_bug.cgi?id=1376932>
- which fails permanently and was disabled: <https://bugzilla.mozilla.org/show_bug.cgi?id=1573511>.
- https://bugzilla.mozilla.org/show_bug.cgi?id=1648635

***

#### `cacheStorageAPI`

Default: `unset`.

After [1.18.6](https://github.com/gorhill/uBlock/commit/0d369cda21bbce23a7376e0f7b2847a3c7a6d3d8) works in Firefox.

If set to `browser.storage.local`, uBO will use WebExtensions storage as a backend to cache storage.

Additionally, should `indexedDB` not be available for whatever reason,
uBO will automatically fallback to `browser.storage.local`.

uBO 1.18.2 and above, Chromium only.

If set to `indexedDB`, uBO will use [IndexedDB](https://developer.mozilla.org/en-US/docs/Glossary/IndexedDB) as a backend to the cache storage, potentially increasing performance and reducing memory usage. See [#328](https://github.com/uBlockOrigin/uBlock-issues/issues/328) for details.
Bad side effects - filter lists will be out of date in Chrome incognito mode - [#399](https://github.com/uBlockOrigin/uBlock-issues/issues/399).

If `unset`, uBO will use whatever backend storage which is optimal for the current platform.

***

#### `cacheStorageCompression`

Default: `true`.

uBO 1.16.21 and above.

If set to true, uBO will lz4-compress data before storing it in its cache storage. The cache storage is used for storing downloaded filter lists, compiled filter lists, selfies. This setting work when IndexedDB is used as the cache storage backend (by default with Firefox/Firefox for Android). See [#141](https://github.com/uBlockOrigin/uBlock-issues/issues/141) for related discussion.

***

#### `cloudStorageCompression`

Default: `true`, was `false` before [1.30.9rc2](https://github.com/gorhill/uBlock/commit/eb8433cb1964f9852d03f8ca1aa2cf51bd51a317)

Introduced in [1.29.3b7](https://github.com/gorhill/uBlock/commit/d8b6b31eca117d2d82ab53bb2477117ef36761ab).

Enable data compression before sending the data to cloud storage.

***

#### `cnameIgnore1stParty`

Default: `true`.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/3a564c199260a857f3d78d5f12b8c3f1aa85b865).

Firefox only.

Whether uBO should ignore to re-run a network request through the filtering engine when the CNAME hostname is 1st-party to the alias hostname.

***

#### `cnameIgnoreExceptions`

Default: `true`.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/91e702cebbe52137f59a94f55e46d31f95eb98b9).

Firefox only.

Whether to bypass the uncloaking of network requests which were excepted by filters/rules.

This is necessary so as to avoid undue breakage by having exception filters being rendered useless as a result of CNAME-uncloaking.

For example, `google-analytics.com` uncloaks to `www-google-analytics.l.google.com` and both hostnames appear in Peter Lowe's list, which means exception filters for `google-analytics.com` (to fix site breakage) would be rendered useless as the uncloaking would cause the network request to be ultimately blocked.

***

#### `cnameIgnoreList`

Default: `unset`.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/3a564c199260a857f3d78d5f12b8c3f1aa85b865).

Firefox only.

Possible values:

- Space-separated list of hostnames.
- `*` - all hostnames.

This tells uBO to NOT re-run the network request through uBO's filtering engine with the CNAME hostname.

This is useful to exclude commonly used actual hostnames from being re-run through uBO's filtering engine, so as to avoid pointless overhead.

***

#### `cnameIgnoreRootDocument`

Default: `true`.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/a16e4161de5b33856312226e71b05c6eef8bf83a).

Firefox only.

Tells uBO to skip CNAME-lookup for root document.

***

#### `cnameMaxTTL`

Default: `120` minutes.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/3a564c199260a857f3d78d5f12b8c3f1aa85b865).

Firefox only.

This tells uBO to clear its CNAME cache after the specified time.

For efficiency purpose, uBO will cache alias=>CNAME associations for reuse so as to reduce calls to `browser.dns.resolve`. All the associations will be cleared after the specified time to ensure the map does not grow too large and too ensure uBO uses up to date CNAME information.

***

#### `cnameReplayFullURL`

Default: `false`.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/a16e4161de5b33856312226e71b05c6eef8bf83a).

Firefox only.

Tells uBO whether after CNAME-uncloaking replay through the filtering engine the whole URL or just the origin part of it.

Replaying only the origin part is meant to lower undue breakage and improve performance by avoiding repeating the pattern-matching of the whole URL -- which pattern-matching was most likely already accomplished with the original request.

***

#### `cnameUncloak`

[Removed in 1.34.0](https://github.com/gorhill/uBlock/commit/1c3b45f75d0f84d68abb51b15bbdc043464ee3e0), deprecated in favor of [_"Uncloak canonical names"_](./Dashboard:-Settings#uncloak-canonical-names) preference in Dashboard/Settings pane.

Introduced in [1.25.0](https://github.com/gorhill/uBlock/commit/91e702cebbe52137f59a94f55e46d31f95eb98b9).

Firefox only.

Whether to enable CNAME-uncloaking feature.

***

#### `cnameUncloakProxied`

Default: `false`.

Introduced in [1.26.0](https://github.com/gorhill/uBlock/commit/3f7ece94691f048377512990a38c0317820bf77f).

Firefox only.

By default (set to `false`) uBO will no longer cname-uncloak when it detects that network requests are being proxied.

This default behavior can be overridden by setting this option to `true`.

This new advanced setting may disappear once the following Firefox issue is fixed: https://bugzilla.mozilla.org/show_bug.cgi?id=1618271

***

#### `consoleLogLevel`

Default: `unset`.

uBO 1.18.5b1 and above

For development purposes only. 

If set to `info`, prints debug messages to the browser console.

***

#### `debugScriptlets`
#### `debugScriptletInjector`

Default: `false`.

If set to `true`, [`debugger;` statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger) will be inserted just before [scriptlet](./Static-filter-syntax#scriptlet-injection) or scriptlet injector code.

***

#### `disableWebAssembly`

Default: `false`.

uBO 1.17.3rc4 and above.

For development purposes only.

If set to `true`, turns off [_WebAssembly_](https://developer.mozilla.org/en-US/docs/WebAssembly/Concepts) optimizations in uBO code.

***

#### `extensionUpdateForceReload`

Default: `false`.

uBO [1.23.0](https://github.com/gorhill/uBlock/commit/93f438f55ebd8d1f558f2e73b64b3f87e928bf02) and above.

If set to `true`, restores update behavior from before [1.22.3b ("Prevent uBO from being reloaded mid-session ")](https://github.com/gorhill/uBlock/commit/59bdf2b4ccd1151a296af36e5536ed00eeb07fb4), extension will unconditionally reload when an update is available; otherwise the extension will reload only when being explicitly disabled then enabled, or when the browser is restarted.

***

#### `filterAuthorMode`

Under development! Do not create related issues!

Default: `false`.

uBO [1.23.0](https://github.com/gorhill/uBlock/commit/59c9a34d34a737f6bb48c4130c65f4fe0fa73806) and above.

Enable point-and-click feature, to create temporary exception filters for static extended filters (i.e. cosmetic, scriptlet & html filters) from within the summary pane in the logger. The button to toggle on/off temporary exception filter is labeled `#@#`:

![filtering tools dialog](https://user-images.githubusercontent.com/886325/69076705-4fb41300-0a34-11ea-8e9a-463b9a1d29d8.png)

The created exceptions are temporary and will be lost when restarting uBO, or manually toggling off the exception filters.

After [1.28.0](https://github.com/gorhill/uBlock/commit/162e53727099ccb0a088cc1399915fb23d9b4fec) restores ability to set _allow_ rules from popup panel. The ability to point-and-click to create _allow_ rules from the popup panel is no longer allowed by default. See [commit message](https://github.com/gorhill/uBlock/commit/162e53727099ccb0a088cc1399915fb23d9b4fec) for reasoning. Tap twice on <kbd>Ctrl</kbd> if you want to access allow rules only temporarily.

***

#### `ignoreRedirectFilters`

Removed in [1.35](https://github.com/gorhill/uBlock/commit/f5b453fae3c77363367cdf9494e90fe276042a72). Can be disabled by filter exception.

***

#### `ignoreScriptInjectFilters`

Removed in [1.35](https://github.com/gorhill/uBlock/commit/bc8c1d00ad728e854b3caf35231d808515058d3f). Can be disabled by filter exception.

***

#### `loggerPopupType`

Default: `popup`.

uBO [1.23.0](https://github.com/gorhill/uBlock/commit/bcf5ac1feec0019663a3ad564caeb1c67679791e) and above.

Control the type of window to be used when the logger is launched as a separate window. Introduced to solve issues with missing/disabled titlebar buttons, resizing, incorrect drawing ([#663](https://github.com/uBlockOrigin/uBlock-issues/issues/663)).

Possible values:

- `popup` - browser window without toolbars (default)
- `normal` - normal browser window with all toolbars and buttons
- any other value defined in [Chromium](https://developer.chrome.com/extensions/windows#type-CreateType) or [Firefox](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/windows/CreateType#Type) documentation.

***

#### `manualUpdateAssetFetchPeriod`

Default: `500` milliseconds.

When clicking the _"Update now"_ button in the _"3rd-party filters"_ pane in the dashboard, this is the number of milliseconds to wait before fetching the next asset which needs to be updated. The delay helps spread the load incurred as a result of loading/processing new filter lists, and its purpose is also to be considerate to remote servers by not subjecting them to rapid-fire requests.

***

#### `modifyWebextFlavor`

Default: `unset`.

Introduced in [1.38.7b3](https://github.com/gorhill/uBlock/commit/f49c4e254b7137e40516cecced58c76d05f23672).

Value: A list of space-separated tokens to be added/removed from the [computed default](https://github.com/gorhill/uBlock/blob/18ae79cdf25be59831c295ea7c90afbcd5a70ce8/platform/common/vapi-common.js#L52-L90) webext flavor.

The primary purpose is to give filter list authors the ability to test mobile flavor on desktop computers. Though mobile versions of web pages can be emulated using browser dev tools, it's not possible to do so for uBO itself.

By using `+mobile` as a value for this setting will force uBO to act as if it's being executed on a mobile device. 

Important: this setting is best used in a dedicated browser profile, as this affects how filter lists are compiled. So best to set it in a new browser profile, then force all filter lists to be recompiled, and use the profile in the future when there is a need to test the specific webext flavor.

***

#### `popupFontSize`

Default: `unset`.

A valid CSS font size value (`14px`) to use for the popup panel. Use if you are unhappy with the default size.

***

#### `popupPanelHeightMode`

Default: `0`.

uBO [1.28.0](https://github.com/gorhill/uBlock/commit/5f4e6d80e0a36e180db3b4e906412bf9a730fdbf) and above.

Set to `1` to force the height of the firewall pane to be no more than the height of the basic pane.

Solves clipping of the Overview Panel - [#785 (comment)](https://github.com/uBlockOrigin/uBlock-issues/issues/785#issuecomment-622327450).

***

#### `requestJournalProcessPeriod`

Default: `1000` milliseconds.

uBO 1.16.21b2 and above.

Controls the delay before uBO internally process it's network request journal queue. The network request journal queue exists for the purpose of fixing [issue 2053](https://github.com/gorhill/uBlock/issues/2053).

As a benign side effect to the fix, there is a delay in displaying the number of blocked requests on extension icon (see [#155](https://github.com/uBlockOrigin/uBlock-issues/issues/155)).

A lower delay than the default one could bring back the issue it's meant to fix.

***

#### `selfieAfter`

Default: `3` minutes.

uBO [1.18.6](https://github.com/gorhill/uBlock/commit/ed7e34fb07f956229b2290608e4500b35f431afe) and above. Used to be `11` minutes until [1.20.0](https://github.com/gorhill/uBlock/commit/3cf71835c4fc9c262d93a645a3af70946539bd19).

Number of minutes after which _selfie_ (optimized, internal representation of filters) is created.

***

#### `strictBlockingBypassDuration`

Default: `120` seconds.

uBO 1.17.3b4 and above.

Controls duration of the [Strict blocking](./Strict-blocking) "Temporarily" bypass.

***

#### `suspendTabsUntilReady`
<span name="suspendtabsuntilready-experimental"></span>

Removed in favor of [_"Suspend network activity until all filter lists are loaded"_](./Dashboard%3A-Filter-lists#suspend-network-activity-until-all-filter-lists-are-loaded) checkbox in Dashboard -> Filter lists in [1.40.3b1](https://github.com/gorhill/uBlock/commit/925c8d5d0c37dbc1f82e57a92e74350de2c5eab1).

Default: `unset`.

Possible values:

- `unset` - leave it to the platform to pick the optimal behavior
- `no` - do not suspend tab loading at launch time
- `yes` - suspend tab loading at launch time

If enabled, uBO will hard block all network requests when the browser launches until _all_ the filter lists and rules are loaded and ready, at which time uBO will force a reload of the tabs for which there were network requests blocked during the setup phase.

Disclaimer: In Chromium based browsers, even with this setting enabled, it's impossible for uBO to guarantee with 100% certainty that everything will be properly blocked when the browser is launched. **This is a by-design browser issue** -- do _not_ open an issue on uBO issue tracker about this.

Related browser issues:
- Chromium: <https://bugs.chromium.org/p/chromium/issues/detail?id=523634>
- Firefox: <https://bugzilla.mozilla.org/show_bug.cgi?id=1378459>, fixed by <https://bugzilla.mozilla.org/show_bug.cgi?id=1447551>.

History:
- [1.40.4](https://github.com/gorhill/uBlock/commit/84bd5c1c0ce4cf6f6270231d826851d3d8a490da) released for Chrome with temporary fix allowing to disable tab reloading by setting `suspendTabsUntilReady` to `no` and with `yes` case actually blocking connections.
- Moved to Dashboard in [1.40.3b1](https://github.com/gorhill/uBlock/commit/925c8d5d0c37dbc1f82e57a92e74350de2c5eab1) development builds.
- Broken in Chromium between [1.27.0](https://github.com/gorhill/uBlock/commit/80b758e18dbd6e5ed06975c2d4f30649a62b17a9) and [1.40.3b0](https://github.com/gorhill/uBlock/commit/869c06d4eec4847d4bf82c0453690dd17829d680) - suspending cannot be enabled.
- Do not block connections on startup, but reload active tabs when uBO is ready in Chromium as the default behavior in [1.39.3rc0](https://github.com/gorhill/uBlock/commit/a0a9497b4aca86727b314d8fc31ad345dad08ac8) (workaround for increasing number of reports about ads slipping through).
- After [1.18.6](https://github.com/gorhill/uBlock/commit/87feb47b51202cb8464eab91597b706965a224f3), configurable again in Firefox (can be disabled). In Firefox this feature is always active by default from now on thanks to ["persistent startup listeners"](https://bugzilla.mozilla.org/show_bug.cgi?id=1503721).
- Before [1.18.6](https://github.com/gorhill/uBlock/commit/87feb47b51202cb8464eab91597b706965a224f3), default to `false`.
- Between uBO [1.18.0](https://github.com/gorhill/uBlock/commit/41548be6be35fe17dbb996e605c4befb09e16911) and 1.18.6, Chromium only.

***

#### `uiFlavor`

Default: `unset`.

uBO [1.25.0](https://github.com/gorhill/uBlock/commit/2b0316440e86d1d8f4ae21f8d9ff4c19ac17216f) and above.

Possible values:

- `fenix` - to forcefully enable new, mobile-friendly, Popup UI layout.
- `classic` - to revert back to old Popup UI (it was `-` up to [1.27.0](https://github.com/gorhill/uBlock/commit/b295d4a0d0d25848211c43cc2e7068859c2cb9ea#diff-0d94ddccc559e1231fe0cfa793814429L359-R377)).
- `unset` - uBO will use whatever UI flavor which is optimal for the current platform.

![Mobile Popup UI layout](https://user-images.githubusercontent.com/585534/74933925-1c767c80-53b3-11ea-96fd-79cedd5533cb.png)

***

#### `uiPopupConfig`

Default: `unset`, was `undocumented` before [1.39.2](https://github.com/gorhill/uBlock/commit/395a4e36a939907982d3768c2d9eabb8aca8cbd1).

Introduced in [1.27.0](https://github.com/gorhill/uBlock/commit/db9c32185538c0943cb3f52a037bd11f6f60cbf9).

Override uBO popup interface configuration.

The value can be one or more space-separated tokens:

- `+captions`/`-captions`: enable/disable captions
- `+no-popups`/`-no-popups`: enable/disable no-popups switch
- `+logger`/`-logger`: new in [1.39.1b1](https://github.com/gorhill/uBlock/commit/1408422cbaa8d1efc0832b6cf09595fcc20369d7), enable/disable the logger button

***

#### `uiStyles`

Default: `unset`.

uBO [1.28.0](https://github.com/gorhill/uBlock/commit/9f7e5b621dc5e7a3e0fed0daa57d922f1ec56d80) and above.

Allow to bypass uBO's default CSS styles in case they are causing issues to specific users. It is the responsibility of the user to ensure the value of `uiStyles` contains valid CSS property declarations. uBO will assign the value to `document.body.style.cssText`.

For example, in the case of the [issue #1044](https://github.com/uBlockOrigin/uBlock-issues/issues/1044), one could set `uiStyles` to `font-family: sans-serif` to force uBO to the system font for its user interface. Another example is [issue #1254](https://github.com/uBlockOrigin/uBlock-issues/issues/1254) where in [uBO v1.30.0](https://github.com/gorhill/uBlock/commit/1cdffea6186af8965d722575ed8fa74b0a6e193c) will be possible to adjust width of popup panels.

***

#### `uiTheme`

Default: `unset`.

uBO [1.30.1b3](https://github.com/gorhill/uBlock/commit/e3a6d8465f19f4ef5d84ceddb9570644cf4fc0a3) and above.

For development purposes only! DO NOT create issues about this feature!  
Locked to dev build only in [1.31.3b5](https://github.com/gorhill/uBlock/commit/9aef41738b66b25028403d8e0f25f7fb4deafb0e).

Allows to manually override dark mode theme status.

Possible values:

- `unset`: depending on uBO version - force light theme or uBO will pick the theme according to browser's `prefers-color-scheme`
- `light`: force light theme
- `dark`: force dark theme

***

#### `updateAssetBypassBrowserCache`

Default: `false` 

With [1.22.0](https://github.com/gorhill/uBlock/commit/048bfd251c9b8eeafce020b4f894d736044d6a6f) and above.

If set to `true`, uBO will ensure the browser cache is bypassed when manually<sup>[1.27.0](https://github.com/gorhill/uBlock/commit/4687c60bf9cec5b68e5a007d740af93f4119a79e)</sup> fetching a remote resource more often than every hour.

This is for the convenience of filter list maintainers who may want to test the latest version of their lists when fetched from their remote location.

***

#### `userResourcesLocation` 

Default: `unset`.

One or more space-separated URLs which content will be parsed as token-identified resources to be used for [`redirect`](./Static-filter-syntax#redirect) or [scriptlet-injection](./Static-filter-syntax#scriptlet-injection) (`+js(...)`) purpose.

uBO expects valid content such as can be seen in [scriptlets.js](https://github.com/gorhill/uBlock/blob/master/assets/resources/scriptlets.js), anything else will lead to undefined results.

Any duplicate as per token will result in the previous resource being replaced by the latter one. The resource files are loaded in order of URL appearance, and uBO stock resource file is always loaded first.

Additional resources will be updated at the same time the built-in resource file is updated. Purging the cache of 'uBlock filters' will also purge the cache of the built-in resource file -- and hence force a reload of user-specified resources if any.

The setting was introduced in [1.12.0](https://github.com/gorhill/uBlock/releases/tag/1.12.0). Support for multiple URLs was introduced in [1.19.0](https://github.com/gorhill/uBlock/releases/tag/1.19.0).
