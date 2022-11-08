---
layout: 'docs'
title: 'Minter Dapp introduction'
publicationDate: '2022-04-25'
tags:
  - minter dapp
excerpt: "Fully functional and optimized minter dapp based on the Next framework, integrated with Elven Tools Smart Contract."
ogTitle: "Minter Dapp template - introduction"
ogDescription: "Fully functional and optimized minter dapp based on the Next framework, integrated with Elven Tools Smart Contract."
ogUrl: "https://www.elven.tools/docs/minter-dapp-introduction.html"
twitterTitle: "Minter Dapp template - introduction"
twitterDescription: "Fully functional and optimized minter dapp based on the Next framework, integrated with Elven Tools Smart Contract."
twitterUrl: "https://www.elven.tools/docs/minter-dapp-introduction.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/minter-dapp-introduction.md"
---

Elven Tools Dapp is a template (landing page) with preconfigured logic to be used with the Elven Tools Smart Contract. 

It is a minter dapp based on the [NextJS](https://nextjs.org/) framework, which gives many possibilities for modifications and extending.

- [Elven Tools Dapp repository](https://github.com/ElvenTools/elven-tools-dapp)
- [Elven Tools Dapp live demo](https://dapp-demo.elven.tools/) (you can mint some NFTs on the devnet here!)

You can use it primarily for this particular case, so for minting NFTs based on Elven Tools Smart Contract, you could also use it as a boilerplate for your other projects. You would only need to do some modifications.

Because it is built using the NextJS framework, deployment and hosting with [Vercel](https://vercel.com/) or [Netlify](https://www.netlify.com/) is as simple as pushing the code to the repository. Also, private repository and not only on GitHub. I will be covering both of these later.

Below you'll find the explanation of a couple of choices:

### Why NextJS?

There are a couple of reasons. The most important are:

1. Based on React, which is well known and most popular
2. Offers static sites generation or/and server-side rendering. Very important when it comes to landing pages and SEO.
3. Optimized with the Web Standards in mind. There are many tools for optimizing the assets loading and overall performance.
4. Simple PWA and Service Workers configuration is essential for optimization.
5. A lot of plugins and excellent development experience.

### Why not the dapp-core library?

1. It is too complicated for this purpose.
2. The Dapp should also be helpful as a boilerplate for other projects, so it needs to be simple.
3. There is more control over auth flows with a custom approach. And this is the core of the dapp, so it is critical.
4. It has too many utilities that, for this case, won't be used.

### Why the API endpoint is proxied?

1. Allows hiding the API endpoint under the same domain `www.your-domain.com/api/elrond`.
2. No one will be able to use this endpoint from outside the Dapp.
3. When used with no public API, You can hide the API keys which need to be attached to the endpoint.
4. Usage of the public MultiversX API for production release is always a bad idea in such a dapp, so it seems to be a perfect solution for third-party providers.
5. Anyway, proxied API will still work well with the public MultiversX API.

### Why written with Typescript and not JavaScript only?

1. Typescript becomes the standard for JavaScript projects.
2. Better control over the code.
3. Better control over bugs.
4. Smooth refactoring experience.

### Why not use the Redux for state handling?

1. The Redux is a great tool, but it seems to be an overkill in this case.
2. The Dapp uses [Valtio](https://valtio.pmnd.rs/) for global state management, a small yet powerful tool.

### Why Chakra UI?

1. Intuitive configuration.
2. Excellent approach to the theming.
3. You can use it almost the same as with utility CSS classes.
4. Very flexible. You can write CSS in JS in many ways.
5. A lot of React-specific utilities (Hooks).
6. Integrates well with Next.
7. Built with accessibility in mind.
8. A lot of ready-to-use components.

### Below, you will find a sneak peek video
(here with old approach to configuration, new vid soon)

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/ATSxD3mD4dc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### What's next?
- [How to start with Elven Tools Dapp - step by step](/docs/how-to-start-with-the-dapp.html)

### More detailed docs

- [Dapp structure](/docs/dapp-structure.html) - here, you will learn about the essential components of the Dapp
- [Dapp API proxy](/docs/dapp-api-proxy.html) - here, you will learn how the API proxy and 'guard' middleware works
- [Dapp backend integration](/docs/dapp-backend-integration.html) - here you will learn how to extend your dapp and verify the user on the backend side when needed
- [Dapp deployment](/docs/dapp-deployment.html) - here, you will learn how to deploy the Dapp using Netlify or Vercel
- [Dapp React prebuilt hooks, components, and utilities](/docs/dapp-react-hooks-and-components.html) - here, you will learn about all the custom React hooks and tools which can be used in many different ways
- [Soon...] Quick intro to Chakra UI and NextJS with links - here, you will learn how to modify the Dapp using included tools like Chakra UI and NextJS
- [Soon...] Dapp configuration walkthrough - here, you will learn how to configure the Dapp properly

- Other docs will pop up when needed...
