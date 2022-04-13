No: it is significantly less resource-intensive than Adblock Plus (ABP).

Sloppy benchmarks can lead to the myth that uBlock Origin (uBO) is less resource-intensive than ABP.

Rigorous benchmarks demonstrate that uBO is significantly more efficient than ABP.

Examples of sloppiness:

- Using memory footprint figures **before** the browser's garbage collector kicks in
- Not taking measures to avoid tainting memory footprint with [Chromium bug 441500](https://bugs.chromium.org/p/chromium/issues/detail?id=441500)
- Using memory footprint figures while option pages for one of the extensions are open
- Disregarding the [contributed memory footprint to web pages](./Contributed-memory-usage:-benchmarks-over-time)
- Comparing memory footprint after extensions have run for a significantly different amount of time
- Using memory footprint figures after one of the extensions has performed a one-time resource-intensive task (updating filter lists, etc.)
- Not taking into account the number of filters in both extensions
