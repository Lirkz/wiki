[Back to Wiki home](./)

***

<sub>Note: To temporarily remove elements without creating new filters, use the [[element zapper]].</sub>

The element picker's purpose is to assist the user in the creation of network or cosmetic filters.

![eye dropper highlighted in row of tool buttons](https://user-images.githubusercontent.com/886325/95906120-fd8d8600-0d99-11eb-9a91-84585e4c5739.png)

If there is an element on a web page you wish to remove forever, open the extension's popup menu, and click the small "eye-dropper" icon. You will enter the interactive element picker mode.

![Element picker](https://user-images.githubusercontent.com/886325/99714989-9359b680-2aa6-11eb-8805-487fca0c8fef.png)

Once in element-picker mode, you have to point and click on the element you wish to remove.

Once you click on the element, you will be presented with a modal dialog box which allows you to select, and optionally edit and create a filter for the element(s) you wish to remove from the web page.


> ***
> **Tip:**
>
> You can easily move the element picker dialog out of the way, using the mouse by clicking and dragging the empty space between the _Preview_ and _Create_ buttons.
> ***

If possible, one or more network filters will be suggested, as well as a list of cosmetic filters. When you click on one of the suggested filters, you will be shown what effect it will have on the page. You may want to ensure the selected filter will not also get rid of useful items on the page.

When you select a cosmetic filter, there will be two sliders appearing to let you further adjust the suggested cosmetic filter.

The slider on the left-hand side is to adjust the depth of the elements to target, i.e. filters with lower depth typically will remove larger areas in the page.

The slider on the right hand-side is to adjust the specificity of the filter to create, i.e. higher specificity tends to cause less elements to be filtered (down to a single one), while lower specificity tends to cause more elements to be filtered.

Adjust as needed in order to pick the filter which best matches what you wish to accomplish (see [demo of this](https://www.youtube.com/watch?v=8TvCGWwQr5o)).

You may manually edit the filter. However the result needs to be a valid filter, otherwise you won't be allowed to create a filter out of it. A valid filter in the context of the element picker is one which matches at least one element on the web page.

You may quit the interactive element picker by clicking the _Quit_ button (or press _Esc_). You may close the modal dialog and go pick an element again by clicking the _Pick_ button.

The _Create_ button will be enabled only if a proper filter can be created from the content of the text area. Once you click the _Create_ button, the element picker will add the necessary tokens to ensure the filter apply **only** to the current web site, will add it to your custom list of filters and save it.

On touch screen devices:
- swipe right to exit element-picker mode
- when dialog is visible, swiping right will hide element-picker dialog (will make it dimmed and transparent)
- when dialog is hidden, swipe right again to exit element-picker mode
- swipe left to make dialog visible again

### Element picker does not work, removed element reappears when you reload the page?

There may be many different reasons for this.

- If this is a network filter you may need to bypass the browser cache when you reload the page -- hold down the <kbd>Shift</kbd> key when you click the reload button.
- The URL or selector for the blocked element has variable part(s) in it, which changes each time a page is loaded.
    - If this is a network filter you may need to manually edit the filter to make use of wildcards for the parts of the URL which are variable.
    - If this is a cosmetic filter, you may have to manually craft a better [CSS selector](https://www.w3.org/TR/selectors/#overview). Sometimes this requires observing the surrounding DOM data.
- Cosmetic filtering is disabled for the site, or globally. There are many ways to disable cosmetic filtering:
    - The [per-site cosmetic filtering switch](./Per-site-switches#no-cosmetic-filtering).
    - The option [_"Parse and enforce cosmetic filters"_](./Dashboard:-3rd-party-filters#parse-and-enforce-cosmetic-filters) is un-checked in the [_3rd-party filters_](./Dashboard:-3rd-party-filters) pane in the dashboard.
- You un-checked _My filters_ in the _3rd-party filters_ pane in the dashboard.
- There is a static filter in one of the 3rd-party filter lists in use which counters your filter.
    - Exception cosmetic filters (`#@#`) cancel cosmetic filters (`##`).
    - Exception filter with [`elemhide`](./Static-filter-syntax#elemhide-1) or [`specifichide`](./Static-filter-syntax#specifichide) option.
-  The site you're trying to use Picker or Zapper on, is unsupported:
    - unsupported pages: [Privileged Pages](https://github.com/gorhill/uBlock/wiki/Privileged-Pages), also see [related issue](https://github.com/uBlockOrigin/uBlock-issues/issues/512)
    - unsupported protocol: Picker and Zapper are restricted to work on protocols `http(s)://` only, which means for example it won't work on `file:///` protocol, however cosmetic filters still can be added manually to My Filters pane, related issues: [issue 1](https://github.com/gorhill/uBlock/issues/1601#issuecomment-215929108), [issue 2](https://github.com/gorhill/uBlock/issues/1721#issuecomment-225959408), related comments: [comment 1](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964243361), [comment 2](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964254310), [comment 3](https://github.com/DandelionSprout/adfilt/issues/63#issuecomment-964341350)
