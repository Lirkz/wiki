TL;DR: Do **not** rely on the number shown over an extension badge to judge blocking power to assess how well your privacy is protected. Doing so would fool you big time.

***

For both Adblock Plus (ABP) and uBlock Origin (uBO) (and many other such extensions), the badge on the icon reports the number of net requests blocked by the extension.

Sometimes one extension can report more stuff blocked than the other on the same page, while the reality could be the opposite.

The fewer the extension blocks, the higher the number of network requests. The higher the number of these, the more likely some will need to be blocked. Occasionally you end up with more network requests blocked, as shown by the badge, while internally, additional network requests were allowed for the web page.

For me, it's ultimately the [benchmarks I run](uBlock-and-others%3A-Blocking-ads%2C-trackers%2C-malwares) to report blocking power that tells the real story. The badge is not a good way to assess the blocking ability of an extension, as you could conclude the opposite of what is happening.

If you don't want to run a benchmark, I have this [little online tool](http://raymondhill.net/httpsb/har-parser.html) with which you can find out the requests which were **not** prevented from leaving your browser. Use it by opening the dev console for the page you want a report from and going to the _Network_ tab. **Edit:** since then, I have created [uBO-Scope](https://github.com/gorhill/uBO-Scope), an extension whose purpose is to inform you about what was not blocked.

Clear the browser cache by right-clicking somewhere in the _Network_ tab console. Force a reload of the web page. Right-click in the _Network_ tab console and select _"Copy all as HAR"_. Paste the result in the text area on [this online tool](http://raymondhill.net/httpsb/har-parser.html), and click _Parse_. It will show the hostnames that were hit by the browser for the particular page you loaded.

For example, for the front page of <https://www.cnet.com/>, **uBO shows ten requests blocked**, while **ABP shows sixteen requests blocked** (both have a lot of filter lists). Here is what happened internally:

Remote servers reached:

ABP
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com
- 1ab45d4854fe036a37ff-6643978b1699ef52a80b7f45a7bcfe3d.r85.cf2.rackcdn.com
- www.googletagservices.com
- zor.livefyre.com
- platform.twitter.com
- s.yimg.com
- dw.cbsimg.net
- geo.query.yahoo.com

uBO:
- dw.cbsi.com
- cnet3.cbsistatic.com
- cnet4.cbsistatic.com
- fonts.cnet.com
- urs.cnet.com
- www.cnet.com

uBO caused the browser to hit far fewer remote servers. Meaning it blocked more, yet its badge displayed a lower number of requests blocked.

So the point is, do not rely on the badge to judge blocking power to assess how well your privacy is protected. Doing so would fool you big time.

On the other hand, blocking too much may "break" some aspects of a website, so in the end, as long as you understand what is happening under the hood, you can make informed choices.