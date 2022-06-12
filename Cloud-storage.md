- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)
- Back to [Dashboard: Settings](./Dashboard:-Settings)

***

Support for cloud storage started with uBlock Origin (uBO) 1.1.0.0.

_Cloud storage_ in uBO is supported through your browser's _sync_ feature, as in [_Firefox Sync_](https://support.mozilla.org/en-US/kb/how-do-i-set-sync-my-computer), or [Chrome browser's Google account](https://support.google.com/chrome/answer/165139), i.e. through your browser's ability to synchronize extensions settings across multiple devices.

If your browser/environment does not support cloud storage, the feature will be disabled.

Using your browser's built-in sync ability means uBO does not need a remote server of its own, your browser's specific solution for syncing data will be used, assuming you enabled such a feature in your browser.

In uBO, cloud storage support must be explicitly enabled by the user, from the _Settings_ pane in the dashboard: check the _"Enable cloud storage support"_ checkbox.

Once you enable cloud storage support, a new UI widget will be available in the dashboard for panes that support the export/import of settings to/from cloud storage:

![screenshot](https://user-images.githubusercontent.com/95879668/173246418-e8101bc9-1ae9-41e5-b99e-1b2b885b1b9f.png)

> ***
> **Important:**
>
> Even if cloud storage support is enabled, it will work **if and only if** you actually enable sync support in your browser -- as uBO itself does not connect to any remote server, your browser does this through its own sync feature, if you enabled such feature.
> ***

A narrow, purple-grey strip on the bottom of the cloud storage widget allows estimating available space on cloud storage servers. The violet part represents the space occupied by settings on the current page. Dark grey represents all storage used by uBO settings. ([1.29.3b7](https://github.com/gorhill/uBlock/commit/2afcc13ca6c09175b33ff74494eba7113ceb3df1))

Your uBO settings are precious, and in order to prevent any automated browser's syncing task to cause precious local data (or cloud data) to be mistakenly overwritten, the chosen solution in uBO is to _never_ ever export to/import from cloud storage without **the user expressly asking uBO to do so**.

So essentially, the sync feature in uBO is implemented as a global clipboard (through cloud storage) to where settings are copied to/pasted from, and only you decide when to export/import.

The granularity of uBO settings regarding cloud storage support is straightforward: one dashboard pane = one dedicated cloud storage entry. This way it is possible for a user to use cloud storage for specific panes, and not for others. Given that cloud storage is limited by browser vendors, one can choose to not persist one specific pane to the cloud.

The import/export of cloud storage data in a pane works strictly at the UI level, i.e. when you import cloud storage data, it will fill in the pane's UI as if you entered the data yourself: depending on the pane, you will still have to validate/commit the imported data.

If ever an export operation causes the cloud storage capacity limit to be reached, typically the cloud storage providers will refuse the operation, and the data on the cloud storage will be left unchanged. This is what I have observed with Chromium-based browsers.

If you do not have a syncing account with your browser vendor, I have observed that the cloud storage feature can still be used as a local clipboard to save a pane's settings. Might be convenient sometimes, but please do not use cloud storage as a replacement for uBO's [backup feature](./Dashboard:-Settings#backuprestore-section). It is recommended you back up your settings regularly, this is especially true for those who have extensive custom static filters, custom rules or trusted sites directives.

> ***
> **Important:**
>
> Some browsers offer the ability to use a passphrase for their sync feature, in order to enable end-to-end encryption of the data stored for sync purpose ([example](https://support.google.com/chrome/answer/165139)). It is strongly suggested to make use of such a passphrase.
> ***

#### Caveats

Cloud storage services offered by specific browser vendors have their own limitations and quirks -- and this is out of control of uBO.

##### Chromium-based browsers

- Various size limits: for example, on Chrome storage space limit is 102,400 bytes.
- Various limits on the number of operations per unit of time.
- See [`chrome.storage` API](https://developer.chrome.com/docs/extensions/reference/storage/#property-sync) for more technical details.

##### Firefox browsers

- Note that Firefox Sync is not triggered when you export uBO settings, it seems to be executed regularly however if you want to force the cloud export you have to launch Firefox Sync manually.
![Sync button](https://user-images.githubusercontent.com/886325/41821498-e081fe7e-77e1-11e8-81de-03a09d826cb9.png)
- I have observed that too large an amount of per-pane data will cause a warning in the browser console (> 8K).
- **A new installation of uBO will cause cloud storage data to be blanked.**
    - Update: [Reportedly fixed in BZ#753289](https://bugzilla.mozilla.org/show_bug.cgi?id=753289), included in [Firefox 43.0](https://bugzilla.mozilla.org/buglist.cgi?j_top=OR&f1=target_milestone&o3=equals&v3=Firefox%2043&o1=equals&resolution=FIXED&o2=anyexact&query_format=advanced&f3=target_milestone&f2=cf_status_firefox43&bug_status=RESOLVED&bug_status=VERIFIED&bug_status=CLOSED&v1=mozilla43&v2=fixed%2Cverified&limit=0)
    - See: <https://discourse.mozilla.org/t/how-to-sync-preferences-of-a-bootstrapped-extension-via-sync/3024>.
    - But since uBO won't automatically import settings from the cloud storage, this will not cause any loss of local settings. However, you will have to push again your settings to the cloud storage.
- There is [not much doc about this for Firefox](https://support.mozilla.org/en-US/products/firefox/sync-and-save), so there might be undocumented limitations yet to be found.
- It appears Firefox for Android can't sync extensions settings. This is tracked in [Bugzilla #1316442](https://bugzilla.mozilla.org/show_bug.cgi?id=1316442).
- Other Firefox-related platforms:
    - I have no clue whether this new feature will work for other brands of Firefox-based browsers.