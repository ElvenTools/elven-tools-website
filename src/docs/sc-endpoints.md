---
layout: 'docs'
title: 'Endpoints'
publicationDate: '2022-01-24'
tags:
  - smart contract
ogTitle: "Smart Contract version 1 - endpoints review"
ogDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
ogUrl: "https://www.elven.tools/docs/sc-endpoints.html"
twitterTitle: "Smart Contract version 1 - endpoints review"
twitterDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
twitterUrl: "https://www.elven.tools/docs/sc-endpoints.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/sc-endpoints.md"
---

Below you'll find all endpoints with a short description. You can always see the complete code [here](https://github.com/juliancwirko/elven-nft-minter-sc).

Please check all attributes for each endpoint in the linked code line in the repository. It is all open-source.

### Setup endpoints

These are the required operations you would need to perform once always when configuring a new collection and Smart Contract. Check the CLI tool to simplify the work required.

- [init](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L22) - standard init endpoint, it will be triggered on deployment and upgrade
- [populateIndexes](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L255) - A very important endpoint. It populates the VecMapper with indexes to mint. You would need to split the number of total tokens provided when deploying the contract into batches of 5000 max. The split is required because of the max gas limits. When using the Elven Tools CLI, the usage of this endpoint will be hidden when deploying. It will be done automatically. You won't mint if the indexes are not correctly populated. This operation is done only once with the number of transactions depending on the total amount of tokens. This additional configuration step gives us a performant way of randomly minting because the base is a VecMapper, and we use `swap_remove` there. I found it the simplest and most performant way of doing that.
- [issueToken](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L72) - required endpoint for creating a new collection, this is done once, and the token is one for one smart contract instance. It is a handler for the whole collection. You can read more about it [here](https://docs.elrond.com/developers/nft-tokens/#issuance-of-non-fungible-tokens)
- [setLocalRoles](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L104) - Set roles set only one role for now. The required one for creating the NFTs.
- [shuffle](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L367) - this one is not owner only because everyone can call it, but it is required to call it at least once to be able to start minting
- [startMinting](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L129) - You will need to start the minting process after deploying the contract and each time you use the pauseMinting function

### Only owner endpoints

Only the owner of the Smart Contract can call them. In such a Smart Contract, there are quite a lot of them. Some of them are mandatory for the initial Smart Contract setup. See above. To keep everything in order, they are also copied here.

 - [init](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L22) - standard init endpoint, it will be triggered on deployment and upgrade
 - [populateIndexes](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L255) - A very important endpoint. It populates the VecMapper with indexes to mint. You would need to split the number of total tokens provided when deploying the contract into batches of 5000 max. The split is required because of the max gas limits. When using the Elven Tools CLI, the usage of this endpoint will be hidden when deploying. It will be done automatically. You won't mint if the indexes are not correctly populated. This operation is done only once with the number of transactions depending on the total amount of tokens. This additional configuration step gives us a performant way of randomly minting because the base is a VecMapper, and we use `swap_remove` there. I found it the simplest and most performant way of doing that.
- [issueToken](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L72) - required endpoint for creating a new collection, this is done once, and the token is one for one smart contract instance. It is a handler for the whole collection. You can read more about it [here](https://docs.elrond.com/developers/nft-tokens/#issuance-of-non-fungible-tokens)
- [setLocalRoles](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L104) - Set roles set only one role for now. The required one for creating the NFTs. 
- [pauseMinting](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L120) - You can pause the minting process in any moment you need. 
- [startMinting](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L129) - You will need to start the minting process after deploying the contract and each time you use the pauseMinting function
- [setDrop](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L137) - You can set the 'drop' by defining how many tokens per drop will be minted 
- [unsetDrop](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L147) - You can unset the drop in any time. Minting will continue without limits.
- [setNewPrice](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L157) - You can change the price for each NFT at any time. The best is to do this when configuring the next drop.
- [changeBaseCids](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L166) - You can change the CIDs for images and metadata, but only when there is no NFTs minted yet. Otherwise, it doesn't make sense because the collection will be unsynchronized.
- [setNewTokensLimitPerAddress](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L185) - You can change the limit of tokens per single address in any given time.
- [giveaway](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L193) - You can organize the giveaway by providing the address and amount of tokens to send. It will mint and send tokens without the payment.
- [claimScFunds](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L220) - You can claim the funds which are there on the payable Smart Contract. For example, royalties paid by marketplaces. 

### Endpoints for all

- [mint](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L235) - The main mint/buy function. The smart contract works like a candy machine. You pay, and it randomly mints the NFT for you. Then it sends it into your wallet. The NFTs on the Elrond network are ESDT standardized tokens.
- [shuffle](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L367) - To be more transparent, the Smart Contract has a public endpoint that allows everyone to trigger the shuffling mechanism which is also triggered after every mint. This additional functionality ensures that the process is random, and anyone can set the following index.

### Smart Contract queries

- [getDropTokensLeft](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L508) - This query will return the tokens left for the active drop.
- [getTotalTokensLeft](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L517) - This query will return total amount of tokens left to mint 
- [getNftTokenId](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L527) - This query will return the collection token ticker
- [getNftTokenName](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L531) - This query will return the collection token name
- [getNftPrice](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L535) - This query will return the price for a single NFT
- [getTokensLimitPerAddress](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L543) - This query will return the limit of tokens for a single address
- [getTokensMintedPerAddress](https://github.com/juliancwirko/elven-nft-minter-sc/blob/main/src/lib.rs#L547) - This query will return tokens already minted per single address 


### How to interact with endpoints

The simplest way is to use the Elven Tools CLI, check how in the [Jump start](/docs/jump-start.html) article or the [CLI introduction](/docs/cli-introduction.html).

If you don't want to use the CLI, you need to do the queries and transaction calls using the [erdjs SDK](https://github.com/ElrondNetwork/elrond-sdk-erdjs).

Check the examples:

- [Smart Contract transaction](https://github.com/ElrondNetwork/elrond-sdk-erdjs#creating-smart-contract-transactions) 
- [Smart Contract query](https://github.com/ElrondNetwork/elrond-sdk-erdjs#querying-smart-contracts)

You can also check the [elven-tools-cli](https://github.com/juliancwirko/elven-tools-cli) source code, where I also used the erdjs SDK.

With the landing page, you will get all of these as widgets.
