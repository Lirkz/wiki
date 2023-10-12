- Back to ["Deploying uBlock Origin"](./Deploying-uBlock-Origin)

***

I do not know much about enterprise deployment, so I will let a knowledgeable person guide you:

- [Managing Google Chrome with adblocking and security](https://web.archive.org/web/20220816090848/https://decentsecurity.com/ublock-for-google-chrome-deployment/) [via archive.org] by [SwiftOnSecurity](https://twitter.com/SwiftOnSecurity/status/783348579943317504)
- [Deploy Firefox in the Enterprise with uBlock Origin, HTTPS Everywhere and Privacy Badger using Group Policy](https://www.winsysadminblog.com/2019/03/deploy-firefox-in-the-enterprise-with-ublock-origin-https-everywhere-and-privacy-badger-using-group-policy/) by [John](https://www.winsysadminblog.com/about-me/)
- [How To Deploy AdBlocker for Enterprise](https://www.secjuice.com/how-to-deploy-adblocker-for-smbs/) by [Secjustice](https://twitter.com/secjuice)
- [Tutorial: Deploying uBO configuration for Microsoft Edge Chromium and Google Chrome - older way](https://www.reddit.com/r/uBlockOrigin/comments/o7q2ou/comment/h3cplhd/) by [u/DefinitelyYou](https://www.reddit.com/user/DefinitelyYou)
- [Add group policy templates to aid configuring in Chrome, Edge, and Firefox on Windows](https://github.com/gorhill/uBlock/pull/3865)

### Customizing the settings

Administrators can force specific configurations to deploy uBlock Origin (uBO). At launch time, uBO will look for a setting named `adminSettings`, and if it exists, it will parse, extract and overwrite a user's settings with the administrator-assigned ones. Note that Chromium managed storage is not always ready on first browser start after change, and up to three restarts may be needed for settings to be applied to uBO, see [#1547](https://github.com/uBlockOrigin/uBlock-issues/issues/1547), [#1608](https://github.com/uBlockOrigin/uBlock-issues/issues/1608).

New standalone settings are getting added as per demand. See ["Deploying uBlock Origin: configuration"](./Deploying-uBlock-Origin:-configuration).

For **Firefox**, the setting can be configured in ["Native manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests) and [Policies](https://support.mozilla.org/en-US/kb/customizing-firefox-using-policiesjson). Refer to Mozilla documentation about ["Managed storage manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#managed_storage_manifests) and [its location](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#manifest_location) for the Native manifests approach. See Mozilla's [policy template](https://github.com/mozilla/policy-templates#3rdparty) for the Policies approch. You can also consult [this specific comment](https://github.com/gorhill/uBlock/issues/2986#issuecomment-364035002) in uBO issue tracker.

For **Chrome**, `adminSettings` must be an entry part of the policy for the extension. See <https://www.chromium.org/administrators/configuring-policy-for-extensions/>.

For managing **Chrome** via **Google Workspace**, you can use [this apps-script](https://github.com/Landsil/apps_script--GoogleWorkspace-API/blob/master/uBlock_Origin_GSuite_policy.gs) to generate a policy JSON that will modify Trusted Sites for all designated users.

The content of `adminSettings` is pretty straightforward: configure uBO as you wish for your users, then create a backup using the _"Backup to file"_ in the _Settings_ pane. Now open this backup file using a text editor, and remove all entries you do not want to overwrite while taking care to end up with a valid JSON file (mind trailing commas, etc.). All the entries left are the ones that will become overwritten on the user's side.

For example, I created a backup file after having customized uBO and removed everything except for the _"Color-blind friendly"_ setting to force that setting to be set on the user's side. Resulting text file:

    {
      "userSettings": {
        "colorBlindFriendly": true
      }
    }

Now, this JSON object can be used as the value for `adminSettings`.

### Modifying the list of stock assets

You can configure the content of the "Filter lists" tab by providing a custom version of the [`assets.json`](https://github.com/gorhill/uBlock/blob/16a0ebbfb05c4582ecc68454ba3b45b403164dde/assets/assets.json) file.

In the `assetsBootstrapLocation` key, you must add the URL of the modified `assets.json` file.

Implementation: [#2314](https://github.com/gorhill/uBlock/pull/2314)

### Further readings

Here are issues related to the customization of settings for deployed uBO. There may be some advice in these that you find helpful:
- https://github.com/gorhill/uBlock/issues/832
- https://github.com/gorhill/uBlock/issues/531
- https://github.com/gorhill/uBlock/issues/2986#issuecomment-333198882