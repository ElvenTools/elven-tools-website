---
layout: "docs"
title: "Dapp deployment"
publicationDate: '2022-04-18'
tags:
  - minter dapp
excerpt: "Elven Tools Dapp walkthrough on deploying the app using Netlify and Vercel."
ogTitle: "Elven Tools Dapp deployment - Elrond custom NextJS Dapp"
ogDescription: "Elven Tools Dapp walkthrough on deploying the app using Netlify and Vercel."
ogUrl: "https://www.elven.tools/docs/dapp-deployment.html"
twitterTitle: "Elven Tools Dapp deployment - Elrond custom NextJS Dapp"
twitterDescription: Elven Tools Dapp walkthrough on deploying the app using Netlify and Vercel."
twitterUrl: "https://www.elven.tools/docs/dapp-deployment.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/dapp-deployment.md"
---

Let's look at the two most convenient and popular hosting providers out there. They are not only rich in features but also have an outstanding developer experience.

### Netlify deployment

The [Netlify](https://www.netlify.com/) services are powerful because of two core things:

1. Cloud systems possibilities.
2. Excellent development experience.

At first sight, It looks like Netlify is suitable only for static and simple websites, but it is so wrong to claim that. I will tell you why in the context of [NextJS](https://nextjs.org/) support on which our Elven Tools Dapp is built.

Because NextJS is a full-stack framework, there is always a little more work to make the best custom setup. If you don't know what you are doing or want to have the best options right away, Netlify will be an excellent choice.

They built a lot of tools and ready-to-use configurations. Let's see what Ntlify can do in the context of NextJS:

1. It discovers that you use NextJS and installs required plugins and configuration.
2. It supports [Incremental Static Regeneration](https://nextjs.org/docs/basic-features/data-fetching/incremental-static-regeneration) (ISR).
3. It supports NextJS [Middlewares](https://nextjs.org/docs/api-routes/api-middlewares).
4. It supports Page routing and [NextJS API](https://nextjs.org/docs/api-routes/introduction) out of the box.
5. It supports [image optimization](https://nextjs.org/docs/basic-features/image-optimization) ([next/image](https://nextjs.org/docs/api-reference/next/image#required-props)).
6. It has docs pages, especially for NextJS. See it [here](https://www.netlify.com/with/nextjs/).
7. It supports SSL by default.

How is it possible? 

Netlify services uses special NextJS [build plugin](https://github.com/netlify/netlify-plugin-nextjs). Don't worry. If you build on Netlify, you don't have to install it. It will be handled automatically.

Ok, but what you should do to prepare the Elven Tools Dapp for the deployment. Let's go through the steps. Let's assume that you've cloned the repository and provided changes. Then, when you need to deploy, you can follow these steps: You will also be able to see the walkthrough video below.

1. Create a new project in the Netlify admin panel.
2. You will do this by connecting to the GitHub repository.
3. The only configuration you would need to provide is the environment variables (see it in the video).
4. By default, all code pushed to the 'main' branch will trigger the Netlify deployment.
5. Netlify creates the random domain name, but you can change it or/and you can connect your custom one.

For more details on deploying a NextJS app, check the [official docs](https://docs.netlify.com/). And for this specific case, please watch the walkthrough video below:

Be aware that there were changes in the env vars list, the video is older, you will always find actual list in the `.env.example` file
<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/SQN-0XMxibU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Vercel deployment (TODO)

Soon there will also be some more information about how to deploy it using [Vercel](https://vercel.com/). Stay tuned!
