---
layout: "docs"
title: "Jump start"
publicationDate: "2022-01-25"
tags:
  - intro
excerpt: "The Elven Tools includes the Smart Contract, CLI tool, and Landing page for NFT launches. Every part of it can be used as a separate tool."
ogTitle: "Elven Tools CLI tool - jump start!"
ogDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Landing page for NFT launches. Every part of it can be used as a separate tool."
ogUrl: "https://www.elven.tools/docs/jump-start.html"
twitterTitle: "Elven Tools CLI tool - jump start!"
twitterDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Landing page for NFT launches. Every part of it can be used as a separate tool."
twitterUrl: "https://www.elven.tools/docs/jump-start.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/jump-start.md"
---

<div class="docs-warning-box">Please be aware that there are not enough tests and no audits! As for the mainnet, use the tools at your own risk! The code is open source. You can always validate it and test it on the devnet. Check it back a million times before you'll use it on the mainnet. Please report all the issues and ideas.</div>

### TL;DR

1. `npm install -g elven-tools` -> install the npm library (you would need to have Node configured on the system)
2. `elven-tools derive-pem` -> provide the seed phrase, the walletKey.pem file will be generated
3. `elven-tools deploy nft-minter` -> provide all the data. There will be a couple of prompts
4. `elven-tools nft-minter issue-collection-token` -> provide the name and ticker, be careful. They should be short. The ticker should be capitalized
5. `elven-tools nft-minter set-roles` -> roles for the issued token
6. `elven-tools nft-minter shuffle` -> this one should be called at least one. It can be called at any time by anyone
7. `elven-tools nft-minter start-minting` -> starts the minting. By default, it is paused at start
8. `elven-tools nft-minter mint` -> mint tokens, provide the amount, be careful. There will be custom limits per address

### Longer step-by-step guides

The Elven Tools includes the Smart Contract, CLI tool, and Landing page for NFT launches. Every part of it can be used as a separate tool. But the best is to use it all together. You can, of course, use the Smart Contract separately using, for example, erdpy, but the elven-tools cli gives you a lot of simplification with the process. You don't have to think about proper arguments because it will ask you for them. Let's see what the workflow could look like.

Let's say that you want to prepare a collection generated randomly from .png layers. You can do this with many tools on the Internet. Btw, please take a look at my [custom solution](https://github.com/juliancwirko/nft-art-maker).

In the end, you will have a set of generated images and metadata JSON files corresponding to each. It can look like `1.png` and `1.json`. Then you would need to pack them and upload them to the IPFS. The IPFS is the only recommended decentralized hosting on the Elrond chain, at least for now. You can upload the files using for example the [Pinata](https://www.pinata.cloud/) or [NFT.storage](https://nft.storage/). When you do that, you will get the CIDs, a [content identifier](https://docs.ipfs.io/concepts/content-addressing/) for your assets. With that, we can start using the elven-tools cli. Let's jump to it right now.

First of all, you would need to install it globally. You need to set up the [Node](https://nodejs.org/en/) environment. The npm tool should be included. Then you would need to install the elven-tools CLI. You can do this by: `npm install -g elven-tools`.

By default, the elven-tools cli will come with pre-configured options. The most important is the chain on which it works. It is set to the 'devnet' and the source of the minter Smart Contract. It is set to the 'main' branch of [this](https://github.com/juliancwirko/elven-nft-minter-sc) repo. So in simple words, you don't have to do any configuration to start with the nft minter Smart Contract on the devnet. I'll show you how to configure it for the other setup later.

Let's focus on the devnet and the Smart Contract code from a remote source.

What you need to do to start is to run the `elven-tools derive-pem`. You should have the elven-tools cli installed globally so accessible from everywhere in your env. The best would be to create a separate directory to work with it.

```bash
elven-tools derive-pem
✔ Enter mnemonic (seed phrase)
 … source crop brown mountain grace imitate cattle rice profit truck small soul castle prize tube spoil such topic code actor venue friend truck alien
File saved as walletKey.pem
```

Derive PEM is a command which will take your seed phrase and create the key file for signing every transaction. Without it, you want to be able to use the elven-tools cli. The good thing is that you will need to do this only once. And then run every command in the same directory where the `walletKey.pem` file will land after running this command.

<div class="docs-error-box">
  Don't share your PEM file with anyone. It is the main key to your wallet—the same as the seed phrases. The elven-tools don't send any data to the Internet. It works with it only in your local file system.
</div>

After you generate the PEM file, you can run all other commands. Let's walk through the whole process here.

The first command will be `elven-tools deploy nft-minter`. It takes the Smart Contract code from its repository and tries to deploy it on behalf of the user whose walletKey.pem file is generated in this directory. It will ask a couple of questions. Let's explain them here.

When deploying using the CLI tool, it will also trigger the `populateIndexes` transactions, depending on the amount of the tokens provided. You can also call it by hand if something goes wrong. Always check the transactions after deployment on the Elrond explorer. This operation is mandatory, so if you don't use the CLI you would need to do it by yourself.

```bash
elven-tools deploy nft-minter
✔ Decide if the contract can be upgraded in the future.
 › Yes
✔ Decide if the contracts storage can be read by other contracts. Not recommended in this case.
 › No
✔ Decide if the contract can receive funds. Recommended because of the royalties.
 › Yes
✔ Provide the base IPFS CID:
 … main_asset_ipfs_cid_here
✔ Provide the base metadata files IPFS CID:
 … main_metadata_ipfs_cid_here
✔ Do you want to attach the metadata JSON file in the Assets/Uris? 
 (It will be attached and encoded in the attributes anyway, but some marketplaces require that). 
 › Yes
✔ Provide the file extension:
 › .png
✔ Provide amount of tokens in collection:
 … 10000
✔ Provide the seling price (ex. 0.5 for 0.5 EGLD):
 … 0.01
✔ Total tokens limit per one address per whole collection:
 … 6
✔ Provide the royalties value (ex. 20 for 20%) [optional]:
 … 5
✔ Provide tags (ex. tag1,tag2,tag3) [optional]:
 … test1,test2
✔ Provide the provenance hash (sha256 hash of all images) [optional]:
 … optional_provenance_hash_here
Deployment transaction executed: success
Deployment tx: https://devnet-explorer.elrond.com/transactions/6c78b4f9adbf4e04e84e5ffe8bfed577ee2ad080c039fb3c3db1199c5d1d413c
Populating indexes transaction executed!
Populate indexes tx (1): https://devnet-explorer.elrond.com/transactions/284addb23c3d6ec4809fcca1394a5827574aaf68397e0baf703c718c6319bd7a
Populating indexes transaction executed!
Populate indexes tx (2): https://devnet-explorer.elrond.com/transactions/254793bd5a005548f234d4efda54313fd8079e834ac9fe679f124d0a1bcf6a9b
Smart Contract address: erd1qqqqqqqqqqqqqpgqetmlnt8t8u9nll6l87we9wsp60m602pselesmc86cg
```

You will be asked one by one. The prompts are helpful. You don't have to worry about proper arguments preparation. The first three questions are about metadata for code. You need to decide if your smart contract should be payable or upgradable. There are hints for that. You can also read about it [here](https://docs.elrond.com/developers/developer-reference/code-metadata/).

The following prompt is where you would need to provide your CIDs. It can be a different CID for metadata and images, but it can also be the same CID. It depends on how you store your files in the IPFS. 

You will also be able to choose if you want your metadata file to be attached in the Assets/Uris next to the Uri for the asset file (like .png). The metadata Uri is encoded in the attributes, but some marketplaces also require it in the Uris array. 

Then you can also configure the file extension. There are a couple to choose from. 

After that, you will provide the total amount of tokens in your collection. 

Next is the selling price. You can use the standard format here. For example, 0.5 is 0.5 EGLD.

Then you would need to define how many tokens one address can mint. It is usually used to prevent a big player from buying the almost whole collection. Of course, it doesn't avoid minting on the different addresses, but it is always helpful.

Then you can provide the royalties value. Use standard percent here, so 5 is a 5%. 

Then you can give the tags for the collection, and at the end, you can also provide the [provenance hash](https://medium.com/coinmonks/the-elegance-of-the-nft-provenance-hash-solution-823b39f99473). It will also be queryable later.

The following mandatory command which you would use is issuing the collection token. You can do this by running `elven-tools nft-minter issue-collection-token`. The token will be issued, and all will be saved in the `output.json` file in the same directory. Here you will be asked about the name of the collection and the ticker. It looks like that:

```bash
elven-tools nft-minter issue-collection-token
✔ Enter the name for the collection token (ex. MyName123). 
Avoid spaces and special characters
 … TestCollectionName
✔ Enter the ticker for the collection token (ex. MYNAME). 
Avoid spaces and special characters. Keep it short and capitalize.
 … TCLN
⠼ Processing transaction...
Transaction: https://devnet-explorer.elrond.com/transactions/762adbb2485697c5b20a09ca28ff6bd4f0b11238ce57bee99d24c8ebd7a1d826
Your collection token id:  TCLN-416d0e
Also saved in the output.json file.
```

The last mandatory command is `elven-tools nft-minter set-roles`. It will assign the obligatory role, which allows for new NFT tokens creation. Here there won't be any prompts, at least for now. Only a transaction will take the token data from the output.json file and assign the roles.

```bash
elven-tools nft-minter set-roles
Transaction: https://devnet-explorer.elrond.com/transactions/b156ebc9f91a75c56ee5e1ae034c2e4ce09a9de16cde79f297221b457902e326
```

You would also need to call the `elven-tools nft-minter shuffle` at least once. This one is accessible for everyone. Everyone can call it to change the following index, which will be minted without knowing precisely what it will be.

```bash
elven-tools nft-minter shuffle
Transaction: https://devnet-explorer.elrond.com/transactions/c9248963f37e95ce81e58b06a6a8edc2872f48919302ca8d2914dcf3107aac19
```

The following steps can be different on what you want to achieve. You can start minting directly or set up so-called 'drops' where you will define how many tokens will be minted in one drop. You can also always start or pause the minting process. What is necessary is that the contract will always mint randomly in all cases. Let's see how it looks when we want just to start the minting: `elven-tools nft-minter start-minting` and `elven-tools nft-minter mint` You will be asked to provide how many tokens you would wish to mint. Remember that the Smart Contract will have limits per one address. See how to check them later in this article.

```bash
elven-tools nft-minter start-minting
✔ Are you sure that you want to proceed?
 › Yes
⠼ Processing transaction...
Transaction: https://devnet-explorer.elrond.com/transactions/8260437c4a2296169cf7bd925f135223529029ad8e1b3f2b535ee7f07ef3672c

elven-tools nft-minter mint
✔ Provide how many tokens should be minted.
Take into account possible limitations set on the Smart Contract (ex 3 for three tokens):
 … 2
✔ Are you sure that you want to proceed?
 › Yes
Transaction: https://devnet-explorer.elrond.com/transactions/15194f779bebc31babdc7711f685a4bf0560c9a0484f6e644a40a1a0ee2f94ef
```

Now let's see how to define a drop in which we will mint only 2500 of the whole 10k collection. `elven-tools nft-minter set-drop`. You will be asked to provide how many tokens per drop it should mint. After that, it will pause the minting process. You can also pause the minting at any time you want by `elven-tools nft-minter pause-minting`. You can also unset the drop by `elven-mint nft-minter unset-drop`. You'll find all the commands [here](/docs/cli-introduction.html), and some of them will be described later in this article.

```bash
elven-tools nft-minter set-drop
✔ Provide the amount of the tokens for the drop:
 … 2500
Transaction: https://devnet-explorer.elrond.com/transactions/915a9b115d01dbc0026e91ab889284018bd51cee8a030804dbb5da600c1bdd25

elven-tools nft-minter mint
✔ Provide how many tokens should be minted.
Take into account possible limitations set on the Smart Contract (ex 3 for three tokens):
 … 2
✔ Are you sure that you want to proceed?
 › Yes
Transaction: https://devnet-explorer.elrond.com/transactions/8954262fea15e63705d696fcfeb92874a4c10239703b5a6631fd7f989c494ba8
```

### How to work with the Smart Contract locally?

In most cases, it is good to provide some modifications for the final version of the Smart Contract, such as changing the functions' names to make life harder for the bot's owners. 

It is good to build the Smart Contract locally and deploy it from the file system in such a case. It is possible by default with the Elven Tools CLI. You need to prepare the directory `sc/nft-minter` in the same place where you already have the `walletKey.pem` file and later the `output.json` file. The tree should look like that:

```bash
.
├── output.json
├── sc
│   └── nft-minter
│       ├── elven-nft-minter.abi.json
│       └── elven-nft-minter.wasm
├── walletKey.pem
```

As you can see, we have the `.abi.json` and `.wasm` files there. You will find them in the `output` directory after building the Smart Contract locally, and the elven-tools cli tool will take them by default. Remember to only keep the same naming convention for the directories - `sc/nft-minter` and also run the `elven-tools` in the same directory.

If you need some help working with the Smart Contract in the Elrond ecosystem, please check docs and my article [here](https://www.julian.io/articles/elrond-smart-contracts.html).

### How to use the configuration file?

The configuration file is optional, and you don't need it until you want to change the chain or the Smart Contract source. Plus, maybe after some modifications, you would like to change the functions names and gas limit. All default values are defined [here](https://github.com/juliancwirko/elven-tools-cli/blob/main/src/config.ts), and below, you'll find the example of how to overwrite them from outside of the lib itself.

The configuration file should be named `.elventoolsrc,` or take any compatible name from the [cosmiconfig](https://github.com/davidtheclark/cosmiconfig) project. The main handle should be `elventools`.

```json
{
    "chain": "testnet",
    "nftMinterSc": {
        "version": "v1.2.0",
        "mintFnName": "mintMe"
    }
}
```

In the example above, we define the chain as the 'testnet' (devnet is set by default), and we also define the version for the Smart Contract, `v1.2.0` (the last tag name should always be selected as default). It can also be a branch name. Then we also define the new name for the 'mint' function. You can also change names for other functions and set up different gas limits.

**You will find all possible options [here](/docs/cli-introduction.html#custom-configuration-options).**

Remember, you don't have to change the `config.ts` file. It is for library usage. You don't have to clone the repository to change the configuration. `.elventoolsrc` is the only config file that should be used.

### Good to know

The Elven Tools CLI can list all the available commands for every subcommand. You can do: `elven-tools --help` or `elven-tools nft-minter --help`. You can always check the installed version by `elven-tools --version`.

Every step will update the `output.json` file. So, for example, the Smart Contract address will be put there and the collection token ticker. If you already deployed the Smart Contract without using the Elven Tools CLI, you can always configure it in the `.elventoolsrc` file using the config: `{ "nftMinterSc": { "deployNftMinterSC": "<sc_address_here>" } }`.

Not all the commands trigger a Smart Contract transaction. There are also public queries for the Smart Contract, for example: 

```bash
get-total-tokens-left
get-provenance-hash
get-drop-tokens-left
get-nft-price
get-nft-token-id
get-nft-token-name
get-tokens-limit-per-address-total
get-tokens-minted-per-address-total
get-tokens-limit-per-address-per-drop
get-minted-per-address-per-drop
```

With them, you can get simple information written in the Smart Contract. You can also access them through API. Read more about it [here](https://docs.elrond.com/sdk-and-tools/rest-api/virtual-machine/).

Elven Tools will also provide the landing page for the NFT launch, which will be strictly integrated with the Smart Contract. It will have a lot of useful widgets. There are also plans to write more articles on how to run it with the performance in mind. It will come later.

### Where to go from here?

This part of the docs had one purpose: to guide you through the process step by step. There is also a video which shows it. So I recommend you to check it out:

<div class="embeded-media-container">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/szkNE_qOy6Q" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

From here you can read more detailed docs on:
- [CLI configuration options](/docs/cli-introduction.html#custom-configuration-options)
- [CLI possible commands](/docs/cli-introduction.html#all-commands)
- [Smart Contract endpoints](/docs/sc-endpoints.html)

If you still don't know how to use it, please feel free to contact me on [Twitter](https://twitter.com/JulianCwirko) or [Telegram](https://t.me/juliancwirko). You can also write an e-mail to me: julian.cwirko@gmail.com
