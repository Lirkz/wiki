uBO supports being configured through central policies, see browser documentation for administrators:

- Chromium: ["Configuring Apps and Extensions by Policy"](https://www.chromium.org/administrators/configuring-policy-for-extensions)
- Firefox: ["Managed storage manifests"](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Native_manifests#Managed_storage_manifests)

## toSet

The properties in the `toSet` branch will wholly replace the corresponding local settings. Currently, the following subset of properties are supported:

### hiddenSettings

The purpose of the `hiddenSettings` property is to set the values of various [advanced settings](./Advanced-settings).

Each entry in the array is an array consisting of a pair of name-value strings. Each name string must be a supported advanced setting, and each value string must properly resolve to a supported value.

Every valid entry will be used to overwrite the corresponding default advanced setting, and will also become read-only, i.e. the user won't be able to change it.

Example, to remove the ability to configure uBO from the popup panel:

    {
        "toSet": {
            "hiddenSettings": [
                [ "popupPanelDisabledSections", "28" ]
            ]
        }
    }

### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of string, which of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled. All the directives will be used to wholly replace the local trusted-site directives, including the built-in ones.

See documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)

## toAdd

The properties in the `toAdd` branch will append to the already present local settings. Currently, the following subset of properties are supported:

### trustedSiteDirectives

The `trustedSiteDirectives` property is an array of string, which of which must resolve into a valid trusted-site directive, used to dictate where uBO must be disabled. The directives will be appended to the local ones.

See documentation on how to create valid trusted-site directives: ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted)
