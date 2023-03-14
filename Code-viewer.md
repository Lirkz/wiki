See:
- https://github.com/uBlockOrigin/uBlock-issues/wiki/The-logger#source-code-viewer
- https://github.com/uBlockOrigin/uBlock-issues/wiki/Advanced-settings#filterauthormode

Investigating filter issues can be a serious time sink, and to help with this, a code viewer has been added to uBO. The code viewer will automatically beautify HTML/CSS/JS code, which should be an improvement over the browser built-in view-source tool.

You can view beautified source code of HTML/CSS/JS resources when clicking the link in a logger entry. Additionally, if the [advanced setting `filterAuthorMode`](https://github.com/gorhill/uBlock/wiki/Advanced-settings#filterauthormode) is set to true, an entry labelled _View source code..._ will be added to the context menu, so that you can view the source code of any page/resource without having to open the logger.