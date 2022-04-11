Doing more with less is a virtue in software. For users of uBlock Origin (uBO), this means:

- Less CPU churn when loading a web page may translate into a noticeable faster page load.
- Higher memory consumption correlates with higher CPU-cycle consumption. Any extra memory used is the same that needs to get allocated/written to/read from (at least once)/garbage collected.
- Free to use more filter lists:
    - For instance, [ABP warns against using too many filter lists](https://adblockplus.org/en/getting_started#subscription): _"It is important to note that you should not add too many filter lists to Adblock Plus"_
- Longer battery life. Each time unit, however small, that the CPU is idle rather than churning translates into extended battery life.
- Free to use a blocker on less powerful devices
    - For instance: [Reddit: _"ABP was a significant burden on my CPU"_](https://www.reddit.com/r/chromeos/comments/298jh1/just_a_tip_try_out_%C2%B5block_for_your_adblocking/)
- Free to add more functional features
- Free to use more extensions

Memory and CPU cycles are finite resources. A sure way for a developer to **not** get hired when being interviewed is to dismiss efficiency work because "memory is plentiful" or "CPU nowadays are fast enough".

***

> "Come on people, we are buying our hardware precisely for this - to be used" [[source](https://news.ycombinator.com/item?id=8803595)]

_Wasting_ is not _using_.

***

Not convinced yet? Try using a stopwatch to compare how fast web pages load when using one blocker compared to another.

If you have a multi-core CPU with plenty of spare CPU cycles, you may not notice a difference in page load. Other popular blockers will use any available CPU cycles (see below) to perform the same job as uBO.

CPU overhead<br>
![CPU overhead](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/cpu-usage-overall-chart-20141226.png)

Memory footprint<br>
![Memory overhead](https://raw.githubusercontent.com/gorhill/uBlock/master/doc/benchmarks/mem-usage-overall-chart-20141224.png)