[Back to Dashboard: Settings](./Dashboard:-Settings)

***

Option removed from desktop browsers in [uBlock Origin v1.38](https://github.com/uBlockOrigin/uBlock-issues/issues/1723).

Browsers now obfuscate LAN addresses by mDNS:

- Firefox: ["Enable mDNS hostname obfuscation"](https://bugzilla.mozilla.org/show_bug.cgi?id=1588817)
- Chromium: ["mDNS service for IP handling in WebRTC"](https://bugs.chromium.org/p/chromium/issues/detail?id=878465)

Option is still available in Android Firefox, because obfuscation is still not implemented there: ["Support mDNS hostname obfuscation on Android"](https://bugzilla.mozilla.org/show_bug.cgi?id=1581947)

***

Keep in mind that this feature is to prevent leakage of your non-internet-facing IP adresses. The purpose of this feature is not to hide your current internet-facing IP address -- so be cautious to not misinterpret the results of some WebRTC-local-IP-address-leakage tests found online.

**Important:** Enabling this feature can cause issues for some WebRTC-related services. If this is the case, you will have to disable it to prevent the breakage.

For example, if you use a VPN, your internet-facing IP address is that of the VPN, so your ISP-provided IP address should not be visible to outside world with this setting checked. However, if you are not behind any VPN or proxy, your ISP-provided IP address will be visible regardless of this setting.

Tests:
- [Trickle ICE](https://webrtc.github.io/samples/src/content/peerconnection/trickle-ice/)
    - Click the <kbd>Gather candidates</kbd> button at the bottom; there should be no local IP addresses reported
- [WebRTC Leak Test](https://browserleaks.com/webrtc)
    - The entry "Local IP Address" should be "n/a"

#### Caveats

##### Chromium-based browsers

It has been reported that Google Hangout and Facebook messenger do not work properly when this setting is enabled (issue [#757](https://github.com/gorhill/uBlock/issues/757), [#681](https://github.com/gorhill/uBlock/issues/681)).

If you are using an extension-based VPN, this setting won't [prevent your ISP IP address from leaking](https://code.google.com/p/chromium/issues/detail?id=457492#c44).

Also: ["When using a proxy, WebRTC leaks unproxied IP address even with multiple routes disabled"](https://code.google.com/p/chromium/issues/detail?id=497040) (reportedly fixed in Chromium 47, [see comment #25](https://bugs.chromium.org/p/chromium/issues/detail?id=497040#c25)).

The feature works only on version 42 and above.

##### Firefox

With Firefox 41 and lower **OR** uBlock Origin 1.3.3 and lower, **it is NOT possible** to prevent local IP addresses leakage without completely disabling WebRTC.

With Firefox 42 and higher **AND** uBlock Origin 1.3.4 and higher, **it is possible** to prevent local IP addresses leakage without completely disabling WebRTC.

Due to differences in handling of network connections by different browsers, before version [1.18.12](https://github.com/gorhill/uBlock/commit/977178bef23c7711a050181be979a4668bfebcfb) WebRTC was completely disabled if Firefox was not configured to use proxy. Related issue: [#3009](https://github.com/gorhill/uBlock/issues/3009#issuecomment-329798696)

#### See also

- [WebRTC WG / Privacy/IPAddresses](https://www.w3.org/wiki/Privacy/IPAddresses)