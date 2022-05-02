---
layout: 'docs'
title: 'SC Endpoints'
publicationDate: '2022-01-24'
tags:
  - smart contract
excerpt: "Below you'll find all endpoints with a short description. You can always see the complete code."
ogTitle: "Smart Contract version 1 - endpoints review"
ogDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
ogUrl: "https://www.elven.tools/docs/sc-endpoints.html"
twitterTitle: "Smart Contract version 1 - endpoints review"
twitterDescription: "Below you'll find all endpoints with a short description. You can always see the complete code."
twitterUrl: "https://www.elven.tools/docs/sc-endpoints.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/sc-endpoints.md"
---

Below you'll find all endpoints with a short description. You can always see the complete code [here](https://github.com/ElvenTools/elven-nft-minter-sc).

Please check all attributes for each endpoint in the linked code line in the repository. It is all open-source.

You'll find all the endpoints here: [lib.rs](https://github.com/ElvenTools/elven-nft-minter-sc/blob/main/src/lib.rs).

### Setup endpoints

These are the required operations you would need to perform once always when configuring a new collection and Smart Contract. Check the CLI tool to simplify the work required.

- `init` - standard init endpoint, it will be triggered on deployment and upgrade
- `populateIndexes` - A very important endpoint. It populates the VecMapper with indexes to mint. You would need to split the number of total tokens provided when deploying the contract into batches of 2200 max. The split is required because of the max gas limits. When using the Elven Tools CLI, the usage of this endpoint will be hidden when deploying. It will be done automatically. You won't mint if the indexes are not correctly populated. This operation is done only once with the number of transactions depending on the total amount of tokens. This additional configuration step gives us a performant way of randomly minting because the base is a VecMapper, and we use `swap_remove` there. I found it the simplest and most performant way of doing that.
- `issueToken` - required endpoint for creating a new collection, this is done once, and the token is one for one smart contract instance. It is a handler for the whole collection.
- `setLocalRoles` - Set roles set only one role for now. The required one for creating the NFTs.
- `shuffle` - this one is not owner only because everyone can call it, but it is required to call it at least once to be able to start minting
- `startMinting` - You will need to start the minting process after deploying the contract and each time you use the pauseMinting function

### Only owner endpoints

Only the owner of the Smart Contract can call them. In such a Smart Contract, there are quite a lot of them. Some of them are mandatory for the initial Smart Contract setup. See above. To keep everything in order, they are also copied here.

 - `init` - standard init endpoint, it will be triggered on deployment and upgrade
 - `populateIndexes` - A very important endpoint. It populates the VecMapper with indexes to mint. You would need to split the number of total tokens provided when deploying the contract into batches of 2200 max. The split is required because of the max gas limits. When using the Elven Tools CLI, the usage of this endpoint will be hidden when deploying. It will be done automatically. You won't mint if the indexes are not correctly populated. This operation is done only once with the number of transactions depending on the total amount of tokens. This additional configuration step gives us a performant way of randomly minting because the base is a VecMapper, and we use `swap_remove` there. I found it the simplest and most performant way of doing that.
- `issueToken` - required endpoint for creating a new collection, this is done once, and the token is one for one smart contract instance. It is a handler for the whole collection.
- `setLocalRoles` - Set roles set only one role for now. The required one for creating the NFTs. 
- `pauseMinting` - You can pause the minting process in any moment you need. 
- `startMinting` - You will need to start the minting process after deploying the contract and each time you use the pauseMinting function
- `setDrop` - You can set the 'drop' by defining how many tokens per drop will be minted 
- `unsetDrop` - You can unset the drop in any time. Minting will continue without limits.
- `setNewPrice` - You can change the price for each NFT at any time. The best is to do this when configuring the next drop.
- `changeBaseCids` - You can change the CIDs for images and metadata, but only when there is no NFTs minted yet. Otherwise, it doesn't make sense because the collection will be unsynchronized.
- `setNewTokensLimitPerAddress` - You can change the limit of tokens per single address in any given time.
- `giveaway` - You can organize the giveaway by providing the address and amount of tokens to send. It will mint and send tokens without the payment.
- `claimScFunds` - You can claim the funds which are there on the payable Smart Contract. For example, royalties paid by marketplaces. These are only funds that come from outside. The funds from minting are directly sent to the contract owner after each mint.
- `populateAllowlist` - You can set up the allowlist by populating the storage with addresses. Keep 320 addresses as max per one transaction. Otherwise, it could reach the max gas limit.
- `enableAllowlist` - You can enable to allowlist. Only then will it work. Remember about that.
- `disableAllowlist` - Tou can disable the allowlist and keep standard minting functionality
- `clearAllowlist` - It will clear the whole allowlist. The best is to keep a max of 1300 addresses in the allowlist at a time. Of course, if only you plan to clear it later. If you keep more and want to clear it, you can reach the gas limit for a transaction. So it would be best to split the allowlist per drop, keep it as small as possible and clear it each time.
- `removeAllowlistAddress` - removes a single address from allowlist

### Endpoints for all

- `mint` - The main mint/buy function. The smart contract works like a candy machine. You pay, and it randomly mints the NFT for you. Then it sends it into your wallet. The NFTs on the Elrond network are ESDT standardized tokens.
- `shuffle` - To be more transparent, the Smart Contract has a public endpoint that allows everyone to trigger the shuffling mechanism which is also triggered after every mint. This additional functionality ensures that the process is random, and anyone can set the following index.

### Smart Contract queries (also for all, by design)

- `getDropTokensLeft` - This query will return the tokens left for the active drop.
- `getTotalTokensLeft` - This query will return total amount of tokens left to mint 
- `getNftTokenId` - This query will return the collection token ticker
- `getNftTokenName` - This query will return the name for NFTs
- `getCollectionTokenName` - This query will return the collection token name
- `getNftPrice` - This query will return the price for a single NFT
- `getTokensLimitPerAddressTotal` - This query will return the limit of tokens for a single address as total for the whole collection
- `getMintedPerAddressTotal` - This query will return tokens already minted per single address as total for the whole collection
- `getTokensLimitPerAddressPerDrop` - This query will return the limit of tokens for a single address per drop
- `getMintedPerAddressPerDrop` - This query will return tokens already minted per single address per drop
- `getProvenanceHash` - This query will show the provenance hash if provided.
- `getAllowlistAddressCheck` - This query will check if the provided address is on the allowlist.
- `getAllowlistSize` - This is mainly to check if the allowlist has the correct size after populating it with addresses.
- `isAllowlistEnabled` - This is an important check to ensure that the allowlist is enabled. Only then will it work.
- `isDropActive` - This is for checking if there is currently a drop active.
- `getTotalSupply` - This is for checking the total supply
- `getTotalSupplyOfCurrentDrop` - This is for checking the supply of the current drop
- `isMintingPaused` - This is for checking if the minting process is now paused

### How to interact with endpoints

The simplest way is to use the Elven Tools CLI, check how in the [Jump start](/docs/jump-start.html) article or the [CLI introduction](/docs/cli-introduction.html).

If you don't want to use the CLI, you need to do the queries and transaction calls using the [erdjs SDK](https://github.com/ElrondNetwork/elrond-sdk-erdjs) or [erdpy](https://docs.elrond.com/sdk-and-tools/erdpy/erdpy/).

Check the examples for `erdjs`:

- [Smart Contract transaction](https://github.com/ElrondNetwork/elrond-sdk-erdjs#creating-smart-contract-transactions) 
- [Smart Contract query](https://github.com/ElrondNetwork/elrond-sdk-erdjs#querying-smart-contracts)

You can also check the [elven-tools-cli](https://github.com/ElvenTools/elven-tools-cli) source code, where I also used the erdjs SDK.

Check the examples for `erdpy`:

- [Command Line Interface](https://github.com/ElrondNetwork/elrond-sdk-erdpy/blob/main/erdpy/CLI.md) 
- [Blog post with usage examples](https://www.julian.io/articles/elrond-smart-contracts.html)
