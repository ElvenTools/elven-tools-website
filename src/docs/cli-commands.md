---
layout: 'docs'
title: 'CLI Commands'
publicationDate: '2022-01-25'
tags:
  - cli tool
excerpt: "Here you will find all CLI commands with short descriptions."
ogTitle: "Elven Tools CLI tool - commands"
ogDescription: "Here you will find all CLI commands with short descriptions."
ogUrl: "https://www.elven.tools/docs/cli-commands.html"
twitterTitle: "Elven Tools CLI tool - commands"
twitterDescription: "Here you will find all CLI commands with short descriptions."
twitterUrl: "https://www.elven.tools/docs/cli-commands.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/cli-commands.md"
---

- `elven-tools derive-pem` - derives the PEM file from seed phrase (keywords)
- `elven-tools deploy nft-minter` - deploys the smart contract (by default from the defined tag branch using the devnet, can be configured)
- `elven-tools nft-minter issue-collection-token` [only owner] - issue main collection handle, it costs 0.05 EGLD, and it is a must in the Elrond chain. All NFTs will be under this collection. The cost here is a one-time payment for the whole collection.
- `elven-tools nft-minter set-roles` [only owner] - for now, the command sets the critical role for the collection handle. It is a 'create nft' role.
- `elven-tools nft-minter start-minting` [only owner] - by default, after deploying the smart contract, the minting is disabled. You would need to start it
- `elven-tools nft-minter pause-minting` [only owner] - you can also pause it at any moment
- `elven-tools nft-minter set-new-price` [only owner] - you can set a new price per NFT for the whole collection
- `elven-tools nft-minter giveaway` [only owner] - as an owner, you can give some random tokens to other addresses.
- `elven-tools nft-minter set-drop` [only owner] - you can also split the minting into drops. These are 'waves' of minting where you can change prices and promote each one (v1 doesn't include any logic for revealing the CIDs with delay, the revealed NFTs will be sent in every drop).
- `elven-tools nft-minter unset-drop` [only owner] - you can also disable the drop and pause minting
- `elven-tools nft-minter claim-dev-rewards` [only owner] - as an owner of the Smart Contract, you can always claim the developer rewards. Read more about them in the Elrond docs.
- `elven-tools nft-minter change-base-cids` [only owner] - you can change base IPFS CIDs only before any NFT was minted. Otherwise, it doesn't make sense to do that.
- `elven-tools nft-minter set-new-tokens-limit-per-address` [only owner] - it is possible to change the limits per address which are configured when deploying the Smart Contract
- `elven-tools nft-minter claim-sc-funds` [only owner] - this is treated as a fallback for royalties, there is no way for now to implement other solution, the Smart Contract will receive the royalties as the creator, so there has to be a way to get them back. Generally, it shouldn't be required otherwise. Proper solutions will be with the `esdt_nft_create_as_caller`, which doesn't work yet.
- `elven-tools nft-minter shuffle` - as a user, you can take part and ensure that the minting is random. This transaction will reshuffle the next index to mint. Everyone can run it.
- `elven-tools nft-minter mint` - the main mint function, you can mint NFTs using any `walletKey.pem` file
- `elven-tools nft-minter get-total-tokens-left` - the Smart Contract query, returns amount of tokens left
- `elven-tools nft-minter get-provenance-hash` - the Smart Contract query returns the provenance hash if provided when deploying
- `elven-tools nft-minter get-drop-tokens-left` - the Smart Contract query returns the number of tokens left per drop
- `elven-tools nft-minter get-nft-price` - the Smart Contract query, returns the current price
- `elven-tools nft-minter get-nft-token-id` - the Smart Contract query, returns the collection token id
- `elven-tools nft-minter get-nft-token-name` - the Smart Contract query, returns the collection token name
- `elven-tools nft-minter get-tokens-limit-per-address-total` - the Smart Contract query returns the tokens limit per address
- `elven-tools nft-minter get-minted-per-address-total` - the Smart Contract query returns the number of tokens minted per one address
- `elven-tools nft-minter get-minted-per-address-per-drop` - when the drop is configured, it will return the number of tokens minted per address per drop
- `elven-tools nft-minter get-tokens-limit-per-address-per-drop` - when the drop is configured, it will return the total limit of tokens per address per drop
- `elven-tools nft-minter populate-allowlist` - the command for preparing the allowlist, you will be able to read it for `sc/nft-minter/allowlist.json` file or you can provide addresses by hand. There is a limit of 250 addresses per transaction
- `elven-tools nft-minter enable-allowlist` - enable the allowlist, it won't be onsidered unles enabled even when it is filled with addresses,
- `elven-tools nft-minter disable-allowlist` - the option to disable the allowlist,
- `elven-tools nft-minter get-allowlist-size` - check the size of the allowlist,
- `elven-tools nft-minter is-allowlist-enabled` - check if allowlist is currently enabled,
- `elven-tools nft-minter get-allowlist-address-check` - check if provided address is included in the allowlist,