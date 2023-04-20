[[Back to Wiki home|Home]]

***

The toolbar icon of uBlock Origin (uBO) informs you about the state of uBO and what it is doing.

The normal state of uBO is to be enabled and fully ready to filter, which is represented by the usual uBO icon:

![Screenshot from 2023-03-18 11-58-42](https://user-images.githubusercontent.com/585534/226121677-aa0b3547-1e44-4c97-9887-020b2c79ede4.png): 

The toolbar icon badge reports the number of network requests blocked on the current webpage.

---

If you disable uBO for a given site, the toolbar icon will be grayish, which indicates that no filtering will occur:

![Screenshot from 2023-03-29 05-11-31](https://user-images.githubusercontent.com/585534/228486438-e1e9bc56-40cc-4ff0-b97d-53d354bb3252.png)

---

When you launch uBO, it needs to load all settings and filter lists in memory to be able to filter properly. When uBO is not yet ready to filter properly, the toolbar icon will be yellowish:

![Screenshot from 2023-03-18 12-50-34](https://user-images.githubusercontent.com/585534/226121557-0428852b-59a6-4320-ab77-d5ca68a8cdf7.png)

---

A yellowish toolbar icon badge `!` means some network requests were fired by the browser while uBO was not ready to filter properly, potentially leading to ads/trackers/etc. not being filtered in some of the already opened webpages:

![Screenshot from 2023-03-18 12-25-30](https://user-images.githubusercontent.com/585534/226121582-ce77b8ef-be4f-4214-97c9-a11497045cef.png)

---

The yellowish badge `!` will persist once uBO is ready to filter properly, to remind you that the current webpage was not properly filtered:

![Screenshot from 2023-03-18 11-58-36](https://user-images.githubusercontent.com/585534/226121627-27b1ae78-58a0-454a-aa74-658944197096.png)

To address the improper filtering that occurred on a webpage, you can simply force a reload of that webpage, which as a result will bring back the badge to be rendered as expected.

If you do not force a reload of the page, the yellowish badge will time out after ~1 minute, having done its duty of warning you about the incomplete filtering.

#### Important note ####

The sticky yellowish badge once uBO is fully loaded affects only Chromium-based browsers because Chromium lacks the framework to ensure extensions are ready before firing network requests. This is a browser limitation, not an extension issue.

Firefox does not suffer this issue. See [uBlock Origin works best on Firefox / Browser launch](./uBlock-Origin-works-best-on-Firefox#browser-launch).
