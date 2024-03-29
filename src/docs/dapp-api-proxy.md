---
layout: "docs"
title: "Dapp API proxy"
publicationDate: "2022-04-19"
tags:
  - minter dapp
excerpt: "The Elven Tools Dapp API proxy - how the API proxy and 'guard' middleware works."
ogTitle: "Elven Tools Dapp API proxy - MultiversX custom NextJS Dapp"
ogDescription: "The Elven Tools Dapp API proxy - you will learn how the API proxy and 'guard' middleware works."
ogUrl: "https://www.elven.tools/docs/dapp-api-proxy.html"
twitterTitle: "Elven Tools Dapp API proxy - MultiversX custom NextJS Dapp"
twitterDescription: "The Elven Tools Dapp API proxy - you will learn how the API proxy and 'guard' middleware works."
twitterUrl: "https://www.elven.tools/docs/dapp-api-proxy.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/dapp-api-proxy.md"
---

Think of the Dapp API proxy as the Nextjs API rewrites on the backend side. Why is it even included? Because it helps to hide your actual API endpoint. A lot of the dapps use the public API endpoints. If you want to do that, this article won't be helpful for you. On the other hand, if you want to use a third-party service or your architecture, it might be worth reading more about it.

### How it works by default

By default, the Dapp provides the `.env.example`, configured not to use the API rewrites and configured to use the official public MultiversX API endpoint. 

You have three options:

1. By commenting this out the dapp will use the default MultiversX api endpoint (e.g. https://devnet-api.multiversx.com) \
  **Note**: `MULTIVERSX_PRIVATE_API` needs to be removed/commented out.
2. Set this to an absolute address to use a custom MultiversX api endpoint
   (e.g. http://dev.mydomain.com) \
  **Note**: `MULTIVERSX_PRIVATE_API` needs to be removed/commented out.
3. Enter a relative path to proxy/mask your MultiversX api endpoint (e.g. /api/multiversx)
   Only current instance of the Dapp can use it if only `API_ALLOWED_DAPP_HOST` is set.  \
  **Note**: `MULTIVERSX_PRIVATE_API` must include the actual MultiversX API endpoint.

### How the API rewrite works

Reminder, the Elven Tools Dapp code is [here](https://github.com/ElvenTools/elven-tools-dapp).

In the `.env.example` (and later in your proper `.env.local`) file, you will find a variable `MULTIVERSX_PRIVATE_API`. By default, there will be a public MultiversX API endpoint, but this is a place for your custom API endpoint. The endpoint won't be exposed on the frontend. So you can use services such as Tatum or BlastAPI and put there your custom endpoint. This way, you will make it private but still usable by your dapp and only by it.

There is also `NEXT_PUBLIC_MULTIVERSX_API`, which will define the public API proxy. The best is to make it a subset of the `/api`, so by default, it is `/api/multiversx`.

Ok, so far, so good. Your endpoint won't be visible in public. What's next?

In the `nextjs.config.json`, you will find the main rule for the rewrite. It is something like:

```javascript
async rewrites() {
  if (!process.env.MULTIVERSX_PRIVATE_API) {
    return [];
  }
  return [
    {
      source: `${process.env.NEXT_PUBLIC_MULTIVERSX_API}/:path*`,
      destination: `${process.env.MULTIVERSX_CUSTOM_API}/:path*`,
      destination: `${process.env.MULTIVERSX_PRIVATE_API}/:path*`,
    },
  ];
},
```

It is pretty simple. As you can see, we redirect all `/api/multiversx/*` (NEXT_PUBLIC_MULTIVERSX_API) calls to the proper API endpoint. So the only API endpoint that will be visible on the frontend side is `/api/multiversx/*` and all that is provided by your service provider. Sometimes it can be the same functionality as for api.multiversx.com, and sometimes it will be limited to functionality from gateway.multiversx.com. Depends on the `MULTIVERSX_PRIVATE_API` setup.

Ok, now you think my endpoint is proxied and hidden, but it is still public, and anyone can use it, right? Not really. See why.

### Guard middleware

NextJS should block other hosts from accessing its API by default, but our `/api/multiversx/*` endpoint is still accessible using Postman or any other App or CLI tool. So, as an additional check, the Elven Tools Dapp implements optional middleware that checks the `referer` header. It will check if the referer is the same as defined in the `API_ALLOWED_DAPP_HOST` env variable. Otherwise, it will throw the `403 Forbidden`. You can find the middleware in the `/middleware.ts`.

There is one caveat with that approach, if you want to test your API through proxy/rewrite using some third-party tool or even the browser, you won't be able to do that because of the middleware, but don't worry. It is all optional. To disable the guard, it is enough to remove the `API_ALLOWED_DAPP_HOST` from your env vars. Still, remember that the proxied API will be the same as your primary API endpoint, so you can always test everything from outside the dapp using your original API endpoint.

### What's next?

Check more topics [here](/docs/minter-dapp-introduction.html#more-detailed-docs).
