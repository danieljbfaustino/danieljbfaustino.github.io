---
tags: nextjs routing redirect rewrite
---

After helping a client move a website to a different CMS, focus was also put on SEO. Which, between other things, meant that some pages on the old CMS ended up having different URLs. This required the setup of a bunch of redirects.

Using NextJs, that meant setting [redirects](https://nextjs.org/docs/app/api-reference/config/next-config-js/redirects) in the configuration file for each page with content that was reproduced in the new setup.

However, this won't work for pages where the only difference in URL is in the casing. With NextJs (at least up to v15.1.5):
- Routing is case-sensitive.
- Redirects are case-insensitive.

For example, if a page in the old setup had a slug of `Page-with-content`, and in the new setup the slug is `page-with-content`, then a redirect won't work, making you end up with a 310 (Too Many Redirects).

One simple way to solve this is to use [rewrites](https://nextjs.org/docs/app/api-reference/config/next-config-js/rewrites). For example:

```js
rewrites: async () => [
    {
        source: "/Page-with-content",
        destination: "/page-with-content",
    },
],
```

Resources:
1. Discussion on NextJs' repo: <https://github.com/vercel/next.js/discussions/48043>