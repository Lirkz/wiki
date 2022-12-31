- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)
- Back to [Dashboard: Settings](./Dashboard:-Settings)

***

Support for cloud storage started with uBlock Origin (uBO) 1.1.0.0.

uBO's cloud storage uses your browser's sync feature ([Firefox Sync](https://support.mozilla.org/en-US/kb/how-do-i-set-sync-my-computer) or [Google Account](https://support.google.com/chrome/answer/165139)) to synchronize extension settings across multiple devices.

If your browser/environment does not support cloud storage, the feature will be disabled.

uBO does not need a remote server due to using your browser's built-in sync ability as long as you have enabled it.

The user must explicitly enable cloud storage support on uBO's Settings pane in the dashboard by checking the "Enable cloud storage support" checkbox.

Once you enable cloud storage support, a new UI widget will be available in the dashboard for panes that support the export/import of settings to/from cloud storage.

![screenshot](https://user-images.githubusercontent.com/95879668/173246418-e8101bc9-1ae9-41e5-b99e-1b2b885b1b9f.png)

**Important:** Even if cloud storage support is enabled, it will only work if you have enabled sync support in your browser. uBO itself does not connect to any remote server. Your browser does this through its sync feature if you have enabled this feature.

A narrow, purple-grey strip on the bottom of the cloud storage widget allows for estimating available space on cloud storage servers. The violet part represents the space occupied by settings on the current page. Dark grey represents all storage used by uBO settings. ([1.29.3b7](https://github.com/gorhill/uBlock/commit/2afcc13ca6c09175b33ff74494eba7113ceb3df1))

Your uBO settings are precious. To prevent any automated browser syncing task from overwriting your local or cloud data, **you must expressly ask uBO to export to/import from cloud storage**.

uBO's implemented sync feature is a global clipboard where settings are copied and pasted. Only you decide when to export/import.

The granularity of uBO settings regarding cloud storage support is straightforward. One dashboard pane equals one dedicated cloud storage entry. This way, it is possible for a user to use cloud storage for different panes and choose whether or not to persist a specific pane to the cloud because browser vendors can limit cloud storage.

The import/export of cloud storage data in a pane works strictly at the UI level. When importing cloud storage data, it will fill in the pane's UI as if you entered the data yourself. However, depending on the pane, you will still have to validate/commit the imported data.

Cloud storage providers may refuse an export operation if you reach the cloud storage capacity limit, and the data on the cloud storage will be left untouched.

If you do not have a syncing account with your browser vendor, I have observed that the cloud storage feature can still be used as a local clipboard to save a pane's settings. It might be convenient sometimes, but please do not use cloud storage to replace uBO's [backup feature](./Dashboard:-Settings#backuprestore-section). Regularly backing up your settings is recommended, especially for those having extensive custom static filters, custom rules, or trusted site directives.

**Important:** Some browsers offer to use a passphrase for their sync feature to enable end-to-end encryption of the data stored for sync purposes ([example](https://support.google.com/chrome/answer/165139)). Using such as passphrase is strongly suggested.

#### Caveats

Cloud storage services offered by specific browser vendors have limitations and quirks and are out of the control of uBO.

##### Chromium-based browsers

- Various size limits: for example, on Chrome storage space limit is 102,400 bytes.
- Various limits on the number of operations per unit of time.
- See [`chrome.storage` API](https://developer.chrome.com/docs/extensions/reference/storage/#property-sync) for more technical details.

##### Firefox

- Note that Firefox Sync is not triggered when you export uBO settings. It seems to get executed regularly; however, if you want to force the cloud export, you must launch Firefox Sync manually.

![Sync button](https://user-images.githubusercontent.com/886325/41821498-e081fe7e-77e1-11e8-81de-03a09d826cb9.png)

- I have observed that too large an amount of per-pane data will cause a warning in the browser console (> 8K).
- **A new installation of uBO will erase cloud storage data.**
    - Update: Reportedly fixed in [Bugzilla Report #753289](https://bugzilla.mozilla.org/show_bug.cgi?id=753289) and included in [Firefox 43.0](https://bugzilla.mozilla.org/buglist.cgi?j_top=OR&f1=target_milestone&o3=equals&v3=Firefox%2043&o1=equals&resolution=FIXED&o2=anyexact&query_format=advanced&f3=target_milestone&f2=cf_status_firefox43&bug_status=RESOLVED&bug_status=VERIFIED&bug_status=CLOSED&v1=mozilla43&v2=fixed%2Cverified&limit=0).
    - See <https://discourse.mozilla.org/t/how-to-sync-preferences-of-a-bootstrapped-extension-via-sync/3024>.
    - But since uBO will not automatically import settings from the cloud storage, this will not cause any loss of local ones. However, you will have to push your settings to the cloud storage again.
- Due to [minimal documentation](https://support.mozilla.org/en-US/products/firefox/sync-and-save), there might be undocumented limitations about this in Firefox.
- It appears Firefox for Android can not sync extension settings. This is tracked in [Bugzilla Report #1625257](https://bugzilla.mozilla.org/show_bug.cgi?id=1625257).
- It is unknown if this new feature will work for other Firefox-based browsers.