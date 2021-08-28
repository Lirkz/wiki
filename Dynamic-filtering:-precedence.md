[Back to "Dynamic-filtering"](./Dynamic-filtering)

***

First: Trusted site directives override both dynamic filtering _and_ static filtering. Trusted site directives appear in the [_Trusted sites_ pane in the dashboard](./How-to-mark-a-web-site-as-trusted), and they are used to completely disable filtering. The [big blue button in the popup UI](./Quick-guide:-popup-user-interface#the-large-power-button) is used to easily add current site/page to the _Trusted sites_ list.

***

Dynamic `allow`/`block` rules override static filtering rules.
- Use `allow` to force requests to be allowed regardless of whether they would normally be blocked by static filtering.
    - Useful to fix sites broken by false positives in _EasyList_, _EasyPrivacy_ (or any other static filter lists).
- Use `block` to force requests to be blocked regardless of whether they would normally be allowed by static filtering.
    - Useful to block with 100% certainty, to bypass exception filters with which you may disagree in _EasyList_, _EasyPrivacy_ (or any other static filter lists).

There is a precedence logic for dynamic filtering cells. In general, narrower rules override broader ones; ties are broken first by destination domain, then by request type. From highest to lowest precedence, we have:

| Precedence rule | Example |
|---|---|
| More qualified destination domains take precedence over less qualified ones | `* www.dest.com * block` overrides `* dest.com * noop` |
| Specific destination domains take precedence over specific request types | `* dest.com * noop` overrides `* * 3p-script block` |
| Party-and-content types take precedence over party types |`* * 3p-script block` overrides `* * 3p noop` |
| Party types take precedence over content types | `* * 3p noop` overrides `* * image block` |
| Specific request types take precedence over specific source domains | `* * image block` overrides `source.com * * noop` |
| More qualified source domains take precedence over less qualified ones | `www.source.com * * noop` overrides `source.com * * block` |
| Specific source domains take precedence over universal rules | `source.com * * block` overrides `* * * noop` |

The UI is designed in such way that the precedence logic should hopefully become clear with usage. Lower rows in the grid of cells always take precedence over higher rows, and a cell in the right column takes precedence over the cell to its left. Rules in the left column (global, all source domains) "bleed" to the right (local, this particular source domain) when there's not a specific rule in the right column.