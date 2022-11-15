uBlock Origin (uBO) supports configuration through central policies. See browser documentation for administrators:

- Chromium: ["Configuring Apps and Extensions by Policy"](https://www.chromium.org/administrators/configuring-policy-for-extensions/)
- Firefox: ["Managed storage manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#managed_storage_manifests)
- [Tutorial: Deploying uBO configuration for Microsoft Edge Chromium and Google Chrome - newer way](https://www.reddit.com/r/uBlockOrigin/comments/o7q2ou/comment/h3crkxf/) (Editing Registry by PowerShell) by [u/DefinitelyYou](https://www.reddit.com/user/DefinitelyYou)
- [Deploying uBlock via Google workspace? (Q&A discussion)](https://github.com/uBlockOrigin/uBlock-issues/discussions/1834) (with a successful deployment)

The documented settings below are only available with uBO version 1.33.0 and above.

## userSettings

The purpose of the `userSettings` property is to set the values of various [user settings](./Dashboard:-Settings) (more specifically, to modify [these variables](https://github.com/gorhill/uBlock/blob/1c3b45f75d0f84d68abb51b15bbdc043464ee3e0/src/js/background.js#L86-L109)).

Each entry in the array consists of a pair of name-value strings. Each name string must be a supported user setting, and each value string must correctly resolve to a supported value.

Every valid entry gets used to overwrite the corresponding default user setting at launch time.

Example:

    {
        "userSettings": [
            [ "contextMenuEnabled", "false" ],
            [ "dynamicFilteringEnabled", "false" ]
        ]
    }

## advancedSettings

The `advancedSettings` property is to set the values of various [advanced settings](./Advanced-settings).

Each entry in the array consists of a pair of name-value strings. Each name string must be a valid advanced setting, and each value string must correctly resolve to a supported value.

Every valid entry will get used to overwrite the corresponding default advanced setting and become read-only. The user will not be able to change it.

Example:

    {
        "advancedSettings": [
            [ "disableWebAssembly", "true" ]
        ]
    }

## disableDashboard

Set to `true` to prevent access to uBO's dashboard.

## disabledPopupPanelParts

An array of strings where each string refers to a part of the popup panel that gets removed. Each supported component and its name:

- `globalStats`: remove access to _"Blocked since install"_ statistic.
- `basicTools`: remove access to [basic tools](./Quick-guide:-popup-user-interface#the-tools).
- `extraTools`: remove access to [per-site switches](./Quick-guide:-popup-user-interface#the-per-site-switches).
- `overviewPane`: remove access to the [overview pane](./Quick-guide:-popup-user-interface#the-overview-panel).

## toOverwrite

The properties in the `toOverwrite` branch will wholly replace the corresponding local settings. Currently, the following properties are supported:

#### filters

The `filters` property is an array of strings that represent all the lines making the text to use as the content of the [_"My filters"_ pane](./Dashboard:-My-filters).

#### filterLists

The `filterLists` property is an array of strings, where each one is a token that identifies a list to enable by default. To activate a stock filter list, this is the token identifying the list per the contents of [`assets.json`](https://github.com/gorhill/uBlock/blob/master/assets/assets.json). For an external list not found in `assets.json`, the token is the URL of the filter list.

Use the token `user-filters` in your list of filter lists to enforce the filters in the _"My filters"_ pane.

For reference, the following array corresponds to the default list of filter lists enabled in uBO by default:

    [
      "user-filters",
      "ublock-filters",
      "ublock-badware",
      "ublock-privacy",
      "ublock-abuse",
      "ublock-unbreak",
      "easylist",
      "easyprivacy",
      "urlhaus-1",
      "plowe-0"
    ]

Additionally, according to the current locale, one or more regional lists may be enabled.

#### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of strings, each of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled.

All directives will replace the local trusted-site rules, including the built-in ones.

See the documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)

## toAdd

The properties in the `toAdd` branch will append to the already present local settings. Currently, the following properties are supported:

#### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of strings, each of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled.

Here is an example of how adding `example.com` and `example.org` would look like for managed storage on Chromium/Linux:

    xxxxx@xxxxx:~$ cat /etc/chromium/policies/managed/ubo.json
    {
      "3rdparty": {
        "extensions": {
          "cjpalhdlnbpafiamejdnhcphjbkeiagm": {
            "toAdd": {
              "trustedSiteDirectives": [
                "example.com",
                "example.org"
              ]
            }
          }
        }
      }
    }

The directives will get appended to the local ones.

See the documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)