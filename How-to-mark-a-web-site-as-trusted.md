- Back to [[Wiki home|Home]]
- Back to [Dashboard](./Dashboard)
- Back to [Trusted sites pane](./Dashboard:-Trusted-sites)

***
 - [Big power button](#click-the-big-power-button)
 - [Detailed syntax](#detailed-syntax)
    - [Plain hostname](#plain-hostname)
    - [Single web page](#single-web-page)
    - [Section of a web site](#section-of-a-web-site)
    - [Specific pattern](#specific-pattern)
    - [Regular expression](#regular-expression)
 - [Disable filtering on YouTube channel](#disable-filtering-on-youtube-channel)
 - [Disabling filtering by default (blocklist mode)](#disabling-filtering-by-default)
 - [Other details](#other-details)

***

### Click the big power button
It serves to turn off blocking **on the current website** (will add current site to _Trusted sites_ list), and its state will be remembered next time you visit the website.

| uBO is enabled | uBO is disabled |
| -------------- | --------------- |
| ![uBO enabled](https://user-images.githubusercontent.com/585534/89903803-1caf4200-dbb6-11ea-95b2-16a807781de0.png) | ![uBO disabled](https://user-images.githubusercontent.com/585534/89904193-9fd09800-dbb6-11ea-9b29-db2506fe577f.png) |


### Detailed syntax

All trusted site directives are matched against the URL address of web pages.

As of version uBlock Origin (uBO) 0.8.2.0, the trusted site directive syntax is split into three classes:
- Plain
- Complex
- Comment

Plain syntax is when using only hostname label(s), which means only the hostname portion of a URL will be taken into account.  With plain syntax, the matching is performed by comparing the right-most portion of the page hostname with the trusted site directive.  Wildcards are not allowed when using plain syntax.

Complex syntax occurs if and only if at least one `/` appears in a trusted site directive.  Optionally, the wildcard `*` can be used with complex directives for more flexibility.

A comment is a line prefixed with `#`.  Comments are ignored by uBO.

If no `/` appears in a trusted site directive, and if the directive contains characters which are not allowed for a plain hostname, then the trusted site directive will be commented out and ignored by uBO.  This allows you to fix your directive.

#### Plain hostname

- `example.com`: matches on all pages from `example.com` or above (i.e. `example.com`, `www.example.com`).
- `www.example.org`: matches on all pages from `www.example.org` or above (i.e. `www.example.org`, `forums.www.example.org`, but not `example.org`).
- `org`: matches on all pages from TLD `org` (i.e. `example.org`, `wikipedia.org`).

#### Single web page

- `https://www.twitch.tv/letofski`: matches on only this one page, i.e. when the URL in the address bar **matches exactly** `https://www.twitch.tv/letofski`.

#### Section of a web site

 - `https://www.twitch.tv/letofski*`: matches on this one page, and everything underneath, i.e. when the URL in the address bar **starts exactly** with `https://www.twitch.tv/letofski`.

#### Specific pattern

- `*reddit.com/r/privacy/*`

Wildcards can be used at any position. However, when a wildcard is used within the hostname portion of a directive, it cannot be at the end of the hostname, and also must be at the boundary of a hostname label.

#### Regular expression

- `/^https?://192\.168\.0\.\d+//`
- `/^https://[0-9a-z-]+//`

When you are facing a case where no other directive syntax work, you may use a regular expression ("regex") as a last resort solution. When a trusted site directive starts and ends with a forward slash (`/`), uBO will treat the directive as a regex-based one.

Given that trusted site directives dictate where uBO should be completely disabled, be very careful with regex-based directives, you could easily mistakenly cause uBO to be disabled on more sites than you intended. Typically, only advanced users will resort to regex-based directives, and only for cases where no other syntax can do the job.

### Disable filtering on YouTube channel

There are two ways to do this:

1. By [browser extension](https://github.com/x0a/YouTube-Channel-Whitelist-for-uBlock-Origin#youtube-channel-whitelist-for-ublock-origin).

	Kept updated, should be easy to use, point and click, with good description of usage.
2. Using one of the [user scripts from Greasy Fork](https://greasyfork.org/en/scripts?q=YouTube+whitelist+channels+in+uBlock+Origin&sort=updated) based on [YouTube - whitelist channels in uBlock Origin](https://greasyfork.org/en/scripts/13226-youtube-whitelist-channels-in-ublock-origin).

	Simple, with clearly visible code, but can be outdated. Someone posted instructions on Reddit, it was years ago, but explains few things: ["Any way to whitelist certain youtube channels?"](https://www.reddit.com/r/ublock/comments/4x4jol/any_way_to_whitelist_certain_youtube_channels/).

**Warning!** These are third party tools, I can't vouch for them, you will have to find out for yourself whether they work.

### Disabling filtering by default

Not supported.

Blocklist mode can be achieved by specifically crafted Regular Expression trusted site directive:

    /^((?!example\.com|different\.example\.net|another\.example\.org).)*$/

With this directive all domains separated by `|` characters will be treated as _blocklisted_, and uBO will be enabled only on these pages.

### Other details

If you re-enable uBO by clicking the big power button in the popup while a trusted site directive you handcrafted is in effect, your handcrafted directive will simply be commented out. This way you can bring it back to life if ever you clicked the button by mistake.
