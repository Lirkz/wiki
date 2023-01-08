This page is just a place for me to collect my counterarguments when I spot something which I believe deserves countering.

#### Who cares about efficiency, I have 8 GB

I heard this argument from apologists of bloated software frequently. I decided to give this counterargument a [dedicated page](./Who-cares-about-efficiency,-I-have-8-GB-RAM-and|or-a-quad-core-CPU).

#### Just use a hosts file

uBlock Origin (uBO) supports the parsing/enforcing of hosts files and ships with a couple. One of them, _"Peter Lowe’s Ad server list"_, is enabled by default.

Using a hosts file at the OS level rather than the uBO level is the better solution for lists of malware domains since these malware-linked domains would be blocked system-wide, and all applications would benefit from it.

However, for lists of domains linked to ad servers, trackers, analytics, etc., this is not a good solution: **You can not easily un-break web pages with a [hosts file](https://en.wikipedia.org/wiki/Hosts_(file)) at OS level.**

With the hosts file under the control of uBO, it is possible to un-break websites. A user can disable uBO for the website that breaks or create an exception filter to counter the blocking of a specific hostname appearing in a hosts file.

Many of the exception filters in [_"uBlock filters"_](https://github.com/gorhill/uBlock/blob/master/assets/ublock/filters.txt) are exception filters to counter entries in the hosts files shipped with uBO.

I want the project to be committed to fully supporting the hosts files that ship with uBO. Report any issues from using these, and the appropriate exception filters will get created.

I use all of these hosts files, and so far, not much breakage has occurred.

#### uBO is a fork of Adblock Plus (ABP) code

No. The code is wholly original and written from scratch. There are very few places I borrowed code from elsewhere, and these have identification. For example, for the element picker, I embedded [CSS.escape](https://github.com/mathiasbynens/CSS.escape) from Mathias Bynens (because Chromium did not at the time support [CSS.escape](https://developer.mozilla.org/en-US/docs/Web/API/CSS/escape)).

#### Adblock Edge is as light as uBO

No, it is not. Adblock Edge is like ABP but without the _"Acceptable ads"_ exception filters out of the box. See for yourself: [here](https://web.archive.org/web/20150425084356/https://bitbucket.org/adstomper/adblockedge/diff/lib/filterClasses.js?diff1=f89367e6ddc7&diff2=a642b932365d9521042cf8fec56089caca496a7d&at=default) [via archive.org] is a diff of a code change for Adblock Edge, and [here](https://github.com/adblockplus/adblockplus/commit/384cb64c6d3c2aa698b5f15c9d8aaefd22c889aa#diff-3) is the same exact diff for ABP. The timestamps show that Adblock Edge pulled code changes from the ABP project.