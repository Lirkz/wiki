This page is just a place for me to keep track of contributed memory to web pages over time. I consider the contributed memory to web pages to be more important than the own memory footprint. Unfortunately, a user can not see how much memory overhead an extension contributes to a web page without running a benchmark like the one here. Keep in mind the results here are only for **one basic web page.**

Using [Acid Test 3](http://acid3.acidtests.org/), a simple web page with embedded `iframes`, the web page opened in a new tab for each extension after a browser restart.

Each extension was tested alone, with no other extensions enabled. Leaving the browser idle for more than 1 minute ensured that the web page memory was garbage collected.

Added the following steps for benchmarks dated December 2014 and later:

1. Click _"Stats for nerds"_ in _"Task Manager"_: _"About memory"_ opens.
2. Wait a few seconds.
3. Close the _"About memory"_ tab.
4. Wait a few seconds.
5. Repeat all the above steps until the memory footprint of the Acid Test tab stops decreasing.

I found that this was now necessary as it appears the Chromium garbage collector has become rather lazy. The above steps force it into action.

### 24 December 2014

- Chromium 39.0.2171.65 64-bit (Linux)
- uBlock Origin (uBO) 0.8.2.2 (default lists: _EasyList_, _Peter Lowe’s Ad server_, _EasyPrivacy_, malware domain lists, _Fanboy’s Social Blocking List‎_)
- Adblock Plus (ABP) 1.8.8 (_EasyList_, _EasyPrivacy_, _Malware Protection List_, _"Acceptable ads"_ disabled)

Summary of results:
- Reference memory usage for the web page: 23 MB
- uBO adds over 10 MB
- ABP adds over 33 MB
- ABP with the same filter lists as uBO adds over 46 MB

No extension (reference):<br>
![no extension](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20141224-none.png)

uBO:<br>
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20141224-ublock.png)

ABP:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20141224-abp.png)

ABP with same filter lists as uBO:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20141224-abp-more.png)

### 19 September 2014

- Chromium 37.0.2062.94 64-bit (Linux)
- uBO 0.6.2.1 (default filter lists)
- ABP 1.8.5 (_EasyList_, _EasyPrivacy_, _Malware Protection List_, _"Acceptable ads"_ disabled)

Summary of results:
- Reference memory usage for the web page: 22 MB
- uBO Plus adds over 9 MB
- ABP adds over 32 MB

No extension (reference):<br>
![no extension](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20140919-none.png)

uBO:<br>
![uBlock](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20140919-ublock.png)

ABP:<br>
![Adblock Plus](https://raw.githubusercontent.com/gorhill/uBlock/6c046ed95cd02d023453c66f766159f6410ae7f7/doc/benchmarks/mem-usage-in-page-20140919-abp.png)

Observations:

The last time I ran this benchmark [was on Chromium 34 64-bit](./%C2%B5Block-vs.-ABP:-efficiency-compared#added-memory-footprint-to-web-pages), and it does appear that Chromium 37 is causing web pages to consume more memory. The reference result went from ~17 MB to ~22 MB.
