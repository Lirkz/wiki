- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)

***

- [Filter list licenses ↪](./Filter-list-licenses)

***

The _Filter lists_ pane is where you subscribe to filter lists. The filter lists to which you subscribe will feed uBlock Origin's [static filtering engine](./Overview-of-uBlock's-network-filtering-engine:-details#static-filtering).

The picture below shows uBlock Origin's default selection of filter lists. You can add more, or remove some of the filter lists already selected by default (for reference, most other blockers have only EasyList selected).

If you remove filter lists, it is still strongly advised to at least keep _uBlock filters_ selected: these filters are optimized for uBlock Origin.

The more filter lists you add, the higher the likelihood some web pages may not render properly, due to the higher probability of false positives. When this occurs, you should report the issue to the maintainers of the filter list causing the issue, or create your own exception filters to fix the issue.

![Filter lists pane](https://user-images.githubusercontent.com/886325/148105230-2a8abe39-c320-4c24-8c32-d17da8d2f029.png) |
--- |

uBlock Origin discards duplicate filters, so the number of filters used within a filter list depends on how many duplicate filters were detected within that filter list. The order in which the filter lists are loaded into memory is undefined.

When you hover the cursor over the clock icon of a filter list, a tooltip will tell you when the list was last updated. If you click the clock icon, uBlock Origin will mark the list as out-of-date. Lists that are out of date will be automatically updated in the background eventually when you check the option _"Auto update filter lists"_. You can force out-of-date lists to be immediately updated by clicking _"Update now"_.

Related: [_"Launch and filter lists load performance"_](./Launch-and-filter-lists-load-performance).

***

### Update now

![_"Update now"_ button](https://user-images.githubusercontent.com/585534/143616552-94dd8b15-d33c-4d45-97bd-2f73f95972ba.png)

This button is available for use if and only if there is at least one filter list that is deemed outdated. If this condition is fulfilled, you can force an update of all filter lists which are deemed out of date.

When a filter list has been updated using a newer version from its remote location, a clock icon will be present aside the filter list. You can force an update of a single filter list by clicking the clock icon of that filter list only, which will reset the "last update" timestamp for this list, remove its content from storage, and cause the _"Update now"_ button to become available for use:

![update by clock icon](https://user-images.githubusercontent.com/886325/148108034-73419703-10a1-4f72-af4b-5dd5231fface.gif)

Note: When forcing an update of the "uBlock filters" entry itself, this will also update additional resources when possible. (Library of resources used by [Scriptlet injection](./Static-filter-syntax#scriptlet-injection) allowed to be updated on Chromium-based browsers and development builds).

***

### Purge all caches

![_"Purge all caches"_ button](https://user-images.githubusercontent.com/585534/143480823-7b54e49d-fea7-4416-963d-c679243c770d.png)

This will reset the "last update" timestamp for all of the subscribed filter lists. Essentially, this will cause all filter lists to become out of date. This can be used to force an update of all filter lists.

Clicking this button with <kbd>Shift</kbd> (version [before 1.34](https://github.com/gorhill/uBlock/commit/972feae05d22239c46b837e64001f9f322724585) required also <kbd>Ctrl</kbd>) pressed will remove all locally cached content of filter lists, which will force uBlock Origin to rebuild all of its databases from the beginning.

***

### Auto-update filter lists

If you check this option, uBlock Origin will automatically update the currently selected filter lists at regular intervals. This option is checked by default (recommended).

Filter lists are automatically updated according to:
- the [_Expires_ directive](https://help.eyeo.com/en/adblockplus/how-to-write-filters#special-comments) if present in the filter list header
- or the `updateAfter` attribute if found in the list entry in [`assets.json`](https://github.com/gorhill/uBlock/blob/master/assets/assets.json)
- or every 5 days by default.

***

### Parse and enforce cosmetic filters

Uncheck this option if you do not want cosmetic filters from various filter lists to be parsed and enforced. This option is mostly of interest for those who want to further reduce uBlock Origin's memory and CPU footprint. Cosmetic filtering has no value privacy-wise, its only purpose is to [hide elements](./Does-uBlock-Origin-block-ads-or-just-hide-them%3F) on a web page that can't be blocked otherwise. An example of this is the ads served with some Google Search results.

Note that if you disable this option, your own custom cosmetic filters in `My Filters` (if any) will still be enforced.

***

### Ignore generic cosmetic filters 

Generic cosmetic filters are those cosmetic filters that are meant to apply on all websites. Though handled efficiently by uBlock Origin, generic cosmetic filters may still end up contributing measurable memory and CPU overhead on some web pages, especially the large and long-lived ones.
Enabling this option will eliminate the memory and CPU overhead added to web pages as a result of handling generic cosmetic filters, and also lower the memory footprint of uBlock Origin itself.
This option can be enabled on very low-end devices, but mind that some filter lists (EasyList Cookie for ex.) rely on generic cosmetic filters a lot, so they may pretty much stop working.

***

### Suspend network activity until all filter lists are loaded

New in [1.40.3b1](https://github.com/gorhill/uBlock/commit/925c8d5d0c37dbc1f82e57a92e74350de2c5eab1) development version. Will be available in stable next release cycle.

This new setting suspends network activity until uBlock Origin has loaded all filter lists into memory. The default for this setting is enabled.

If this behavior is undesirable, disable the setting to prevent uBlock Origin from suspending network activity when the browser launches.

This setting gives the option to potentially speed up page load at launch, at the cost of possibly not properly filtering network requests as per filter lists or rules.

This setting will use any mechanism on the platform not supporting network activity suspension to mitigate the improper filtering of network requests at launch. For example, in Chromium-based browsers, disabling the setting will prevent the browser from reloading tabs in which there was network activity while being in a suspended state at launch.

See also [`suspendTabsUntilReady`](./Advanced-settings#suspendtabsuntilready).

***

### Stock filter lists

This is a collection of various filter lists, grouped by purpose. To use a specific filter list, just select it through its checkbox. Any change in the selection of filter lists must be committed by using the _Apply change_ button, which will appear if and only if the current selection of filter lists differs from the previous selection of filter lists.

#### Important

The more filter lists are selected, the higher the likelihood of website breakage. The quality of the selected filter lists also affects the likelihood of website breakage. The _EasyList_-related filter lists are high-quality filter lists, as they are actively maintained.

***

### 3rd-party filter lists

#### Adding Manually

To add a 3rd-party filter list, place a checkmark next to _Import_ under the _Custom_ section near the bottom of the _Filter lists_ pane. Paste the URL of the filter list into the text area that appears below. (You can add multiple filter lists at once; however, only one URL per line. Invalid URLs will be silently ignored). These filter lists are automatically updated regularly.

![custom-filter-lists](https://user-images.githubusercontent.com/886325/41821466-99d67040-77e1-11e8-9973-08f9fe4f4049.png)

To remove a 3rd-party filter list, click the trash can icon at the end of the filter list name. Then click on the _Apply changes_ button. The removed filter list will disappear.

#### Adding via Approved External Websites

You can subscribe to 3rd-party filter lists by clicking on a link for them on these approved external websites.

<p>https://easylist.to/*<br>
https://*.fanboy.co.nz/*<br>
https://filterlists.com/*<br>
https://forums.lanik.us/*<br>
https://github.com/*<br>
https://*.github.io/</p>