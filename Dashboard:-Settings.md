- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)
   - [Cloud storage](./Cloud-storage)
   - [Advanced user features](./Advanced-user-features)
      - [Advanced-settings](./Advanced-settings)

***

![Figure 1](https://user-images.githubusercontent.com/95879668/161320322-51242d45-db55-4884-9cae-2e23c7634dfa.png)

***

## General

### Hide placeholders of blocked elements

Collapse the placeholder space left behind when some elements like an image or a frame get blocked by network filtering.

### Show the number of blocked requests on the icon

Display how many blocked network requests were on the page in the badge of the extensions button.

### Make use of the context menu where appropriate

If checked, this permits uBlock Origin (uBO) to add items in the [browser's context menu](./The-context-menu) to improve convenience.

### Enable cloud storage support

See [Cloud storage](./Cloud-storage) documentation.

***

## Privacy

### Disable prefetching

Checking this will disable prefetching in your browser. When prefetching is enabled, the browser _can_ establish connections to remote servers even if the resources from these remote servers were supposed to be blocked by uBO.

It prevents the browser from bypassing uBO's filtering engine before establishing a connection to remote servers.

Mozilla's [_"Link prefetching FAQ"_](https://developer.mozilla.org/en-US/docs/Web/HTTP/Link_prefetching_FAQ):

> **Privacy implications** Along with the referral and URL-following implications already mentioned above, prefetching will generally cause the cookies of the prefetched site to be accessed.

#### **IMPORTANT NOTE:**
On Chromium 51 and above (including browsers based on Chromium 51 and above), disabling prefetching is unreliable because it does not cause DNS lookups, preconnections and prefetches to be reliably blocked since Chromium allows web pages to override that user setting. For details, see:
- <https://github.com/gorhill/uBlock/issues/3219>
- <https://bugs.chromium.org/p/chromium/issues/detail?id=785125>
- Example of different behavior with Firefox: <https://github.com/uBlockOrigin/uBlock-issues/issues/435>

### Disable hyperlink auditing

Checking this will prevent hyperlink auditing. _Hyperlink auditing_ is best summarized as a "phone home" feature (or even more accurately, "phone anywhere") meant to inform one or more servers of which links you click on (and when). [Here](https://www.wilderssecurity.com/threads/hyperlink-auditing-aka-a-ping-and-beacon-aka-navigator-sendbeacon.364904/) are the well-explained details, and the case of why such a feature is harmful to users is well-argued [here](https://www.wilderssecurity.com/threads/major-browsers-to-prevent-disabling-of-click-tracking-privacy-risk.415381/#post-2822723).

### Prevent WebRTC from leaking local IP address

Option removed from desktop browsers in [uBO v1.38](https://github.com/uBlockOrigin/uBlock-issues/issues/1723).

Browsers now obfuscate LAN addresses by mDNS:

- Firefox: ["Enable mDNS hostname obfuscation"](https://bugzilla.mozilla.org/show_bug.cgi?id=1588817)
- Chromium: ["mDNS service for IP handling in WebRTC"](https://bugs.chromium.org/p/chromium/issues/detail?id=878465)

The option is still available in Firefox for Android because obfuscation is still not implemented. See: ["Support mDNS hostname obfuscation on Android"](https://bugzilla.mozilla.org/show_bug.cgi?id=1581947)

<details>
<summary>Details</summary>

![highlighted Prevent WebRTC from leaking local IP address preference](https://cloud.githubusercontent.com/assets/585534/8344622/0ce20cc4-1ab2-11e5-8f46-a0a387c91d63.png)

Background info: [STUN IP Address requests for WebRTC](https://github.com/diafygi/webrtc-ips)

Test case: [Prevent WebRTC from leaking local IP address](./Prevent-WebRTC-from-leaking-local-IP-address)

Keep in mind that this feature prevents **leakage** of your non-internet-facing IP address. The purpose of this feature is not to hide your current internet-facing IP address. Make sure you do not misinterpret the test results above. For example, if you use a VPN, your internet-facing IP address is that of the VPN, so your ISP-provided IP address should not be visible to the outside world with this setting checked. Your ISP-provided IP address will be visible regardless of this setting if you are not behind a VPN or proxy.

**Caveats:**
- Chromium-based browsers:
   - The feature works only on versions 42 and above.
- Firefox:
   - Due to the different ways in different browsers of handling network connections, before version [1.18.12](https://github.com/gorhill/uBlock/commit/977178bef23c7711a050181be979a4668bfebcfb), WebRTC was disabled if not using a proxy in Firefox. Related issue: [#3009](https://github.com/gorhill/uBlock/issues/3009#issuecomment-329798696)

</details>

### Block CSP reports

In [1.31.3rc1](https://github.com/gorhill/uBlock/commit/bc9b8a13300d7a6de93d0632369be15b05b7646e), blocking CSP reports was enabled in Firefox to mitigate fingerprinting attempts described in [LiCybora/NanoDefenderFirefox#196](https://github.com/LiCybora/NanoDefenderFirefox/issues/196).

You can block network requests made as a result of your browser reporting Content Security Policy violations ("CSP reports") to a remote server (which can be 3rd-party to the site where the violation occurred).

**Important:** disabling CSP reporting is not something that will break web pages. The purpose of CSP reporting is _strictly_ a development tool for websites.

Consider this excerpt from [Reporting API / Privacy Considerations](https://w3c.github.io/reporting/#privacy) (my emphasis):

> 9.4. Disabling Reporting
> 
> [...]
> 
> That said, it can’t be the case that this general benefit be allowed to take priority over the ability of a user to individually opt-out of such a system. Sending reports costs bandwidth, and potentially could reveal some small amount of additional information above and beyond what a website can obtain in-band ([NETWORK-ERROR-LOGGING], for instance). **User agents MUST allow users to disable reporting with some reasonable amount of granularity in order to maintain the priority of constituencies espoused in [HTML-DESIGN-PRINCIPLES].**

There is no easy way to toggle CSP reporting in either Chromium or Firefox. This per-site switch is to address this shortcoming.

The behind-the-scene network requests that are actual CSP reports will get filtered out by this setting. So if you globally disable CSP reporting in uBO, this will also apply to behind-the-scene network requests.

Note that the blocking of CSP reports is implemented as a per-site switch internally in uBO so that an advanced user could create rules in the _My rules_ pane in the dashboard to allow for more granular control of the blocking of CSP reports. For example:

    no-csp-reports: example.com false

The above rule means CSP reports would not be blocked on `example.com` when CSP reports are blocked globally. The reverse will also work:

    no-csp-reports: example.com true

The above rule means CSP reports would be blocked on `example.com` when CSP reports are not blocked globally.

### Uncloak canonical names

![higlighted Uncloak canonical names preference](https://user-images.githubusercontent.com/95879668/172086299-2feb30ec-4abd-4be3-bb8f-133c1ac1c75a.png)

From uBO 1.34.0 and above, you can enable/disable the uncloaking of canonical names. This setting is default enabled.

Before 1.34.0, this was an [advanced setting](./Advanced-settings) since [1.25.0](https://github.com/gorhill/uBlock/releases/tag/1.25.0).

See [_"What's CNAME of your game? This DNS-based tracking defies your browser privacy defenses"_](https://www.theregister.com/2021/02/24/dns_cname_tracking/) for background information.

The setting will be disabled on platforms not supporting this feature. It is currently supported only on Firefox.

In some edge cases, it might be necessary to disable this setting to prevent network-related issues. For example, [_"Pages load slowly when uBlock Origin is installed"_](https://bugzilla.mozilla.org/show_bug.cgi?id=1694404#c5) occurred when funneling network requests through a proxy.

**Important note when using extension-based proxy service:** Extension-based proxy services usually are performed on the fly through a [browser API](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/API/proxy/onRequest). In such a case, uBO's DNS queries to uncloak canonical names will **NOT** be caught and proxied by an extension-based proxy service. So you may want to disable this setting when using an extension-based proxy service.

***

## Appearance

### Theme

Allows choosing between light and dark interface themes. The "auto" option will adapt to the theme selected in the browser.

### Custom accent color

Allows choosing the custom leading color for user interface elements.

Note it will be automatically adjusted to keep proper contrast between interface elements.

### Color-blind friendly

Currently most useful for users who checked _"I am an advanced user"_ (see below).

Changes color coding of blocked/allowed/nooped connections in the overview panel and logger to be more accessible for people with color vision deficiency.

### Disable tooltips

Turns off the popup bubbles with text descriptions when hovering the mouse cursor over user interface elements.

***

## Default behavior

Please see: ["Per site switches"](./Per-site-switches)

***

## Advanced

### I am an advanced user

If you check this, this will enable uBO's [dynamic filtering](./Dynamic-filtering), and the dynamic filtering pane will become available from uBO's popup UI.

Unchecking this disables dynamic filtering, and the associated pane in the popup UI will no longer be available.

_Advanced user_ mode also gives access to the [advanced settings](./Advanced-settings) (usually hidden) and enables filtering [behind-the-scene network requests](./Behind-the-scene-network-requests).

You should avoid playing with advanced features and settings unless [you fully understand what you are doing](./Advanced-user-features).

***

## Backup/restore section

![buttons](https://user-images.githubusercontent.com/95879668/172087321-56d8d75d-2843-4e68-acdd-7b13151940e3.png)

The bottom-most section is for you to conveniently backup/restore/reset settings in uBO.

uBO saves a text file with all setting modified from default, indentifiers of selected filters lists, adresses of custom filter lists, content of "My filters", "My rules" and "Trusted sites", to the location specified by your browser for the backup.

Recommend that you backup all your settings regularly.