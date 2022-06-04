---
layout: "docs"
title: "Common problems"
publicationDate: "2022-01-24"
tags:
  - intro
excerpt: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
ogTitle: "Elven Tools CLI tool - Common problems"
ogDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
ogUrl: "https://www.elven.tools/docs/common-problems.html"
twitterTitle: "Elven Tools CLI tool - Common problems"
twitterDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
twitterUrl: "https://www.elven.tools/docs/common-problems.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/common-problems.md"
---

Here you will find common problems when using the Elven Tools. In the future, there will be more improvements, good error messages, etc.

### CLI deploy transaction error

`Request error on url [transactions]: [{"statusCode":400,"message":""}]`

**Problem**: The problem occurs when deploying the smart contract with Elven Tools CLI with `elven-tools deploy nft-minter` \
**Cause**: You either don't have funds on the wallet that you are using with Elven Tools, or you have mismatched the configuration with the actual PEM file \
**Solution**: Ensure that the PEM file corresponds to your chain type configuration (the devnet by default, even without the configuration file). The PEM file should be derived from the seed phrase corresponding to the chain you want to deploy the smart contract. Also, make sure that you have funded the wallet.

### 'Token not issued' - the error from smart contract results

**Problem**: The problem occurs when setting the roles for the collection token with `elven-tools nft-minter set-roles` \
**Cause**: There is a time required between issuing the token and assigning the roles. The transaction can fail if the setting roles command is fired too quickly. \
**Solution**: Wait could of seconds and call the command again.

