- Back to [Wiki home](./)
- Back to [Dashboard](./Dashboard)

***

The _Trusted sites_ pane lists all the _trusted site directives_. The purpose of a trusted site directive is to tell on which page uBlock Origin ("uBO") should disable itself completely. When uBO is disabled on a page, there will be no filtering applied to that page.

When uBO is disabled for a site, its toolbar icon will be grayed, and the large blue "power" button in the popup panel is dimmed.

When you visit a web page, uBO will try to match the URL of the page in the address bar against the existing trusted site directives. When there is a match, uBO will be disabled for that page.

The easiest way to create a trusted site directive is by toggling the large "power" button in uBO's popup panel -- this will cause a site-wide trusted site directive for the current site to be automatically created and added to the _Trusted sites_ pane.

The _Trusted sites_ pane allows you to review or edit the exisiting trusted site directives, or to manually add new ones.

### Important: read carefully

There are predefined trusted site directives when you first install uBO:

    about-scheme
    chrome-extension-scheme
    chrome-scheme
    edge-scheme
    moz-extension-scheme
    opera-scheme
    vivaldi-scheme
    wyciwyg-scheme

For Firefox Legacy platform, `behind-the-scene` is also in this predefined trusted sites list.

You should not remove these predefined trusted site directives, unless you know _exactly_ the consequences of doing so.

Removing the predefined trusted site directives without understanding the consequences could cause your browser to malfunction. **This is especially true for the `behind-the-scene` trusted site directive on Firefox Legacy platform.**

If despite this warning you still want to remove one or more of the predefined trusted site directives, I strongly suggest to comment out an entry rather than outright delete it. To comment out an entry, just prefix it with `# `. This way you do not have to remember which predefined trusted site directive you removed, it will be just a matter of removing the `# ` prefix if ever you want to restore an entry. After [1.19.3b7 ](https://github.com/gorhill/uBlock/commit/f7bbc807176fa93680fdaf8b713593a43a3df2a5) removed _predefined trusted site directives_ are commented out automatically.

### Trusted sites directive syntax

Further details about the supported syntax for trusted site directives can be found at ["How to mark a web site as trusted"](./How-to-mark-a-web-site-as-trusted).
