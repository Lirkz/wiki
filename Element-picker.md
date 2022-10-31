The element picker can permanently remove elements on a web page by using it to create a network or cosmetic filter. The [[element zapper]] can temporarily remove elements on a web page without creating new filters.

Open the extension's popup menu and click the small "eye-dropper" icon to enter the interactive element picker mode.

![eye dropper highlighted in row of tool buttons](https://user-images.githubusercontent.com/886325/95906120-fd8d8600-0d99-11eb-9a91-84585e4c5739.png)

![Element picker](https://user-images.githubusercontent.com/95879668/198896994-ea330f62-45e3-4f7a-83fe-f226abcbdfcf.png)

### Once in element-picker mode:

Point and click on the element you wish to remove.

After clicking on the element, a modal dialog box will appear, allowing you to select and optionally edit and create a filter to remove it.

**Tip:** You can conveniently move the element picker dialog box out of the way by using the mouse to click and drag on the empty space between the _Preview_ and _Create_ buttons.

![Empty Space To Move Dialog Box](https://user-images.githubusercontent.com/95879668/198899349-6eb4a1a4-e5df-404d-b60a-485113ab3ddc.png)

If possible, one or more network filters may get suggested, as well as a list of cosmetic filters. When you click on one of the filters, you will see what effect it will have on the web page. Also, ensure the selected filter will not remove any additional elements on the page meant to stay.

When you select a cosmetic filter, two sliders will appear that let you further adjust the suggested filter.

The slider on the left-hand side is to adjust the depth of the elements to target. For example, filters with lower depth typically remove large areas of the web page.

The slider on the right-hand side is to adjust the specificity of the filter to create. For example, higher specificity tends to cause fewer elements to be filtered (down to a single one), while lower specificity tends to cause more to be filtered.

Adjust as needed to pick the filter that best matches what you wish to accomplish. ([Demo Video](https://www.youtube.com/watch?v=8TvCGWwQr5o))

You may manually edit the filter, but the result needs to be valid and match at least one element on the web page, or you will not be allowed to create a filter.

You may quit the interactive element picker mode by clicking the _Quit_ button (or pressing the _Esc_ key). You may close the modal dialog and pick an element again by clicking the _Pick_ button.

To enable the _Create_ button, you must first create a proper filter in the text area. Once you click the _Create_ button, the element picker will add the necessary tokens to ensure that the filter **only** applies to the current website and save it to your custom list.

### On touch screen devices:

- Swipe right to exit element picker mode.
- When the dialog is visible, swiping right will hide the element picker dialog (this will make it dimmed and transparent).
- When the dialog is hidden, swipe right again to exit element picker mode.
- Swipe left to make the dialog visible again.

### Element picker does not work, removed element reappears when you reload the page?

There may be many different reasons for this.

- If this is a network filter, you may need to bypass the browser cache when you reload the page by holding down the <kbd>Shift</kbd> key when you click the reload button.
- The URL or selector for the blocked element contains variable parts that change each time a page is loaded.
    - If this is a network filter, you may need to manually edit the filter to use wildcards for the parts of the URL which are variable.
    - If this is a cosmetic filter, you may have to manually craft a better [CSS selector](https://www.w3.org/TR/selectors/#overview). Sometimes this requires observing the surrounding DOM data.
- Cosmetic filtering is disabled for the site or globally. There are many ways to disable cosmetic filtering:
    - The [per-site cosmetic filtering switch](./Per-site-switches#no-cosmetic-filtering).
    - The option [_"Parse and enforce cosmetic filters"_](./Dashboard:-3rd-party-filters#parse-and-enforce-cosmetic-filters) is unchecked in the [_3rd-party filters_](./Dashboard:-3rd-party-filters) pane in the dashboard.
- You unchecked _My filters_ in the _3rd-party filters_ pane in the dashboard.
- There is a static filter in one of the 3rd-party filter lists that counters your filter.
    - Exception cosmetic filters (`#@#`) cancel cosmetic filters (`##`).
    - Exception filter with [`elemhide`](./Static-filter-syntax#elemhide-1) or [`specifichide`](./Static-filter-syntax#specifichide) option.
-  The site you are trying to use the element picker or element zapper on is unsupported:
    - Unsupported pages: [Privileged Pages](https://github.com/gorhill/uBlock/wiki/Privileged-Pages). Also, see this [related issue](https://github.com/uBlockOrigin/uBlock-issues/issues/512).
    - Unsupported protocol: The element picker and element zapper are restricted to work only on the `http(s)://` protocols. For example, it will not work on the `file:///` protocol, but manually adding cosmetic filters to the My Filters pane is still possible. Related issues: [Issue 1](https://github.com/gorhill/uBlock/issues/1601#issuecomment-215929108) and [Issue 2](https://github.com/gorhill/uBlock/issues/1721#issuecomment-225959408). Related comments: [Comment 1](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964243361), [Comment 2](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964254310), and [Comment 3](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964341350).