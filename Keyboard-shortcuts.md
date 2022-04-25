## Supported shortcuts

- Activate extension

   Will open uBlock Origin (uBO) popup panel - equivalent of clicking the button on the toolbar

- Enter element picker mode

   Will activate [[Element picker]] that will allow creating new filters

- Enter element zapper mode

   Will activate [[Element zapper]] that will allow to temporarily remove elements from the page

- Open the logger

   Will activate [[The logger]] where you can preview network connection and applied filters

- Open the dashboard

   Will open [[The dashboard|Dashboard]] where you can configure uBO settings

- Relax blocking mode

   Advanced feature, will decrease [[blocking mode]] one step at a time.

   Default sequence:

     - Hard mode + No scripting
     - Medium mode + No scripting
     - Medium mode
     - Default.

   Can be configured in [[Advanced settings#blockingprofiles]]

- Toggle cosmetic filtering

   New in [1.41.7b1](https://github.com/gorhill/uBlock/commit/ad1800fbcaeea30a860871f3179def5c4af1bc45).

   Will toggle [["cosmetic filtering"|Per-site-switches#no-cosmetic-filtering]] (element hiding filters) on/off for current website.

## Accessing shortcut configuration

### Firefox

- Main menu (three bars) in top right corner
- Add-ons
- "Tools for all add-ons" menu in top right corner of the page (gear wheel)
- Manage Extension Shortcuts

![Configuring shortcuts in Firefox](https://user-images.githubusercontent.com/886325/83352569-a9cf5280-a34c-11ea-9e84-9d24c40430ec.gif)

***

In Firefox versions older than 74 shortcut configuration is also available in uBO Dashboard ([v1.26.1b1](https://github.com/gorhill/uBlock/commit/20332c65b4b597d2ba04993fcdcc4ea81dd64fb9)):

![image](https://user-images.githubusercontent.com/886325/64020978-37b6ac80-cb33-11e9-9fee-01a94175c252.png)

A new shortcut option to open popup panel was added in [1.24.0](https://github.com/gorhill/uBlock/commit/e2fdc1b94bee06da77fa45a59395cb7cedfa61ae)

### Chrome

- Main menu (three dots) in top right corner
- More tools
- Extensions
- Extensions menu in top left corner (three bars)
- Keyboard shortcuts

![Configuring shortcuts in Chrome](https://user-images.githubusercontent.com/886325/83352168-11d06980-a34a-11ea-81da-28334a4fa2d7.gif)

