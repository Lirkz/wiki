Motivation for creating this page, this comment made in the spirit of _Fake News_ (with no supporting objective evidence, merely just a _"trust me"_ statement):

> Ublock is inferior in capabilities [to Adblock Plus (ABP)] as a result of being lighter on the browser [[source](https://forums.mozillazine.org/viewtopic.php?p=14743232#p14743232)]

There is nothing wrong with preferring ABP to uBlock Origin (uBO). There is, however, something wrong when someone engages in misinformation regarding uBO because of their preference for ABP.

Here is my reference answer to such claims.

uBO is lighter on the browser because of the many choices made regarding the internal design of the filtering engine. A coarse enumeration of these choices is:
- lean in-memory filter representation
- plain string comparisons instead of regular expressions wherever possible
    - a majority of network filters can reduce to basic string comparison, and is what uBO does internally for these filters, whereas ABP converts _all_ network filters into regular expressions.
    - Example, `&ad_zones=` (filter found in EasyList).
        - ABP's code conceptually is: `/&ad_zones=/.test(url)` -- the whole URL must be scanned
        - uBO's code conceptually is: `url.startsWith('&ad_zones=', i)` -- no scanning of the URL
- does not unconditionally inject 18,000+ (that is with EasyList only) generic CSS rules in all pages/frames<br><sup>meaning no undue [memory usage issues](https://bugzilla.mozilla.org/show_bug.cgi?id=1320872)</sup>

Do these design choices cause uBO to be _"inferior in capabilities"_ compared to ABP? See the capabilities comparison grid below for an answer (at the time of writing):

Features |  ABP  |  uBO
-------- | :---: | :---:
**network filtering**
[multi-stage filtering engine](./Overview-of-uBlock's-network-filtering-engine)<br><sup>ability for users to easily override filters in 3rd-party filter lists on a per-site basis</sup> |     | yes
`@@...$document` | yes | [no](./Static-filter-syntax#not-supported)
can read hosts files |     | yes
CNAME uncloaking |    | [yes](./Static-filter-syntax#cname)
`denyallow` |    | [yes](./Static-filter-syntax#denyallow)
`domain` with entity-matching |    | [yes](./Static-filter-syntax#domain)
`inline-script`<br><sup>to prevent execution of inline javascript</sup> | [no](https://issues.adblockplus.org/ticket/748/) | [yes](./Static-filter-syntax#inline-script)
`important`<br><sup>to be able to override exception filters</sup> |     | [yes](./Static-filter-syntax#important)
`popunder` | [no](https://issues.adblockplus.org/ticket/2095/) | yes
`redirect`<br><sup>to redirect to local resources, key to privacy and to counter anti-blockers</sup> |     | yes
`csp=`<br><sup>see [rationale](https://github.com/gorhill/uBlock/issues/1930#issuecomment-301055346)</sup> |     | yes
`badfilter`<br><sup>to disable an existing filter</sup> |     | yes
[strict blocking](./Strict-blocking) |     | yes
rule-based filtering<br><sup>firewall-like or URL-based rules with corresponding point-and-click UI</sup> |     | yes
behind-the-scene<br><sup>uBO's logger reports behind-the-scene request, filtering is opt-in</sup> |     | [yes](./Behind-the-scene-network-requests)
**cosmetic filtering**
entity-based filters |     | [yes](./Static-filter-syntax#entity-based-cosmetic-filters)
`-abp-properties` | yes | [no](https://github.com/gorhill/uBlock/issues/139)
`:has` | ~~[not yet](https://issues.adblockplus.org/ticket/2360/)~~ yes (`:-abp-has`) | yes
`:has-text` | [yes](https://issues.adblockplus.org/ticket/5249/) (`-abp-contains`) | yes
`:if` `:if-not`<br>`:matches-css` `:matches-css-before` `:matches-css-after`<br>`:xpath` |     | yes
`:remove` |    | yes
`:style` | [no](https://issues.adblockplus.org/ticket/756/) | yes
`:upward` |    | yes
**Scriptlet filtering**
`+js(...)`<br>Ability to inject scriptlets in page content<br><sup>key to counter anti-blockers</sup> |     | [yes](./Static-filter-syntax#scriptlet-injection)
**HTML filtering**
Ability to modify response data on the fly<br><sup>WebExtensions uBO 1.15+</sup> |     | [yes](./Static-filter-syntax#html-filters)
**privacy**
pro-user default settings<br><sup>uBO is not monetized, it's under no pressure to [compromise](https://forum.adblockplus.org/viewtopic.php?f=17&t=50215) on pro-user interests</sup> |     | yes
disable pre-fetching |     | [yes](./Dashboard:-Settings#disable-pre-fetching)
disable hyperlink auditing |     | [yes](./Dashboard:-Settings#disable-hyperlink-auditing)
disable local IP addresses leakage through WebRTC |     | [yes](./Dashboard:-Settings#prevent-webrtc-from-leaking-local-ip-address)
block CSP reports |     | [yes](./Dashboard:-Settings#block-csp-reports)
**other features**
pre-compilation of filter lists for fast loading of filters |     | [yes](./Launch-and-filter-lists-load-performance)
"acceptable ads" | yes | [no](https://github.com/gorhill/uBlock/blob/master/MANIFESTO.md)
disable everywhere | yes |
count filter hits | yes, [disabled by default](https://issues.adblockplus.org/ticket/5298/) | [no](https://github.com/gorhill/uBlock/issues/1353)
ability to globally ignore generic cosmetic filters<br><sup>useful for low-performance mobile devices</sup> |     | yes
cloud storage | Firefox only | yes
point-and-click firewall-like filtering<br><sup>allows for [relax](./Blocking-mode:-medium-mode) or [strict](./Blocking-mode:-hard-mode) default-deny approach</up> |     | yes
logger | per-page | [unified](./The-logger)
point-and-click per-site no-popups |     | [yes](./Per-site-switches#no-popups)
point-and-click per site no-cosmetic-filtering |     | [yes](./Per-site-switches#no-cosmetic-filtering)
point-and-click per site no-large-media-elements |     | [yes](./Per-site-switches#no-large-media-elements)
point-and-click per site no-remote-fonts |     | [yes](./Per-site-switches#no-remote-fonts)
integrated element picker | Chromium-based browsers only | [yes](./Element-picker)
element zapper | | [yes](./Element-zapper)
easy backup/restore of all settings | Firefox only | yes
