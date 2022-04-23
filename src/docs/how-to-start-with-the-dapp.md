---
layout: 'docs'
title: 'How to start with the Dapp'
publicationDate: '2022-04-23'
tags:
  - minter dapp
excerpt: "A quick intro to the Elven Tools Dapp - custom Elrond frontend app. You'll learn how to start using it."
ogTitle: "How to start with the Dapp - Elrond custom NextJS Dapp"
ogDescription: "A quick intro to the Elven Tools Dapp - custom Elrond frontend app. You'll learn how to start using it."
ogUrl: "https://www.elven.tools/docs/how-to-start-with-the-dapp.html"
twitterTitle: "How to start with the Dapp - Elrond custom NextJS Dapp"
twitterDescription: "A quick intro to the Elven Tools Dapp - custom Elrond frontend app. You'll learn how to start using it."
twitterUrl: "https://www.elven.tools/docs/how-to-start-with-the-dapp.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/how-to-start-with-the-dapp.md"
---

In this section, I'll explain how to start with the Elven Tools Dapp. You will find the repository here: [ElvenTools/elven-tools-dapp](https://github.com/ElvenTools/elven-tools-dapp).

There are a couple of steps to run it locally and start working on modifications:

1. Clone/Download the repository code
2. Install npm dependencies
3. Configure basic .env variables
4. Configure smart contract information (optionally other things too).
5. Run the dapp locally
6. Prepare it for deployment

The only essential thing here will be the sufficiently configured Node environment. I recommend using the LTS versions of Node and being careful with permissions on your system. The best is to use the Node version manager. I recommend [NVM](https://github.com/nvm-sh/nvm). Also, the best would be to work on Linux/macOS or Windows with a Linux subsystem.

### Clone/Download the repository code

You can clone the repository using the git command:

```
git clone https://github.com/ElvenTools/elven-tools-dapp.git
```

or you can also download it as a zip file using this URL:

```
https://github.com/ElvenTools/elven-tools-dapp/archive/refs/heads/main.zip
```

You can also download a specific version of it. Check the release and download the source code. For example: [v1.0.1](https://github.com/ElvenTools/elven-tools-dapp/releases/tag/v1.0.1).

### Install npm dependencies

When you have the code, you need to install all npm dependencies. Just run:

```
npm install
```

### Configure basic .env variables

The Elven Tools Dapp uses a .env file for crucial environment variables. These are:

- the chain type (devnet, testnet, mainnet),
- the API endpoint
- the public API proxy endpoint
- the Dapp hostname

You will find the example of such .env file here: [.env.example](https://github.com/ElvenTools/elven-tools-dapp/blob/main/.env.example). It contains the config which will allow running the dapp locally, so you can copy it or change its name to `.env.local`. Not all variables there are public, some of them should be kept secret, so this is why there is included only an example in the repo. You should always keep them in `.env.local` when working. For production, you would need to configure them within your CI pipeline or on the hosting provider side, for example, in Netlify.

Variables with the `NEXT_PUBLIC_` prefix can be read by every user interacting with the dapp. All other variables will be private and not accessible on the frontend, so it is good. For example, here, we can hide the actual API endpoint. 

Read more about env vars in NextJS here: [Environment Variables](https://nextjs.org/docs/basic-features/environment-variables).

### Configure smart contract information

The Elven Tools Dapp is prepared to work with properly configured and deployed Elven Tools Smart Contract. There is an additional configuration for the smart contract to save some API calls and traffic, which is essential in the case of paid third-party API providers. You will find it in the `config` directory [here](https://github.com/ElvenTools/elven-tools-dapp/blob/main/config/nftSmartContract.ts). Each variable is described so that I won't repeat it here. 

Remember that this config should always sync with the smart contract. Otherwise, the Dapp will show incorrect data or stop working. In the future, it will be served as an option. By default, the data will be queried on the smart contract.

In the same directory, there are also other configuration files. All should also be descriptive there. These are mainly UI-based configurations, like the Chakra UI theme configuration or static data for the Dapp. You can review them and change whatever you need.

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