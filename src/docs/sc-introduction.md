---
layout: 'docs'
title: 'SC Introduction'
publicationDate: '2022-01-25'
tags:
  - smart contract
excerpt: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying NFT tokens"
ogTitle: "Smart Contract version 1 - introduction"
ogDescription: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying NFT tokens"
ogUrl: "https://www.elven.tools/docs/sc-introduction.html"
twitterTitle: "Smart Contract version 1 - introduction"
twitterDescription: "You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying NFT tokens"
twitterUrl: "https://www.elven.tools/docs/sc-introduction.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/sc-introduction.md"
---

NFT minter Smart Contract v1

<div class="docs-info-box ">Be aware that the Smart Contract doesn't have any audits. It has complete functionality for the first version, but it is still needs some improvements. Test it first on the devnet/testnet.</div>

You are reading about the Smart Contract designed for the MultiversX blockchain. Its primary purpose is to provide a simple logic for minting and buying NFT tokens from a previously configured collection. It does it in a randomized way. 

### Version 1 supports

- issuing the collection token
- setting the create role
- pausing/unpausing the process
- random mint and distribution
- minting multiple NFTs in one transaction
- giveaway options
- possibility to split the process into drops/waves
- claiming the developer rewards
- changing basic setup where it is possible

The smart contract works like a candy machine. In short, the user can pay in EGLD and, in return, will get randomly minted tokens from the previously configured collection. The amount of tokens per address is configured on the smart contract.

### Required initial configuration

All are mandatory operations and should be done only once. Make the transactions in this order.

1. The Smart Contract requires initial configuration to start the minting process. First, you would need to deploy it with all the arguments defined for the `init` endpoint. Check the description and link to the code in the [endpoints section](/docs/sc-endpoints.html). It is simpler if you are using the [Elven Tools CLI](/docs/cli-introduction.html).
2. You would need to issue the collection token using the `issueCollection` endpoint. With CLI, it is simpler to do that. Again, check it in the endpoints section.
3. Next is the `setLocalRoles` endpoint - it is required to set up proper roles for the collection token.
4. Finally, you need to start the minting by calling the `startMinting` endpoint. By default, in the beginning, the minting is paused.

**Remember that everything is more straightforward with the Elven Tools CLI** Check the [jump start section](/docs/jump-start.html).

### Ways of using it

The best way of using it will be with [Elven Tools CLI tool](/docs/cli-introduction.html). It has a lot of valuable functions integrated with the smart contract, so deploying or interacting is simple. You can deploy the smart contract directly from its repository. Almost no coding skills are required in this case.

You can also take a more standard path and use [erdpy](https://docs.multiversx.com/sdk-and-tools/erdpy/) for that. Erdpy is an official CLI SDK for MultiversX blockchain based on Python. For more information, check the [blog post](https://www.julian.io/articles/multiversx-smart-contracts.html).

### Limitations and caveats

- Remember that it is most likely that because of the open-source nature of this Smart Contract, it won't be used only in a way that everyone would want to, be aware that you can always change the names of the endpoints in the Smart Contract. You can even deploy a couple of them. In the last minutes before the mint decide to use one of them. This will limit the bots. Remember always to inform which one is the official one.
- Smart Contract in version 1 doesn't have many mechanisms which will strongly limit unwanted behaviors. It only implements random minting, but in version 2, there will be more mechanisms for fair launches.

### Issues and ideas

Please post issues and ideas [here](https://github.com/ElvenTools/elven-nft-minter-sc/issues).

### Contact

- [Telegram](https://t.me/juliancwirko)
- [Twitter](https://twitter.com/JulianCwirko)
- julian.cwirko@gmail.com

<div class="next-page-link">
  Next: <a href="/docs/sc-endpoints.html">SC endpoints review</a>
</div>
