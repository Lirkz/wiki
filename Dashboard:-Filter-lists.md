- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)

***

- [Filter list licenses](./Filter-list-licenses)

***

The _Filter lists_ pane is where you subscribe to filter lists that feed into uBlock Origin (uBO)'s [static filtering engine](./Overview-of-uBlock's-network-filtering-engine:-details#static-filtering).

The picture below shows uBO's default selection of filter lists. You can add more or remove some filter lists already selected by default. (Most other blockers only enable EasyList.)

If you remove filter lists, keeping the _uBlock filters_ is strongly recommended due to their optimization for uBO.

The likelihood of page breakage increases with more filter lists added. When this issue occurs, you should report it to the maintainers of the corresponding filter list or create an exception filter to fix it for yourself.

![Filter lists pane](https://user-images.githubusercontent.com/95879668/152668651-7032a46d-8e66-4f8e-9e2b-dee79e73a972.png)

---

uBO discards duplicate filters, so the number of filters used within a filter list depends on how many duplicates were detected. The order in which filter lists get loaded into memory is undefined.

When you hover the cursor over the clock icon of a filter list, a tooltip will display the last updated time. If you click the clock icon, uBO will mark the list as out-of-date. Outdated lists will be automatically updated in the background when you check the _Auto update filter lists_ option. You can force update outdated lists immediately by clicking the _Update now_ button.

Related: [Launch and filter lists load performance](./Launch-and-filter-lists-load-performance)

***

### Update now

![_"Update now"_ button](https://user-images.githubusercontent.com/585534/143616552-94dd8b15-d33c-4d45-97bd-2f73f95972ba.png)

This button is available only if there is at least one filter list that is out of date. You can force an update of all outdated filter lists.

When a filter list gets updated using a newer version from its remote location, a clock icon will appear next to it. You can force an update of a single filter list by clicking the clock icon. Clicking this icon will reset the last updated timestamp, remove its content from storage, and cause the _Update now_ button to become available.

![update by clock icon](https://user-images.githubusercontent.com/886325/148108034-73419703-10a1-4f72-af4b-5dd5231fface.gif)

Forcing an update of the "uBlock filters" entry will also update additional resources when possible. (On Chromium-based browsers and development builds, the Resources Library used by [scriptlet injection](./Static-filter-syntax#scriptlet-injection) gets updated.)

***

### Purge all caches

![_"Purge all caches"_ button](https://user-images.githubusercontent.com/585534/143480823-7b54e49d-fea7-4416-963d-c679243c770d.png)

This will reset the "last update" timestamp for all of the subscribed filter lists. Essentially, this will cause all filter lists to become out of date. This can be used to force an update of all filter lists.

Clicking this button with <kbd>Shift</kbd> (version [before 1.34](https://github.com/gorhill/uBlock/commit/972feae05d22239c46b837e64001f9f322724585) required also <kbd>Ctrl</kbd>) pressed will remove all locally cached content of filter lists, which will force uBO to rebuild all of its databases from the beginning.

***

### Auto-update filter lists

If you check this option, uBO will automatically update the currently selected filter lists at regular intervals. This option is checked by default (recommended).

Filter lists are automatically updated according to:
- the [_Expires_ directive](https://help.eyeo.com/en/adblockplus/how-to-write-filters#special-comments) if present in the filter list header (After [1.47.3b5](https://github.com/gorhill/uBlock/commit/db118483c91da468d22b943aba07bbcfc2e37427), uBO supports an update period below 1-day).
- or the `updateAfter` attribute if found in the list entry in [`assets.json`](https://github.com/gorhill/uBlock/blob/master/assets/assets.json)
- or every 5 days by default.

***

### Parse and enforce cosmetic filters

Uncheck this option if you do not want cosmetic filters from various filter lists to be parsed and enforced. This option is mostly of interest for those who want to further reduce uBO's memory and CPU footprint. Cosmetic filtering has no value privacy-wise, its only purpose is to [hide elements](./Does-uBlock-Origin-block-ads-or-just-hide-them%3F) on a web page that can't be blocked otherwise. An example of this is the ads served with some Google Search results.

Note that if you disable this option, your own custom cosmetic filters in `My Filters` (if any) will still be enforced.

***

### Ignore generic cosmetic filters

Generic cosmetic filters are those cosmetic filters that are meant to apply on all websites. Though handled efficiently by uBO, generic cosmetic filters may still end up contributing measurable memory and CPU overhead on some web pages, especially the large and long-lived ones.
Enabling this option will eliminate the memory and CPU overhead added to web pages as a result of handling generic cosmetic filters, and also lower the memory footprint of uBO itself.
This option can be enabled on very low-end devices, but mind that some filter lists (EasyList Cookie for ex.) rely on generic cosmetic filters a lot, so they may pretty much stop working.

***

### Suspend network activity until all filter lists are loaded

This setting suspends network activity until uBO has loaded all filter lists into memory.

In Firefox-based browsers, this setting is enabled by default. Disabling it gives the option to potentially speed up page load at browser launch, at the cost of possibly not properly filtering network requests as per filter lists or rules.

In Chromium-based browsers, this setting is disabled by default, since Chromium-based browsers do not support natively suspending network requests.<sup>2</sup> Enabling this setting in Chromium-based browsers _may_ lead to negative side-effects at browser launch.

<sub>__1__ New in [1.41.0](https://github.com/gorhill/uBlock/commit/925c8d5d0c37dbc1f82e57a92e74350de2c5eab1).</sub><br>
<sub>__2__ This setting will use any mechanism on the platform not supporting network activity suspension to mitigate the improper filtering of network requests at launch. For example, in Chromium-based browsers it's not possible to suspend network activity, in which case this setting will only force a reload of the webpage once uBO is fully loaded.<sub>

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

`https://easylist.to/*`  
`https://*.fanboy.co.nz/*`  
`https://filterlists.com/*`  
`https://forums.lanik.us/*`  
`https://github.com/*`  
`https://*.github.io/`  
`https://*.letsblock.it/*` - New in [1.41.7b0](https://github.com/gorhill/uBlock/commit/26048a11bcd002cafc4b2b2fdcb709115a2e07e4).