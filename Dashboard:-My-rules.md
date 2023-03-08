- [[Back to Wiki home|Home]]
    - [Dynamic filtering](./Dynamic-filtering)
        - [Quick guide](./Dynamic-filtering:-quick-guide)
        - [Rule syntax](./Dynamic-filtering:-rule-syntax)
        - [Rule precedence](./Dynamic-filtering:-precedence)
        - [Blocking mode](./Blocking-mode)
    - [URL filtering](./Dynamic-URL-filtering)

***

![My rules pane](https://user-images.githubusercontent.com/886325/64913787-ea4b5980-d746-11e9-9428-5910c77c8b0a.png)

### Default ruleset

The default ruleset when uBO is freshly installed:

```
no-large-media: behind-the-scene false
behind-the-scene * * noop
behind-the-scene * image noop
behind-the-scene * 3p noop
behind-the-scene * inline-script noop
behind-the-scene * 1p-script noop
behind-the-scene * 3p-script noop
behind-the-scene * 3p-frame noop
```

Additionally, Firefox has also the following rule:

```
no-csp-reports: * true
```
