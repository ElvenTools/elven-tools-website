---
layout: 'docs'
title: 'CLI SFT Workflow'
publicationDate: '2022-01-26'
tags:
  - cli tool
excerpt: "Here you will find a detailed explanation of how the CLI works with the SFT Minter smart contract."
ogTitle: "Elven Tools CLI tool - SFT Workflow"
ogDescription: "Here you will find a detailed explanation of how the CLI works with the SFT Minter smart contract."
ogUrl: "https://www.elven.tools/docs/cli-sft-workflow.html"
twitterTitle: "Elven Tools CLI tool - SFT Workflow"
twitterDescription: "Here you will find a detailed explanation of how the CLI works with the SFT Minter smart contract."
twitterUrl: "https://www.elven.tools/docs/cli-sft-workflow.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/cli-sft-workflow.md"
---

The Elven Tools includes the smart contracts, CLI tool, and Minter Dapp. Every part of it can be used as a separate tool. But the best is to use it all together. You can, of course, use the Smart Contract separately using, for example, mxpy, but the elven-tools cli gives you a lot of simplification with the process. You don't have to think about proper arguments because it will ask you for them. Let's see what the workflow could look like.

Let's assume you want to create SFTs with one .png file as their asset. You can make such a collection using Elven Tools SFT smart contract and CLI tool.

When it comes to assets you can upload the files using for example the [Pinata](https://www.pinata.cloud/) or [NFT.storage](https://nft.storage/). When you do that, you will get the CIDs, a [content identifier](https://docs.ipfs.io/concepts/content-addressing/) for your assets. Read more about how it works on MultiversX blockchain for SFTs and NFTs [here](/docs/use-of-ipfs-in-the-multiversx-nft-ecosystem.html).

With that, we can start using the elven-tools cli. Let's jump to it right now.

First of all, you would need to install it globally. You need to set up the [Node](https://nodejs.org/en/) environment. The npm tool should be included. Then you would need to install the elven-tools CLI. You can do this by: `npm install -g elven-tools`.

By default, the elven-tools cli comes with pre-configured options. The most important is the chain on which it works. It is set to the 'devnet' and the source of the minter Smart Contract is set to the 'main' branch of [this](https://github.com/ElvenTools/elven-tools-sft-minter-sc) repo. So in simple words, you don't have to do any configuration to start with the sft minter Smart Contract on the devnet. I'll show you how to configure it for the other setup later.

Let's focus on the devnet and the Smart Contract code from a remote source.

What you need to do to start is to run the `elven-tools derive-pem`. You should have the elven-tools cli installed globally so accessible from everywhere in your system. The **best** would be to **create a separate directory** to work with it.

```bash
elven-tools derive-pem
✔ Enter mnemonic (seed phrase)
 … source crop brown mountain grace imitate cattle rice profit truck small soul castle prize tube spoil such topic code actor venue friend truck alien
File saved as walletKey.pem
```

Derive PEM is a command which will take your seed phrase and create the key file for signing every transaction. Without it, you won't be able to use the elven-tools cli. The good thing is that you will need to do this only once. And then run every command in the same directory where the `walletKey.pem` file will land after running this command.

**Important**: You need to use the correct wallet. If you want to deploy the smart contract on the devnet, please use the devnet seed phrase and ensure that your wallet has some funds. You can use the faucet in the devnet web wallet to get some fake EGLD for testing.

<div class="docs-error-box">
  Don't share your PEM file and seed phrase with anyone. It is the main key to your wallet—the same as the seed phrases. The elven-tools don't send any data to the Internet. It works with it only in your local file system.
</div>

After you generate the PEM file, you can run all other commands. But **remember** that your **wallet needs funds**. Otherwise, it won't work. Each transaction takes fees. 

Let's walk through the whole process here.

The first command will be `elven-tools deploy sft-minter`. It takes the Smart Contract code from its repository and tries to deploy it on behalf of the user whose walletKey.pem file is generated in this directory.

```bash
elven-tools deploy sft-minter

✔ Are you sure that you want to proceed?
 › Yes

Deployment transaction executed: success
Deployment tx: https://devnet-explorer.multiversx.com/transactions/3ed03f012b5bafbd1e3634ec37eab201d8fac087010b29ec9596fa4272ad47c9

Smart Contract address: erd1qqqqqqqqqqqqqpgq4vvwttr9flqpn8j83kz4y7cx7lnwvuys67es47jdmp
```

The following mandatory command which you would use is issuing the collection token. You can do this by running `elven-tools sft-minter issue-collection-token`. The token will be issued, and all will be saved in the `output.json` file in the same directory. Here you will be asked about the name of the collection and the ticker. It looks like that:

```bash
elven-tools sft-minter issue-collection-token

✔ Enter the name for the collection token (ex. MyName123). 
(3-20 characters, alphanumeric only)
 … MySFTToken
✔ Enter the ticker for the collection token (ex. MYNAME). 
(3-10 characters, alphanumeric and uppercase only)
 … MST

✔ Are you sure that you want to proceed?
 › Yes

Transaction status: success
Transaction link: https://devnet-explorer.multiversx.com/transactions/b4fca422919a102cec7be4270f21e9e11e2a9c323c7004dadac0ff4337962fa1
```

The next mandatory command is `elven-tools sft-minter set-roles`. It will assign the obligatory role, which allows for new SFT tokens creation. It will also assign mint and burn roles. In the future it will be more configurable. 

Here there won't be any prompts, at least for now. Only a transaction will take the token data from the output.json file and assign the roles.

```bash
elven-tools sft-minter set-roles

✔ Are you sure that you want to proceed?
 › Yes

Transaction status: success
Transaction link: https://devnet-explorer.multiversx.com/transactions/13338b54b7c278975be6745cb8384aba75264029e9aa2dc25105b7db1c572da3
```

Next mandatory command is `elven-tools sft-minter create`. It will create SFT token with all attributes, assets, defined selling price etc. You can create multiple SFT tokens with different initial supply under one collection handle (token).

```bash
elven-tools sft-minter create

✔ Provide token display name (Alphanumeric characters only):
 … My SFT token for testing 
✔ Provide the selling price (ex. 0.5 for 0.5 EGLD):
 … 0.01
✔ Provide the the metadata file CID from IPFS:
 … here_should_land_the_IPFS_CID_for_your_metadata_file
✔ Provide the the metadata file name uploaded using IPFS (ex: metadata.json):
 … metadata.json
✔ Provide the initial SFT supply (amount of tokens):
 … 100000
✔ Provide the max tokens to buy per address:
 … 100
✔ Provide the royalties value (ex. 5.5 for 5.5%):
 … 5
✔ Provide tags (ex. tag1,tag2,tag3):
 … tag1,tag2
✔ Provide assets URIS. Whole URIs from IPFS. To your images, music, video files.
Separate them with comma (","):
 … https://ipfs_url_to_your_assets.com
✔ Are you sure that you want to proceed?
 › Yes

Transaction status: success
Transaction link: https://devnet-explorer.multiversx.com/transactions/8fc21a08d62d2d1312add3a89d758b8e4610bf9ec1ac799def52c75ef80e4e7f
```

After that, you can also use the CLI to buy specific SFT tokens (an amount of them). For simplicity, you must provide its nonce in hex format because, for example, for the TTSFT-d1d695-01 SFT token, the nonce is 01 already in hex format. So you need to find the token ticker and pass the third segment of its name here.

Under the TTSFT-d1d695 collection token, you can have different SFTs with different initial supplies, attributes, and assets. What differentiates them and identifies them is the nonce number.

```bash
elven-tools sft-minter buy 

✔ Provide token nonce (for example in TTSFT-d1d695-01 the 01 has to be provided):
 … 02
✔ Provide the amount of SFT to buy:
 … 12
✔ Are you sure that you want to proceed?
 › Yes

Transaction status: success
Transaction link: https://devnet-explorer.multiversx.com/transactions/848bcbf8254f2197cf32027e99c40e244e2a0c8abdf98990fa477a0bf35b85b2
```

These are crucial commands. There is more. All of them are in the [CLI commands](/docs/cli-commands.html) section.

### Good to know

The Elven Tools CLI can list all the available commands for every subcommand. You can do: `elven-tools --help` or `elven-tools sft-minter --help`. You can always check the installed version by `elven-tools --version`.

Every step will update the `output.json` file. So, for example, the Smart Contract address will be put there. If you already deployed the Smart Contract without using the Elven Tools CLI, you can always configure it in the `.elventoolsrc` file using the config: `{ "sftMinterSc": { "deploySftMinterSC": "<sc_address_here>" } }`.

Not all the commands trigger a Smart Contract transaction. There are also public queries for the Smart Contract, for example: 

```bash
- getCollectionTokenName
- getCollectionTokenId
- getTokenDisplayName
- getPrice
- getMaxAmountPerAddress
```
...and more, check `elven-tools sft-minter --help` for the whole list.

With them, you can get simple information written in the Smart Contract. You can also access them through API. Read more about it [here](https://docs.multiversx.com/sdk-and-tools/rest-api/virtual-machine).

Elven Tools also provides the Minter Dapp for the SFT launch, which strictly integrates with the Smart Contract. It have a lot of useful widgets.

### Where to go from here

- [CLI commands](/docs/cli-commands.html)
- [Recipes](/docs/recipes.html)
