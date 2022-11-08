---
layout: 'docs'
title: 'How to start with the Dapp'
publicationDate: '2022-04-23'
tags:
  - minter dapp
excerpt: "A quick intro to the Elven Tools Dapp - custom MultiversX frontend app. You'll learn how to start using it."
ogTitle: "How to start with the Dapp - MultiversX custom NextJS Dapp"
ogDescription: "A quick intro to the Elven Tools Dapp - custom MultiversX frontend app. You'll learn how to start using it."
ogUrl: "https://www.elven.tools/docs/how-to-start-with-the-dapp.html"
twitterTitle: "How to start with the Dapp - MultiversX custom NextJS Dapp"
twitterDescription: "A quick intro to the Elven Tools Dapp - custom MultiversX frontend app. You'll learn how to start using it."
twitterUrl: "https://www.elven.tools/docs/how-to-start-with-the-dapp.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/how-to-start-with-the-dapp.md"
---

In this section, I'll explain how to start with the Elven Tools Dapp. You will find the repository here: [ElvenTools/elven-tools-dapp](https://github.com/ElvenTools/elven-tools-dapp).

There are a couple of steps to run it locally and start working on modifications:

1. Clone/Download the repository code
2. Install npm dependencies
3. Configure basic .env variables
4. Run the dapp locally
5. Prepare it for deployment

The only essential thing here will be the sufficiently configured Node environment. I recommend using the LTS versions of Node and being careful with permissions on your system. The best is to use the Node version manager. I recommend [NVM](https://github.com/nvm-sh/nvm). Also, the best would be to work on Linux/macOS or Windows with a Linux subsystem.

### Clone/Download/Initialize the repository code

There are three ways of getting the Dapp's code:

1. By using Elven Tools CLI (since v1.8.1).
2. By using the git command and cloning the repository.
3. By downloading it as a zip file from the repository.

You can use the `elven-tools init-dapp` command. It will:
- download the code
- install npm dependencies
- copy the .env.example into .env.local (required step in all cases)

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/Erjabk7d0HU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

The other way is to clone the repository using the git command:

```
git clone https://github.com/ElvenTools/elven-tools-dapp.git
```

And finally, you can also download it as a zip file using this URL:

```
https://github.com/ElvenTools/elven-tools-dapp/archive/refs/heads/main.zip
```

You can also download a specific version of it. Check the release and download the source code. For example: [v1.0.1](https://github.com/ElvenTools/elven-tools-dapp/releases/tag/v1.0.1).

### Install npm dependencies

**This step is handled automatically by `elven-tools init-dapp`. Otherwise, you would need to do that manually.**

When you have the code, you need to install all npm dependencies. Just run:

```
npm install
```

### Configure basic .env variables

The `elven-tools init-dapp` command will copy .env.example into .env.local. So you would only need to change the variables. Otherwise, you would need to do that manually.

The Elven Tools Dapp uses a .env file for crucial environment variables. These are:

- the chain type (devnet, testnet, mainnet),
- the Elven Tools smart contract address
- the mint function name
- the mint base gase limit
- the API endpoint
- the public API proxy endpoint
- the Dapp hostname

You will find the example of such .env file here: [.env.example](https://github.com/ElvenTools/elven-tools-dapp/blob/main/.env.example). It contains the config which will allow running the dapp locally, so you can copy it or change its name to `.env.local`. Not all variables there are public, some of them should be kept secret, so this is why there is included only an example in the repo. You should always keep them in `.env.local` when working. For production, you would need to configure them within your CI pipeline or on the hosting provider side, for example, in Netlify.

Variables with the `NEXT_PUBLIC_` prefix can be read by every user interacting with the dapp. All other variables will be private and not accessible on the frontend, so it is good. For example, here, we can hide the actual API endpoint. 

Read more about env vars in NextJS here: [Environment Variables](https://nextjs.org/docs/basic-features/environment-variables).

### Smart Contract configuration

The Dapp will query smart contract for all setup data, like:
- if minting is paused
- if there are drops enabled
- if the allowlist is enabled
- how many tokens were already minted
- what are the tokens limits, also per address

All that information will be automatically loaded, so if you change something using the Elven Tools CLI, for example, configure a drop, it will automatically update the Dapp state (after refresh).

### Other configuration

You will find a few less important configuration settings in the `config` directory, mainly for the UI. All are readable, so there is no need to describe them here. The dapp should work on the devnet with an adequately deployed smart contract even without those settings.

### Run the dapp locally

To run the Dapp locally, you would need to run:

```
npm run dev
```

This will run the Dapp locally under the `http://localhost:3000`.

You can also build it locally and check the production-ready version:

```
npm run build
```

then:
```
npm start
```

### Prepare it for deployment

There will be a more detailed tutorial on deploying the dapp using Vercel and Netlify. But here, what is most important is to be aware that you need to have the proper configuration. Proper chain type, appropriate API endpoints, and proper smart contract configuration. Only then you can properly deploy the dapp.

For example, Netlify allows configuring env vars using the administration panel. Then you will need to configure the branch in the repository from which Netlify will deploy the dapp.

Because it is a NextJS-based app, Netlify will recognize it, and it will use additional plugins to make the deployment as smooth as possible. The process is nice and straightforward—the same for Vercel, the company behind NextJS.

You can, of course, deploy the Dapp using other providers. In the end, it is a NodeJS-based framework. You will find more info about the deployment of the NextJS apps here: [Deployment](https://nextjs.org/docs/deployment).

### What's next?

Check more topics [here](/docs/minter-dapp-introduction.html#more-detailed-docs).