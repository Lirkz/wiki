Browsers have a list of restricted web pages that do not grant access or permissions to extensions.

These are restricted Chromium<sup>1</sup> domains:

```
clients.google.com
clients[0-9]+.google.com
sb-ssl.google.com
chrome.google.com/webstore/*
chromewebstore.google.com
```

These are restricted Firefox<sup>2</sup> domains:

```
accounts-static.cdn.mozilla.net
accounts.firefox.com
addons.cdn.mozilla.net
addons.mozilla.org
api.accounts.firefox.com
content.cdn.mozilla.net
discovery.addons.mozilla.org
install.mozilla.org
oauth.accounts.firefox.com
profile.accounts.firefox.com
support.mozilla.org
sync.services.mozilla.com
```

- To allow WebExtensions in Firefox to run on these pages (at your own risk), open `about:config` and modify the following<sup>3</sup>:

    - Set `extensions.webextensions.restrictedDomains` to be an empty string.<sup>4</sup>
    - Set `privacy.resistFingerprinting.block_mozAddonManager` to `true`<sup>5</sup>
        - **Firefox 60** - **Firefox 70**: must be manually created by right-clicking and selecting _New > Boolean_<sup>3</sup>
        - **Firefox 71** and later<sup>6</sup>: paste preference name in search bar > in 2nd column set Boolean from single-choice list > click <kbd>➕</kbd> button in 3rd column.

***

[1] [stackoverflow.com](https://stackoverflow.com/questions/11613371/chrome-extension-content-script-on-https-chrome-google-com-webstore/11614440#11614440), [chrome_extensions_client.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/chrome/common/extensions/chrome_extensions_client.cc#235), [extension_urls.cc](https://chromium.googlesource.com/chromium/src/+/ba355f657a607c74f0de82ad925a4dc1a7c9a95b/extensions/common/extension_urls.cc#33), [web_request_permissions.cc](https://chromium.googlesource.com/chromium/chromium/+/26c2ff8d01f1e93082f8fc095e20fb68d5f8c24b/chrome/browser/extensions/api/web_request/web_request_permissions.cc#24)

[2] https://hg.mozilla.org/mozilla-central/rev/39e131181d44

[3] https://www.ghacks.net/2017/10/27/how-to-enable-firefox-webextensions-on-mozilla-websites/

[4] https://bugzilla.mozilla.org/show_bug.cgi?id=1445663#ch-3

[5] https://bugzilla.mozilla.org/show_bug.cgi?id=1310082#c24

[6] https://www.ghacks.net/2019/11/11/firefox-71-new-aboutconfig-interface-lands/