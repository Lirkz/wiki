uBO supports being configured through central policies, see browser documentation for administrators:

- Chromium: ["Configuring Apps and Extensions by Policy"](https://www.chromium.org/administrators/configuring-policy-for-extensions)
- Firefox: ["Managed storage manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#Managed_storage_manifests)

The documented settings below are only available with uBO version 1.33.0 and above.

## advancedSettings

The purpose of the `advancedSettings` property is to set the values of various [advanced settings](./Advanced-settings).

Each entry in the array is an array consisting of a pair of name-value strings. Each name string must be a supported advanced setting, and each value string must properly resolve to a supported value.

Every valid entry will be used to overwrite the corresponding default advanced setting, and will also become read-only, i.e. the user won't be able to change it.

Example:

    {
        "advancedSettings": [
            [ "disableWebAssembly", "true" ]
        ]
    }

## disableDashboard

Set to `true` to prevent access to uBO's dashboard.

## disabledPopupPanelParts

An array of strings, where each string refer to a part of the popup panel which should be removed from view. Current supported named parts:

- `globalStats`: remove access to _"Blocked since install"_ statistic.
- `basicTools`: remove access to [basic tools](./Quick-guide:-popup-user-interface#the-tools).
- `extraTools`: remove access to [per-site switches](./Quick-guide:-popup-user-interface#the-per-site-switches).
- `overviewPane`: remove access to the [overview pane](./Quick-guide:-popup-user-interface#the-overview-panel).

## toOverwrite

The properties in the `toOverwrite` branch will wholly replace the corresponding local settings. Currently, the following properties are supported:

### filterLists

The `filterLists` property is an array of strings, where each string is a token which identifies a list to enable by default. To enable a stock filter list, this is the token identifying the list as per content of [`assets.json`](https://github.com/gorhill/uBlock/blob/master/assets/assets.json). For an external list, i.e. not found in `assets.json`, the token is the URL of the filter list.

### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of string, each of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled.

All the directives will be used to wholly replace the local trusted-site directives, including the built-in ones.

See documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)

## toAdd

The properties in the `toAdd` branch will append to the already present local settings. Currently, the following properties are supported:

### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of string, each of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled.

The directives will be appended to the local ones.

See documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)
