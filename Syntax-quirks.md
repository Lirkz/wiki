See also: [Filter performance](./Filter-performance)

- Filters match on word boundaries unless explicitly wildcarded
    - See <https://github.com/uBlockOrigin/uBlock-issues/issues/954#issuecomment-602041890>
- Looking-like-domain filters match only in [host part of URL](https://en.wikipedia.org/wiki/URL#Syntax)
    - See [HOSTS optimization](./Static-filter-syntax#hosts-files)
- Negated domains in cosmetic filters work like exception (In ABP generic blocking filter overrides filter with negated domain).
    - See <https://github.com/uBlockOrigin/uBlock-issues/issues/388>
- One filter can be counted as many, [example](./Static-filter-syntax#badfilter)
- `$document` works only as [blocking filter](./Static-filter-syntax#document-for-entire-page-exception)
- Generic cosmetic filters don't work in [Shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)
    - See <https://github.com/uBlockOrigin/uBlock-issues/issues/803>
- Popup filters will not close pages opened by direct user action when the page'S URL matches the link clicked
    - See <https://github.com/uBlockOrigin/uBlock-issues/issues/774>
- Domain filter in uBO matches [_fully qualified domain name_](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) (FQDN, these with dot at the end), where in ABP match is exact.
    - See <https://github.com/uBlockOrigin/uAssets/issues/7619>
- Simple generic cosmetic filters no longer hide `<body>` element after uBO v1.37.3b15
    - See <https://github.com/uBlockOrigin/uBlock-issues/issues/1692>