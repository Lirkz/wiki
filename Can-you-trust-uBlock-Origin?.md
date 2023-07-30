After I added the `privacy` permission to make uBlock Origin (uBO) reliable when it comes to blocking network requests, a lot of people questioned uBO's trustworthiness.

First, uBO is completely developed in full public view. All the sources and all the changes to the sources are fully accessible on GitHub.

Second, uBO does not have a dedicated server, it can't "phone home" with your browsing data, there is only GitHub, and GitHub is completely unrelated to uBO.

Third, I have no intent to _ever_ monetize uBO. It started as a personal project, and it still is a personal project. So uBO has absolutely no interest in data mining you.

I think it's time I give examples of how requiring _fewer_ permissions is **not** a sure sign of higher trustworthiness.

#### Web Protector - Reliable Phishing Protection

Chrome store: Web Protector - Reliable Phishing Protection (the extension no longer exists on the Chrome Web Store).

This extension requires the same permission as uBO, _minus_ the `privacy` one. Some might be inclined that it can thus be more trusted than uBO, which requires the `privacy` permission.

However, Web Protector has a home server, and it does "phone home" as opposed to uBO (which has no home server in the first place).

For **every** web page you visit, you can see Web Protector sending behind-the-scene network requests to `webovernet.com`:

![The uBlock Origin logger, showing network requests to webovernet.com every time a website is visited](https://cloud.githubusercontent.com/assets/585534/8253895/fe92dd8c-1661-11e5-9134-5c2b9159a57c.png)

***

This is just to demonstrate that the permissions _alone_ do not tell the whole story. What must be assessed are:

- Is the code developed in **full** view?
- Under which license does the code fall?
- Is there a home server?
- What network requests are made by an extension behind the scene?
    - uBO's logger allows you to see it's own [behind-the-scene network requests](https://github.com/uBlockOrigin/uBlock-issues/wiki/Behind-the-scene-network-requests) (mainly to GitHub, for updating filter lists).
- How is an extension monetizing itself?
    - Learning about this factor will help you best understand whether the extension's developer's interests are aligned or at odds with yours.
