---
layout: 'docs'
title: 'Dapp structure'
publicationDate: '2022-04-21'
tags:
  - minter dapp
excerpt: "The Elven Tools Dapp files structure and logic behind all crucial parts."
ogTitle: "Elven Tools Dapp structure - MultiversX custom NextJS Dapp"
ogDescription: "The Elven Tools Dapp files structure and logic behind all crucial parts."
ogUrl: "https://www.elven.tools/docs/dapp-structure.html"
twitterTitle: "Elven Tools Dapp structure - MultiversX custom NextJS Dapp"
twitterDescription: "The Elven Tools Dapp files structure and logic behind all crucial parts."
twitterUrl: "https://www.elven.tools/docs/dapp-structure.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/dapp-structure.md"
---

Here you will find a description of all crucial parts of the Dapp and how all is structured. Besides that, you'll find more detailed descriptions of each piece in other sections.

Remember that the Dapp is built with the NextJS framework. It is good to know at least the basics of it. But don't worry, you should also be good after reading these docs assuming that you know how to work with React.

### Main sections of the codebase:

1. Global state
2. Dapp required configuration
3. React custom hooks
4. NextJS pages + api configuration
5. React custom UI components

### Global state

The Dapp does not include the [sdk-dapp](https://github.com/multiversx/mx-sdk-dapp) library, it handles all using only [sdk-core](https://github.com/multiversx/mx-sdk-js-core), so it requires its global state management.

The Elven Tools Dapp uses [useElven](https://www.useelven.com) which relies on [valtio](https://github.com/pmndrs/valtio) - a simple but compelling state management library for React. You'll read more about it in their docs. The most important is to know where it is used in the code and why.

The global state configuration sits in the [store](https://github.com/useElven/core/tree/main/src/store) directory in the useElven's repository. You will find there the auth and network global stores. The 'network' is just an object which keeps the information of the dapp provider and network provider. It will re-init them on every hard refresh. And for auth, we use global state with valtio.

The state is also synchronized with the localStorage to be able to reinitialize all required states on hard refresh. You will find such entries in the localStorage:

```
useElven_dapp__account: {"address":"","nonce":0,"balance":"", "addressIndex": 0}
```

```
useElven_dapp__loginInfo: {"loginMethod":"","expires":0,"loginToken":"","signature":"", "accessToken": ""}
```

The state is reused in many places in the app. There are custom Ract hooks for this purpose. We will check them later in the article.

### Dapp required configuration

The Dapp requires an initial configuration. It will be described in more detail in a dedicated section of the docs, so here is only a quick mention of what is where.

The most important would be to set up .env variables. You'll find the example here: [.env.example](https://github.com/ElvenTools/elven-tools-dapp/blob/main/.env.example). For deployment, you will also need to set them up. It can differ for different hosting providers or workflows. We will check the most simple ones, Netlify and Vercel, in separate docs sections.

The other place for configuration is the [config](https://github.com/ElvenTools/elven-tools-dapp/tree/main/config). There are four different config files. The one for UI configuration, mostly Chakra UI variables, the config for the network and static data for the Minter use case. Like the team, faq, etc.

### React custom hooks

The whole logic is based on custom React hooks from [useElven](https://www.useelven.com). There are many of them, but generally, the logic isn't very complicated. You'll find them here: [hook](https://github.com/useElven/core/tree/main/src/hooks). 

The most difficult to understand and, at the same time, the most important would be probably `useNetworkSync`. It is responsible for syncing the whole network, auth providers, and user accounts. It is essential to call it as soon as possible. If needed, you can also optimize component rerenders. The Elven Tools Dapp already has some of the optimization implemented.

Some hooks will serve the user's information, auth status, etc. There are also hooks responsible for auth providers initialization, like xPortal mobile app, browser extension, Ledger, and web wallet. And also, there are hooks responsible for querying smart contracts and making transactions.

For example: 

- [useLogin](https://github.com/useElven/core/blob/main/src/hooks/useLogin.tsx) hook includes all auth providers. It is just an abstraction. You could also want to use one of the providers, not all. You'll still be able to do that.
- [useElvenScQuery](https://github.com/ElvenTools/elven-tools-dapp/blob/main/hooks/interaction/elvenScHooks/useElvenScQuery.tsx) is responsible of querying Elven Tools smart contracts.

See more here [Dapp React hooks and components](/docs/dapp-react-hooks-and-components.html)

### NextJS pages + api configuration

With the Elven Tools Dapp, you are not limited to what you will see at the beginning. You can add more pages and change whatever you want. All is based on [NextJS](https://nextjs.org/) framework, a complete full-stack solution.

In the [pages](https://github.com/ElvenTools/elven-tools-dapp/tree/main/pages) directory, you will find actual pages. The NextJS framework builds the routing based on this directory. You can read more about it here: [Pages](https://nextjs.org/docs/basic-features/pages).

As you will see, the API directory is also inside the `pages`. Here you will find a configuration for the API endpoint. In this case, it is only a fallback endpoint for rewrites in case of no allowed calls to the API.

We also have the middleware logic for API, which will block the usage of the API by third-party services. Only the same host will be able to use it, so our instance of the Dapp. You can always disable that, but it is beneficial when you care about the API traffic. Most useful for paid API providers. Read more about it here: [Dapp API Proxy](/docs/dapp-api-proxy.html).

### React custom UI components

Finally, there are, of course, custom UI components. You will find them in the [components](https://github.com/ElvenTools/elven-tools-dapp/tree/main/components) directory. There is quite a lot of them. Most important are: 

- [LoginComponent](https://github.com/ElvenTools/elven-tools-dapp/blob/main/components/core/LoginComponent.tsx) - this one will handle all auth processes. It will render all auth providers buttons and connect them using the useLogin hook
- [LoginModalButton](https://github.com/ElvenTools/elven-tools-dapp/blob/main/components/core/LoginModalButton.tsx) - the button that also includes the modal wrapper for the LoginComponent
- [MintForm](https://github.com/ElvenTools/elven-tools-dapp/blob/main/components/MintForm.tsx) - this one will render the for minting with the input for the number of tokens to mint and all required states

Other essential parts are mainly specific to the current use case, so the minting dapp. But remember that you can use this Dapp is the boilerplate for any project you want to build.

See more here [Dapp React hooks and components](/docs/dapp-react-hooks-and-components.html)

### What's next?

Check more topics [here](/docs/minter-dapp-introduction.html#more-detailed-docs).

