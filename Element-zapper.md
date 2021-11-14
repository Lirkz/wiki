[[Back to Wiki home|Home]]

***

<sub>Note: to create filters, use the [[element picker]]</sub>

The purpose of the element zapper is to quickly deal with the removal of nuisance elements on a page **without** having to create one or more filters.

![uBO popup interface with "lightning" button highlighted](https://user-images.githubusercontent.com/585534/90419472-9cd91a00-e084-11ea-94ef-91be749a0fdb.png)

Sometimes we visit a page on a site for which we do not intend to become a regular visitor, and many sites nowadays will throw nuisance visual elements preventing you from accessing the content. However oftentimes we would rather not go through the process of creating one or more filters for just that one visit. This is where the element-zapper mode is useful: you can quickly get rid of the nuisance visual element without having to pollute your filter set for this one single visit.

Really, this feature is already supported by all browsers if one care to use the developer tools of the browser, however the purpose of the element-zapper is to make it easy for everybody to use: highlight and click with no need to open the developer tools.

Additionally, depending on what element you are zapping, the element zapper will also try to detect and deal with those pages preventing from scrolling through the whole content.

Once you enter the "element-zapper mode":
- Highlighting then clicking a page element will remove this element from the document and exit element-zapper mode;
    - Press the <kbd>Shift</kbd> key while clicking if you do not want to exit element-zapper mode.
- Highlighting a page element and then pressing the <kbd>Delete</kbd> key will remove the element from the document, without quitting the element-zapper mode;
- Pressing the <kbd>Esc</kbd> key will exit element-zapper mode.

On touch screen devices:
- tap once to select element
- tap highlighted element to remove it
- swipe right to remove incorrect highlighting
- swipe right to exit element-zapper mode

Of course, since no filters are created, all the elements you removed will be back once you reload the page.
