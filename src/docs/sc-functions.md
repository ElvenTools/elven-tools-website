---
layout: 'docs'
title: 'Functions'
publicationDate: '2022-01-24'
tags:
  - smart contract
ogTitle: "Smart Contract version 1 - functions review"
ogDescription: ""
ogUrl: "https://www.elven.tools/docs/sc-functions.html"
twitterTitle: "Smart Contract version 1 - functions review"
twitterDescription: ""
twitterUrl: "https://www.elven.tools/docs/sc-functions.html"
---

Below you'll find all endpoints with short description. You can always see whole code [here](https://github.com/juliancwirko/elven-nft-minter-sc).

### Only owner endpoints

Endpoints which can be called only by the owner. In such a Smart Contract there are quite a lot of them.

- `init` - standard init function, it will be triggered on deployment and upgrade
- `issueToken` - required endpoint for creating a new collection, this is done once, and the token is one for one smart contract instance. This is a handler for the whole collection. You can read more about it [here](https://docs.elrond.com/developers/nft-tokens/#issuance-of-non-fungible-tokens)
- ``

### Endpoints for all

### Smart Contract queries