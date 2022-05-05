---
layout: 'docs'
title: 'Dapp backend integration'
publicationDate: '2022-04-19'
tags:
  - minter dapp
excerpt: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
ogTitle: "Elven Tools Dapp backend integration - Elrond custom NextJS Dapp"
ogDescription: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
ogUrl: "https://www.elven.tools/docs/dapp-backend-integration.html"
twitterTitle: "Elven Tools Dapp backend integration - Elrond custom NextJS Dapp"
twitterDescription: "Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup."
twitterUrl: "https://www.elven.tools/docs/dapp-backend-integration.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/dapp-backend-integration.md"
---

Sometimes, with more extensive apps and more logic, like managing custom information about users, etc., there is a need to implement user verification on the app's backend side. The Minter Dapp doesn't require the backend verification to work. It uses a public blockchain, and the user signs every transaction, but still, it is good to know how to extend it.

Elven Tools Dapp is an excellent base for building more complicated stuff on it. It uses the NextJS framework, so you also have a free backend setup. Here are basic steps on how you could verify the user on the backend side of your dapp: 

1. Login user using one of the dapp auth providers (Web Wallet, browser extension, Maiar mobile app).
2. When logging in, pass the custom token. It can be a randomly generated hash.
3. You will get the signature back. It will also be saved in the local storage in the browser.
4. You already have an address, a custom token, and a signature at this stage. You can send it to your backend and verify it.
5. Then, you could prepare a JWT token and send it back to the frontend. The user can use the JWT token and authorize protected operations/endpoints from now on.

There are three important things here:
1. How will we get the public key?
1. What message will we verify? 
2. How to verify it?

The public key can be fetched using the user's address and erdjs methods. You can do this like that: 

```
import { Address, UserPublicKey } from '@elrondnetwork/erdjs'

const pubKey = new UserPublicKey(address.pubkey());
const verifier = new UserVerifier(pubKey);
```

The message is more complicated than just the custom token. We would need to prepare the message like that: 

```
const msg = 'erdUserAddressHere' + 'yourCustomTokenHere' + JSON.stringify({});
```

Then you would need to prepare the Signature instance:

```
const signature = new Signature(Buffer.from(msg, 'hex'));
```

And finally, you can verify it:

```
const signMessage = new SignableMessage({
    address: address,
    message: Buffer.from(message),
    signature: signature,
});
verifier.verify(signMessage);
```

You would also need to handle the expiration for the JWT token. The expiry for the dapp login is already handled by Elven Tools Dapp.

You will find the full working example in the repository prepared by [@borispoehland](https://github.com/borispoehland). Check it out: [
elven-tools-dapp-with-auth](https://github.com/borispoehland/elven-tools-dapp-with-auth)
