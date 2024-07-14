---
layout: 'docs'
title: 'SFT SC Introduction'
publicationDate: '2023-04-01'
tags:
  - sft smart contract
excerpt: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying SFT tokens"
ogTitle: "SFT Smart Contract - introduction"
ogDescription: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying SFT tokens"
ogUrl: "https://www.elven.tools/docs/sft-sc-introduction.html"
twitterTitle: "SFT Smart Contract - introduction"
twitterDescription: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying SFT tokens"
twitterUrl: "https://www.elven.tools/docs/sft-sc-introduction.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/sft-sc-introduction.md"
---

SFT minter Smart Contract

<div class="docs-info-box ">Be aware that the Smart Contract doesn't have any audits. It has complete functionality for the first version but still needs some improvements. Test it first on the devnet/testnet. And be sure that you know what you are doing.</div>

You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying SFT tokens from a previously configured collection.

### It supports:

- issuing the collection token
- setting the create role
- creating SFT
- changing basic setup where it is possible

In short, you can issue a collection token and then create multiple SFT tokens with different initial supplies, attributes, and assets. Each token will have a different nonce. All that should be done using the owner's wallet. Then other wallets can buy a specific amount of the SFT token with the particular nonce. The operator of the smart contract (owner) can define the price per single token and max tokens to buy per single address. There will be more functionality in the following versions.

### Required initial configuration

All are mandatory operations and should be done only once. Make the transactions in this order.

1. The Smart Contract requires initial configuration to start the minting process. First, you would need to deploy it. Check the description and link to the code in the [endpoints section](/docs/sft-sc-endpoints.html). It is simpler if you are using the [Elven Tools CLI](/docs/cli-introduction.html).
2. You would need to issue the collection token using the `issueCollection` endpoint. With CLI, it is simpler to do that. Again, check it in the endpoints section.
3. Next is the `setLocalRoles` endpoint - it is required to set up proper roles for the collection token.
4. Finally, you need to create the amount of SFT tokens with all attributes and assets. You can do this using `createToken` endpoint.

Then you are ready to buy. You can use `buy` endpoint for that.

**Remember that everything is more straightforward with the Elven Tools CLI** Check the [jump start section](/docs/jump-start.html#sft-minter-tl%3Bdr).

### Ways of using it

The best way of using it will be with [Elven Tools CLI tool](/docs/cli-introduction.html). It has a lot of valuable functions integrated, so deploying or interacting is simple. You can deploy the smart contract directly from its repository. Almost no coding skills are required in this case.

You can also take a more standard path and use [mxpy](https://docs.multiversx.com/sdk-and-tools/sdk-py/mxpy-cli) for that. Mxpy CLI is an official CLI SDK for MultiversX blockchain based on Python. It is harded because you would need to take care of all needed data and data formats. You can check snippets in the repository.

### Issues and ideas

Please post issues and ideas [here](https://github.com/ElvenTools/elven-sft-tools-minter-sc/issues).

### Contact

- [x.com/theJulianIo](https://x.com/theJulianIo)
- julian.cwirko@gmail.com

<div class="next-page-link">
  Next: <a href="/docs/sft-sc-endpoints.html">SC endpoints review</a>
</div>
