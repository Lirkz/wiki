[Back to "Quick guide: popup user interface"](./Quick-guide:-popup-user-interface)

***

The per-site switches allow you to control uBlock Origin (uBO)'s behavior on a per-site basis.

![Popup UI](https://user-images.githubusercontent.com/95879668/172274761-4a2c1018-e6c8-4d79-baab-4d6901b8f211.png)

Changes to the state of per-site switches are temporary until you make them permanent by clicking the padlock icon. Pressing <kbd>Ctrl</kbd> (<kbd>Cmd</kbd> on Mac) when toggling switches will make them permanent immediately.

![eraser and padlock](https://user-images.githubusercontent.com/95879668/172276144-f3be783c-b0c1-45d2-b926-88d793e3fde4.png)
<br><sup>Eraser and padlock icons</sup>

***

- [No popups](#no-popups)
- [No large media elements](#no-large-media-elements)
- [No cosmetic filtering](#no-cosmetic-filtering)
- [No remote fonts](#no-remote-fonts)
- [No scripting](#no-scripting)

***

## No popups

By default, popups are allowed unless there is a filter to block them. When this setting is enabled, **all** popups will be unconditionally blocked for the current site, regardless of filters:

![Popup UI](https://user-images.githubusercontent.com/95879668/172276698-64e59e13-031f-4f10-9aa1-3d4594f284a3.png)<br><sup>The badge shows the number of popups that have been closed on the page.</sup>

No popups rules appear as `no-popups: [hostname] true` entries in the [_My rules_ pane](./Dashboard:-My-rules).

Blocking popups depends on whether the proper filters are present in the selected filter lists, so this feature is most useful when a site creates popups for which there are no filters to take care of them in 3rd-party filter lists.

**Caveat:** It's not _always_ possible for uBO to determine for sure whether a new tab being opened is that of a popup, or is the result of a legitimate click on a link by the user. So if the no-popups switch is in use, you _may_ not be able to open a link in a new tab through the context menu.

***

## No large media elements

The second icon is to toggle on/off the blocking of large media elements for the current site. The primary purpose of this feature is to save bandwidth. A side effect is to possibly speed up the page load.

![Popup UI](https://user-images.githubusercontent.com/95879668/172277040-a027a86f-3927-427d-a388-b58714338e1f.png)<br><sup>The badge shows the number of large media elements that have been blocked on the page.</sup>

By default, this setting is disabled. The global default can be enabled in the [_Settings_ pane](./Dashboard:-Settings) in the [dashboard](./Dashboard).

![a](https://user-images.githubusercontent.com/95879668/172279019-fcade32f-5fc0-4d00-8a51-e62820e0f437.png)

The threshold size -- a global setting -- to decide when to block or not is also configurable. The threshold size can be set to zero: this will cause all media elements to be blocked. For the sake of documentation, let's refer to media elements (images, videos, audios) that are larger than the set size as _"large media elements"_.

You can enable/disable on a per-site basis, there is a switch in the popup panel to toggle for the current site.

When large media elements have been blocked on a page, you may force a reload of these elements interactively: if you hover over the placeholder of a blocked image and the cursor changes into a magnifier, this means that clicking on a blocked image will force a reload of that image.

If you use this feature and large media elements were blocked on a web page, the context menu will contain a new entry: _"Temporarily allow large media elements"_. When you click this entry, uBO will disable temporarily the blocking of large media elements for the site, and attempt to load the blocked media elements without reloading the page. In some cases, you may need to force a reload of the page, for example, if large media elements were fetched programmatically by the page. The temporary disabling will be removed for a tab as soon as you travel to a new site, or close the tab.

Blocked large media elements are reported in the logger with the filter `no-large-media: [scope] true`.

Note that this feature has no privacy value: a connection to the remote server must be performed in order to fetch the size of the resource. This of course applies only to resources that were not otherwise blocked by uBO's filtering engine.

Examples of usefulness (let's say you just stumbled onto these pages not knowing whether the article would really interest you), bandwidth consumed:

- <https://www.wired.com/2016/01/drones-arent-just-toys-anymore/>
    - Not blocking large media elements: 5.5 MB.
    - Blocking media elements larger than 1 MB: 2.1 MB.
    - Blocking media elements larger than 50 kB: 1.2 MB.
- <https://www.tomshardware.com/reviews/samsung-gear-vr-headset,4405.html>
    - Not blocking large media elements: 15.1 MB.
    - Blocking media elements larger than 1 MB: 15.1 MB.
    - Blocking media elements larger than 50 kB: 61 kB.
- <https://twitter.com/> (your Twitter stream):
    - Not loading largish images by default can help Twitter page performance: click on a placeholder to load only the images which seem to be of interest to you.
    - This is true for any "infinite scrolling" web pages ([another example](https://www.bloomberg.com/news/articles/2016-01-19/being-illegal-won-t-keep-drones-from-taking-over-india)). Not loading the images by default help a lot in such cases.

#### Caveat:

If the media elements do not have a `Content-Length` header present, then this switch will fail to block the said media elements by size.

***

## No cosmetic filtering

["Cosmetic filtering" in uBO](./Does-uBlock-Origin-block-ads-or-just-hide-them%3F#cosmetic-filters) is what is known as "element hiding" in Adblock Plus (ABP). The purpose of these filters is to hide the content of the page that cannot be blocked by network filters.

You can easily toggle on/off cosmetic filtering for a given site:

![Popup UI](https://user-images.githubusercontent.com/95879668/172279368-c7dbc860-575a-44eb-af38-ed4edb93ad0f.png)<br><sup>The badge shows the number of DOM elements that have been hidden on the page.</sup>

When present, the badge number indicates the number of elements hidden on the page by uBO as a result of cosmetic filtering. If you disable cosmetic filtering while there are hidden elements on the page, these elements will become visible/hidden as you toggle off/on cosmetic filtering.

A good example of cosmetic filtering in action is the ads showing up with the results of a Google Search page ([example](https://www.google.com/search?q=buy+car)).

Cosmetic filtering is always enabled by default.

> ***
> **Tips**
>
> It is often suggested adding a custom static filter such as `@@||example.com^$elemhide` or `@@||example.com^$generichide` to prevent "adblock" detection by specific sites ([example](https://forum.adblockplus.org/viewtopic.php?f=2&t=30763#p124225), [example](https://forum.adblockplus.org/viewtopic.php?f=2&t=43961)). You can accomplish the same goal more simply by just toggling off cosmetic filtering using this switch while on the problematic site.
> 
> This switch can help uBO to further lower its CPU-cycle footprint, which might be beneficial on devices with limited CPU-cycle resources -- and thus helping extend battery life and speed up page load times. The idea is to disable cosmetic filtering everywhere by default and to enable it only for those sites which really benefit from it.
> ***

To disable cosmetic filtering everywhere by default, go to the [_Settings_ pane](./Dashboard:-Settings) in the [dashboard](./Dashboard), and check the option _"Disable cosmetic filtering"_ under the _"Default behavior"_ header:

![Disable cosmetic filtering everywhere by default](https://user-images.githubusercontent.com/95879668/172282204-f28a6464-9f4e-4c73-a2e9-c77b6dfc3664.png)

From then on, cosmetic filtering will be turned off everywhere by default, and to turn it on for a specific site where it is really needed, just enable it using the switch in uBO's popup panel.

***

## No remote fonts

You can prevent web fonts from being downloaded for the current site:

![Popup UI](https://user-images.githubusercontent.com/95879668/172282836-b3033c8c-de57-4138-a017-814d7f137c3a.png)<br><sup>The badge shows the number of font resources that have been seen on the page.</sup>

Because of security and privacy concerns, many prefer to block all web fonts by default -- toggle the appropriate default behavior in the [_Settings_ pane](./Dashboard:-Settings) in the [dashboard](./Dashboard):

![Block remote fonts everywhere by default](https://user-images.githubusercontent.com/95879668/172284772-509aac36-e09c-4eec-8c05-8a6bce778f4e.png)

This will block all web fonts everywhere by default, and in this case, you can toggle off the switch to allow web fonts on a per-site basis.

Keep in mind, though, that this rule blocks **all** first-party and third-party fonts. As a lighter alternative, you can also choose to allow first-party fonts and block _only_ third-party fonts by adding the filter 

`*$font,third-party`

to the _"My filters"_ pane. If you want to allow third-party fonts for some specific sites you can add them by modifying the above filter:

`*$font,third-party,domain=~example.com|~other.example.net|~different.example.org`

***

## No scripting

New in [1.17.0](https://github.com/gorhill/uBlock/commit/3c85c0319462ca331d53c350fba4bc6c1b2ef96f)

Wholly disable JavaScript for a given site.

![Popup UI](https://user-images.githubusercontent.com/95879668/172292344-054389c0-2469-48f8-97b8-870b3a51f961.png)
<br>The badge shows the approximate number of script resources that have
been seen on the page (the number is limited to 99 because of layout constraints)

![purple badge](https://user-images.githubusercontent.com/95879668/172287593-4e3f0a92-553f-43c0-90a2-ed83cd084d00.png)
<br>Starting with [v1.21.7b5](https://github.com/gorhill/uBlock/commit/7ff750eaf6007bdea4e843d3314fc7275b1ce945), a purple badge on uBO toolbar button indicates activation of the "No scripting" switch.

This master switch has blocking precedence over dynamic filtering rules and static filters related to script resources.

Furthermore, when JavaScript is disabled through this master switch, [`noscript`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/noscript#Example) tags will be honored on a page (as opposed to when just using filters/rules to block script resources).

As with some other per-site switches, the default state of the per-site JavaScript master switch can be set in the [_Settings_ pane](./Dashboard:-Settings), thus allowing to disable JavaScript everywhere by default, and enable on a per-site basis:

![a](https://user-images.githubusercontent.com/95879668/172288712-6b744cfd-ca36-4ae7-9c6d-72a841a62ce2.png)

JavaScript master switch rules appear as `no-scripting: [hostname] true` entries in the [_My rules_ pane](./Dashboard:-My-rules).

The JavaScript master switch can be disabled through the "Relax blocking mode" [keyboard shortcut](./Keyboard-shortcuts).