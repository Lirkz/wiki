Keep in mind that this feature is to prevent leakage of your non-internet-facing IP adresses. The purpose of this feature is not to hide your current internet-facing IP address -- so be cautious to not misinterpret the results of some WebRTC-local-IP-address-leakage tests found online.

For example, if you use a VPN, your internet-facing IP address is that of the VPN, so your ISP-provided IP address should not be visible to outside world with this setting checked. However, if you are not behind any VPN or proxy, your ISP-provided IP address will be visible regardless of this setting.

#### Caveats

##### Chromium-based browsers

It has been reported that Google Hangout and Facebook messenger do not work properly when this setting is enabled (issue [#757](https://github.com/gorhill/uBlock/issues/757), [#681](https://github.com/gorhill/uBlock/issues/681)).

The feature works only on version 42 and above.

##### Firefox

WebRTC is required for Firefox Hello to work properly. Thus Firefox Hello won't work if you enable this setting.