I've seen a couple of instances of people claiming uBlock Origin (uBO) is not as memory efficient as claimed. Examples:

- ["I just installed it, and it uses 117MB - that's not even close"](https://www.reddit.com/r/chrome/comments/2cpogs/fast_and_light_ad_blocker_for_chrome_%C2%B5block/cjhutwz/)
- ["Simply tried, did not see where the province of memory" (Google translate...)](https://bbs.kafan.cn/thread-1762885-1-1.html#pid32323303)

When uBO launches, it loads all selected filter lists, parses the content, eliminates duplicates, then instantiates the filters using efficient internal representation. This parsing of the filter lists requires a good amount of temporary memory.

So if you look at the task manager **right after** uBO has loaded and parsed the filter lists, you will still see uBO's memory footprint due to the loading of all the filter lists. Still, at this point, all this temporary memory has been relinquished to the browser, but the browser hasn't yet collected the freed memory to make it available for reuse.

If the browser is idle enough, before one minute has elapsed<sup>[1]</sup>, the browser should be able to [garbage collect](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)) the temporary memory which was freed by uBO after it finished loading and parsing the filter lists:

![uBO's memory footprint](https://github.com/gorhill/uBlock/raw/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/img/mem-footprint-at-launch-time.png)

The top image shows the memory footprint of uBO right after launch (Chrome 64-bit) (expect a similar memory footprint each time the filter lists get reloaded). The image at the bottom shows the memory footprint of uBO before one minute has elapsed while the browser is idle.

Note that uBO's baseline memory footprint won't change that much afterward. It will likely settle a few MB above the memory footprint reached after garbage collection has occurred, whenever the garbage collector is permitted to do its job.

When reloading all filters (after changing the selection of filter lists, for example), I notice uBO's baseline memory footprint edges higher each time. I entered [an issue](https://github.com/gorhill/uBlock/issues/22) to remind myself to investigate whether there is anything to be done for this. Currently, I think the cause is cumulative memory fragmentation, and there might not be anything to be done. Typically I expect users will select a set of lists and stick to that afterward, so this would make this particular issue irrelevant.

***

[1] In the latest release of Chromium (40+), I have noticed that the garbage collector can be "lazy" (meaning sometimes it takes a while before freed memory is garbage collected). When surveying memory usage, it is essential to **force** a garbage collection cycle using the dev console of the extension itself.