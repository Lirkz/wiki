- Back to ["Deploying uBlock Origin"](./Deploying-uBlock-Origin)

***

I do not know much about enterprise deployment, so I will let a knowledgeable person guide you:

- [Managing Google Chrome with adblocking and security](https://web.archive.org/web/20220816090848/https://decentsecurity.com/ublock-for-google-chrome-deployment/) [via archive.org] by [SwiftOnSecurity](https://twitter.com/SwiftOnSecurity/status/783348579943317504)
- [Deploy Firefox in the Enterprise with uBlock Origin, HTTPS Everywhere and Privacy Badger using Group Policy](https://www.winsysadminblog.com/2019/03/deploy-firefox-in-the-enterprise-with-ublock-origin-https-everywhere-and-privacy-badger-using-group-policy/) by [John](https://www.winsysadminblog.com/about-me/)
- [How To Deploy AdBlocker for Enterprise](https://www.secjuice.com/how-to-deploy-adblocker-for-smbs/) by [Secjustice](https://twitter.com/secjuice)
- [Tutorial: Deploying uBO configuration for Microsoft Edge Chromium and Google Chrome - older way](https://www.reddit.com/r/uBlockOrigin/comments/o7q2ou/comment/h3cplhd/) by [u/DefinitelyYou](https://www.reddit.com/user/DefinitelyYou)
- [Add group policy templates to aid configuring in Chrome, Edge, and Firefox on Windows](https://github.com/gorhill/uBlock/pull/3865)

### Customizing the settings

Administrators can force specific configurations to deploy uBlock Origin (uBO). At launch time, uBO will look for a setting named `adminSettings`, and if it exists, it will parse, extract and overwrite a user's settings with the administrator-assigned ones.

New standalone settings are getting added as per demand. See ["Deploying uBlock Origin: configuration"](./Deploying-uBlock-Origin:-configuration).

For **Firefox**, refer to Mozilla documentation about ["Native manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests) (sections about ["Managed storage manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#managed_storage_manifests) and [its location](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#manifest_location)). You can also consult [this specific comment](https://github.com/gorhill/uBlock/issues/2986#issuecomment-364035002) in uBO issue tracker.

You must add the `adminSettings` entry in `about:config` for **Firefox-legacy**. The key name is `extensions.ublock0.adminSettings`, and the value is a plain string that must be JSON-parseable.

For **Chrome**, `adminSettings` must be an entry part of the policy for the extension. See <https://www.chromium.org/administrators/configuring-policy-for-extensions/>.

For managing **Chrome** via **Google Workspace**, you can use [this apps-script](https://github.com/Landsil/apps_script--GoogleWorkspace-API/blob/master/uBlock_Origin_GSuite_policy.gs) to generate a policy JSON that will modify Trusted Sites for all designated users.

This effort is still a work in progress with limitations. For example, merging an admin's settings with the user's settings is impossible because the settings get overwritten. Hopefully, I will address this limitation eventually, as time permits. (See https://github.com/gorhill/uBlock/issues/832#issuecomment-248138558).

The content of `adminSettings` is pretty straightforward: configure uBO as you wish for your users, then create a backup using the _"Backup to file"_ in the _Settings_ pane. Now open this backup file using a text editor, and remove all entries you do not want to overwrite while taking care to end up with a valid JSON file (mind trailing commas, etc.). All the entries left are the ones that will become overwritten on the user's side.

For example, I created a backup file after having customized uBO and removed everything except for the _"Color-blind friendly"_ setting to force that setting to be set on the user's side. Resulting text file:

    {
      "userSettings": {
        "colorBlindFriendly": true
      }
    }

Now, the value for `adminSettings` must be a plain string which means we need to encode the above text into a string using `JSON.stringify`. Here is a small utility to help you with this step: <http://raymondhill.net/ublock/adminSetting.html>.

### Modifying the list of stock assets

You can configure the content of the "Filter lists" tab by providing a custom version of the [`assets.json`](https://github.com/gorhill/uBlock/blob/16a0ebbfb05c4582ecc68454ba3b45b403164dde/assets/assets.json) file.

In the `assetsBootstrapLocation` key, you must add the URL of the modified `assets.json` file.

Implementation: [#2314](https://github.com/gorhill/uBlock/pull/2314)

### Further readings

Here are issues related to the customization of settings for deployed uBO. There may be some advice in these that you find helpful:
- https://github.com/gorhill/uBlock/issues/832
- https://github.com/gorhill/uBlock/issues/531
- https://github.com/gorhill/uBlock/issues/2986#issuecomment-333198882