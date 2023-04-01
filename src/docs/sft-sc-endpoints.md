---
layout: 'docs'
title: 'SFT SC Endpoints'
publicationDate: '2023-03-30'
tags:
  - sft smart contract
excerpt: "Below you'll find all endpoints with a short description. You can always see the complete code."
ogTitle: "SFT Smart Contract - endpoints review"
ogDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
ogUrl: "https://www.elven.tools/docs/sft-sc-endpoints.html"
twitterTitle: "SFT Smart Contract - endpoints review"
twitterDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
twitterUrl: "https://www.elven.tools/docs/sft-sc-endpoints.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/sft-sc-endpoints.md"
---

Below you'll find all endpoints with a short description. You can always see the complete code [here](https://github.com/ElvenTools/elven-tools-sft-minter-sc).

Please check all attributes for each endpoint in the linked code line in the repository. It is all open-source.

You'll find all the endpoints [here](https://github.com/ElvenTools/elven-tools-sft-minter-sc/tree/main/src).

### Setup endpoints (only owner)

These are the required operations you would need to perform once always when configuring a new collection and Smart Contract. Check the CLI tool to simplify the work required.

- `init` - standard init endpoint, it will be triggered on deployment and upgrade
- `issueToken` - required endpoint for creating a new collection, this is done once. It is a handler for the whole single collection.
- `setLocalRoles` - Set three roles for now, create, mint and burn. Required for management of SFTs.
- `createToken` - create SFT tokens with the defined amount, assets, and attributes.

### Endpoints for all

- `buy` - buy SFT tokens

### Smart Contract queries (also for all, by design)

- `` - TODO

### How to interact with endpoints

The simplest way is to use the Elven Tools CLI, check how in the [Jump start](/docs/jump-start.html) article or the [CLI introduction](/docs/cli-introduction.html).

If you don't want to use the CLI, you need to do the queries and transaction calls using the [sdk-core](https://github.com/multiversx/mx-sdk-js-core), [sdk-dapp](https://github.com/multiversx/mx-sdk-dapp) or [mxpy](https://github.com/multiversx/mx-sdk-py-cli/blob/main/CLI.md).

Check the examples for `sdk-core`:

- [Smart Contract transaction](https://docs.multiversx.com/sdk-and-tools/sdk-js/sdk-js-cookbook#contract-interactions) 
- [Smart Contract query](https://docs.multiversx.com/sdk-and-tools/sdk-js/sdk-js-cookbook#contract-queries)

You can also check the [elven-tools-cli](https://github.com/ElvenTools/elven-tools-cli) source code, where I also used the MultiversX JS SDK.

Check the examples for `mxpy`:

- [Command Line Interface](https://github.com/multiversx/mx-sdk-py-cli/blob/main/CLI.md) 
- [Blog post with usage examples](https://www.julian.io/articles/multiversx-smart-contracts.html)