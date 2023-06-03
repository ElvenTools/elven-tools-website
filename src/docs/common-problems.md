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
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/common-problems.md"
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
**Solution**: Wait a couple of seconds and call the command again.

### 'Account not found' - problem with the account

`Request error on url [accounts/erd1...]: [Account not found]`

**Problem**: The problem can occur with any CLI command, any transaction  \
**Cause**: The problem occurs when something is wrong with the network, or the devnet/testnet was reset, and your wallet doesn't exist anymore (doesn't have funds).  \
**Solution**: Double check your wallet, check if it works properly, and check if there are no problems with devnet/testnet if you use them. If so, then wait till the network works again.

### Ttimeout of 10000ms exceeded

`Request error on url [accounts/erd1...]: [Error: timeout of 10000ms exceeded]`

**Problem**: The public API which is in use by default isn't responding on time  \
**Cause**: The problem occurs when the network isn't responding fast. There is a limit of 10 seconds. Then the connection is closed.  \
**Solution**: You could try again, and if a couple of tries don't help, you would need to change the API provider. Check how [here](https://www.elven.tools/docs/recipes.html#custom-api-endpoints). Or you can wait some time for the public API to be in better shape.

### Problems with the CLI and system permissions

**Problem**: The `npm install elven-tools -g` throws an error related to permissions on the system.  \
**Cause**: Global instalation uses global system directories. Sometimes system users don't have access to them. It depends on the system's setup.  \
**Solution**: You can try to use tools like [nvm](https://github.com/nvm-sh/nvm) for better management of the npm versions and permissions. Or you can also try to fix the problem, the solutions are described here: [Resolving EACCES permissions errors when installing packages globally](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally). You can also try to run elven-tools using `npx`. For example: `npx elven-tools deploy nft-minter`.
