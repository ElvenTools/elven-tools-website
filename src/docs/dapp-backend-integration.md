---
layout: 'docs'
title: 'Dapp backend integration'
publicationDate: '2022-04-19'
tags:
  - minter dapp
excerpt: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
ogTitle: "Elven Tools Dapp backend integration - MultiversX custom NextJS Dapp"
ogDescription: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
ogUrl: "https://www.elven.tools/docs/dapp-backend-integration.html"
twitterTitle: "Elven Tools Dapp backend integration - MultiversX custom NextJS Dapp"
twitterDescription: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
twitterUrl: "https://www.elven.tools/docs/dapp-backend-integration.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/dapp-backend-integration.md"
---

Sometimes, with more extensive apps and more logic, like managing custom information about users, etc., there is a need to implement user verification on the app's backend side. The Minter Dapp doesn't require the backend verification to work. It uses a public blockchain, and the user signs every transaction, but still, it is good to know how to extend it.

Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup. Here are basic steps on how you could verify the user on the backend side of your dapp: 

1. Login user using one of the dapp auth providers (Web Wallet, browser extension, xPortal mobile app, and Ledger).
2. By default useElven uses [@multiversx/sdk-native-auth-client](https://www.npmjs.com/package/@multiversx/sdk-native-auth-client) under the hood.
3. You will get the signature and accessToken back. They will also be saved in the local storage in the browser.
4. You already have an address, a custom token, and a signature and accessToken at this stage. You can send the accessToken to your backend and verify it using [@multiversx/sdk-native-auth-server](https://www.npmjs.com/package/@multiversx/sdk-native-auth-server)

Read more about it in the [docs](https://docs.multiversx.com/sdk-and-tools/sdk-js/sdk-js-signing-providers/#verifying-the-signature-of-a-login-token).