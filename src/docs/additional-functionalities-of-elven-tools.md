---
layout: 'docs'
title: 'Additional functionalities of Elven Tools'
publicationDate: '2022-07-24'
tags:
  - articles
excerpt: "The CLI also has some additional tools and there are also separated helper scripts. Let's see what we have here."
ogTitle: "Additional functionalities of Elven Tools"
ogDescription: "The CLI also has some additional tools and there are also separated helper scripts. Let's see what we have here."
ogUrl: "https://www.elven.tools/docs/additional-functionalities-of-elven-tools.html"
twitterTitle: "Additional functionalities of Elven Tools"
twitterDescription: "The CLI also has some additional tools and there are also separated helper scripts. Let's see what we have here."
twitterUrl: "https://www.elven.tools/docs/additional-functionalities-of-elven-tools.html"
---

Elven Tools CLI is mainly used to simplify and help when deploying and interacting with the Elven Tools smart contract. Read more about that here: [Elven Tools workflows](https://www.elven.tools/docs/elven-tools-workflows.html).
It is its main functionality. But the CLI also has some additional tools and there are also separated helper scripts. Let's see what they are.

### Get NFT owners

First, let's start with the Elven Tools CLI. It has interesting tools built in. For example, you can get the owners of an NFT collection by using `elven-tools collection-nft-owners`. It allows you to filter out the addresses of the smart contracts and filter by metadata/asset file name if needed. It will output the `nft-collection-owners.json` file, which you could use in two complementary tools, and also it is used in token distribution. You will read about everything below. For more docs about the `collection-nft-owners` command, check the section in the docs: [How to get owners' addresses using the collection ticker](https://www.elven.tools/docs/recipes.html#how-to-get-owners-addresses-using-the-collection-ticker).

### Filter and convert to CSV

Ok, what can you do with the `nft-collection-owners.json`? First, you can do more data processing and convert it to CSV using: [elven-tools-collection-owners-csv](https://github.com/ElvenTools/elven-tools-collection-owners-csv) (check the repository for docs). You can filter the JSON file by the token id or/and file name and get a formatted CSV file. It is convenient for all data processing where the CSV is required. You will find an example [here](https://github.com/ElvenTools/elven-tools-collection-owners-csv/tree/main/data). 

### Get long-term owners

Another one is the [elven-tools-snapshots-intersection](https://github.com/ElvenTools/elven-tools-snapshots-intersection) which can be used to filter long-term holders (check the repository for docs). As an input, it takes multiple `nft-collection-owners.json`, and it will create one JSON file with addresses that exist in each `nft-collection-owners.json` file. The address in each list can be considered the long-term holder. So you can do numerous snapshots first and then filter long-term holders. You will find an example [here](https://github.com/ElvenTools/elven-tools-snapshots-intersection/tree/main/data).

### Distribute tokens to owners

The most exciting part is the distribution functionality. It is built into the CLI and uses the `nft-collection-owners.json` file as input. It will let you define the type of tokens to distribute and the amount per address, and it will send them automatically to the addresses from the JSON file. You can run it by `elven-tools distribute-to-owners`. You will read more about it in the docs: [How to distribute tokens to NFT owners](https://www.elven.tools/docs/recipes.html#how-to-distribute-tokens-to-nft-owners).

### Dapp initialization

The last but not least functionality not directly related to the NFT minting is the Dapp initialization. You can use the `elven-tools init-dapp` command to download, install dependencies and prepare env files for the Nextjs-based application, which is used as a frontend for the minting process. You can read more about the Dapp here: [Minter Dapp introduction](https://www.elven.tools/docs/minter-dapp-introduction.html).

### Summary

There will be more tools related to the PFP NFT collections handling. There are also planned new smart contracts, so stay tuned. And if you want a similar CLI tool, but more general, not specific to the NFTs, please check the [Buildo Begins](https://github.com/ElrondDevGuild/buildo-begins). It is a tool to simplify common operations on the Elrond blockchain and also a couple of helper tools. Like generating the herotag or using Elrond data converters.
