---
layout: 'docs'
title: 'CLI NFT Workflow'
publicationDate: '2022-01-26'
tags:
  - cli tool
excerpt: "Here you will find a detailed explanation of how the CLI works with the NFT Minter smart contract."
ogTitle: "Elven Tools CLI tool - NFT Workflow"
ogDescription: "Here you will find a detailed explanation of how the CLI works with the NFT Minter smart contract."
ogUrl: "https://www.elven.tools/docs/cli-nft-workflow.html"
twitterTitle: "Elven Tools CLI tool - NFT Workflow"
twitterDescription: "Here you will find a detailed explanation of how the CLI works with the NFT Minter smart contract."
twitterUrl: "https://www.elven.tools/docs/cli-nft-workflow.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/cli-nft-workflow.md"
---

The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool. But the best is to use it all together. You can, of course, use the Smart Contract separately using, for example, mxpy, but the elven-tools cli gives you a lot of simplification with the process. You don't have to think about proper arguments because it will ask you for them. Let's see what the workflow could look like.

Let's say that you want to prepare a collection generated randomly from .png layers. You can do this with many tools on the Internet. Btw, please take a look at my [custom solution](https://github.com/ElvenTools/nft-art-maker).

In the end, you will have a set of generated images and metadata JSON files corresponding to each. It can look like `1.png` and `1.json`. Then you would need to pack them and upload them to the IPFS. The IPFS is the only recommended decentralized hosting on the MultiversX chain, at least for now. You can upload the files using for example the [Pinata](https://www.pinata.cloud/) or [NFT.storage](https://nft.storage/). When you do that, you will get the CIDs, a [content identifier](https://docs.ipfs.io/concepts/content-addressing/) for your assets. With that, we can start using the elven-tools cli. Let's jump to it right now.

First of all, you would need to install it globally. You need to set up the [Node](https://nodejs.org/en/) environment. The npm tool should be included. Then you would need to install the elven-tools CLI. You can do this by: `npm install -g elven-tools`.

By default, the elven-tools cli will come with pre-configured options. The most important is the chain on which it works. It is set to the 'devnet' and the source of the minter Smart Contract is set to the 'main' branch of [this](https://github.com/ElvenTools/elven-nft-minter-sc) repo. So in simple words, you don't have to do any configuration to start with the nft minter Smart Contract on the devnet. I'll show you how to configure it for the other setup later.

Let's focus on the devnet and the Smart Contract code from a remote source.

What you need to do to start is to run the `elven-tools derive-pem`. You should have the elven-tools cli installed globally so accessible from everywhere in your env. The **best** would be to **create a separate directory** to work with it.

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

The first command will be `elven-tools deploy nft-minter`. It takes the Smart Contract code from its repository and tries to deploy it on behalf of the user whose walletKey.pem file is generated in this directory. It will ask a couple of questions. Let's explain them here.

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
✔ Provide the selling price (ex. 0.5 for 0.5 EGLD):
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
Deployment tx: https://devnet-explorer.multiversx.com/transactions/6c78b4f9adbf4e04e84e5ffe8bfed577ee2ad080c039fb3c3db1199c5d1d413c
```

You will be asked one by one. The prompts are helpful. You don't have to worry about proper arguments preparation. The first three questions are about metadata for code. You need to decide if your smart contract should be payable or upgradable. There are hints for that. You can also read about it [here](https://docs.multiversx.com/developers/developer-reference/code-metadata).

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
(3-20 characters, alphanumeric only)
 … TestOnly
✔ Enter the ticker for the collection token (ex. MYNAME). 
(3-10 characters, alphanumeric and uppercase only)
 … TSTONL
✔ Do you want to remove the edition number from the name? (example: 'name #1' when there is 1.json and 1.png) › No
✔ Enter the name for NFTs. If not provided, the name of the collection will be used. (Optional)
 … 
✔ Please choose token properties.
 ›  
Instructions:
    ↑/↓: Highlight option
    ←/→/[space]: Toggle selection
    a: Toggle all
    enter/return: Complete answer
◉   CanAddSpecialRoles - It is mandatory to proceed
◯   CanFreeze
◯   CanWipe
◯   CanPause
◯   CanTransferCreateRole
◯   CanChangeOwner
◯   CanUpgrade
✔ Are you sure that you want to proceed?
 › Yes

Transaction status: success
Transaction link: https://devnet-explorer.multiversx.com/transactions/cdef352e6d8cb5772b8e461b8255344479c7cf49aca02a3a1e57fd6495306c03

Issued collection token id: TSTONL-f40a25
```

The last mandatory command is `elven-tools nft-minter set-roles`. It will assign the obligatory role, which allows for new NFT tokens creation. Here there won't be any prompts, at least for now. Only a transaction will take the token data from the output.json file and assign the roles.

```bash
elven-tools nft-minter set-roles
Transaction: https://devnet-explorer.multiversx.com/transactions/b156ebc9f91a75c56ee5e1ae034c2e4ce09a9de16cde79f297221b457902e326
```

The following steps can be different on what you want to achieve. You can start minting directly or set up so-called 'drops' where you will define how many tokens will be minted in one drop. You can also always start or pause the minting process. What is necessary is that the contract will always mint randomly in all cases. Let's see how it looks when we want just to start the minting: `elven-tools nft-minter start-minting` and `elven-tools nft-minter mint` You will be asked to provide how many tokens you would wish to mint. Remember that the Smart Contract will have limits per one address. See how to check them later in this article.

```bash
elven-tools nft-minter start-minting
✔ Are you sure that you want to proceed?
 › Yes
⠼ Processing transaction...
Transaction: https://devnet-explorer.multiversx.com/transactions/8260437c4a2296169cf7bd925f135223529029ad8e1b3f2b535ee7f07ef3672c

elven-tools nft-minter mint
✔ Provide how many tokens should be minted.
Take into account possible limitations set on the Smart Contract (ex 3 for three tokens):
 … 2
✔ Are you sure that you want to proceed?
 › Yes
Transaction: https://devnet-explorer.multiversx.com/transactions/15194f779bebc31babdc7711f685a4bf0560c9a0484f6e644a40a1a0ee2f94ef
```

Check out examples of scenarios with all that possibilities: [Elven Tools workflows](/docs/elven-tools-workflows.html).

### Good to know

The Elven Tools CLI can list all the available commands for every subcommand. You can do: `elven-tools --help` or `elven-tools nft-minter --help`. You can always check the installed version by `elven-tools --version`.

Every step will update the `output.json` file. So, for example, the Smart Contract address will be put there. If you already deployed the Smart Contract without using the Elven Tools CLI, you can always configure it in the `.elventoolsrc` file using the config: `{ "nftMinterSc": { "deployNftMinterSC": "<sc_address_here>" } }`.

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
...and more, check `elven-tools nft-minter --help` for the whole list.

With them, you can get simple information written in the Smart Contract. You can also access them through API. Read more about it [here](https://docs.multiversx.com/sdk-and-tools/rest-api/virtual-machine).

Elven Tools also provides the Minter Dapp for the NFT launch, which strictly integrates with the Smart Contract. It have a lot of useful widgets.

### Where to go from here

- [CLI commands](/docs/cli-commands.html)
- [Recipes](/docs/recipes.html)
