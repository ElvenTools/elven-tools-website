---
layout: "docs"
title: "Recipes"
publicationDate: "2022-01-25"
tags:
  - intro
excerpt: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
ogTitle: "Elven Tools CLI tool - recipes"
ogDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
ogUrl: "https://www.elven.tools/docs/recipes.html"
twitterTitle: "Elven Tools CLI tool - recipes"
twitterDescription: "The Elven Tools includes the Smart Contract, CLI tool, and Minter Dapp for NFT launches. Every part of it can be used as a separate tool."
twitterUrl: "https://www.elven.tools/docs/recipes.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/recipes.md"
---

Here are ready-to-use recipes and more information on real-life use cases.

### How to work with the Smart Contract locally

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

As you can see, we have the `.abi.json` and `.wasm` files there. You will find them in the `output` directory after building the Smart Contract locally, and the elven-tools cli tool will take them by default. Remember to only keep the same naming convention for the directories - `sc/nft-minter`.

If you need some help working with the Smart Contract in the Elrond ecosystem, please check docs and my article [here](https://www.julian.io/articles/elrond-smart-contracts.html).

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/TivnKJsyLH8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### How to use the configuration file

The configuration file is optional, and you don't need it until you want to change the chain or the Smart Contract source. Plus, maybe after some modifications, you would like to change the functions names and gas limit. All default values are defined [here](https://github.com/ElvenTools/elven-tools-cli/blob/main/src/config.ts), and below, you'll find the example of how to overwrite them from outside of the lib itself.

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

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/UlyTVa6oLuM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Mainnet deployments

**Important!** The same way as in the example above, you can configure deployment to `mainnet`. Please remember about a couple of things:
- make sure that you derive the walletKey.pem file from the seed from the mainnet wallet. Make sure that the computer you are using is safe, and no one will take the PEM file from you. Or/and seed phrase,
- change the `chain` in the config file to the `mainnet`,
- be careful with Smart Contract versions. By default, the latest version of the CLI will use the newest version of the Smart Contract. Remember that if you have .wasm and .abi files in the `sc/nft-minter` directory, then they will be used instead of the ones from the repository,
- test the whole process 'million' times on the devnet, test with small amounts and big amounts, with multiple wallets as buyers, test queries and transactions, buy to the limits, to test them too,
- **I can't provide individual support**, but I will always try to help.

### Custom API endpoints

It is always advisable to use the custom API endpoints custom proxies for production-ready apps. Even with this tool, it is better to use the custom one. You can read more about how to set up your architecture [here](https://docs.elrond.com/integrators/observing-squad/).

Suppose you don't have the resources to do that. You can find third-party services which do that as a service.

To switch to your custom API endpoint, you would need to add in your `.elventoolsrc` configuration file:

```
{
  "chain": "devnet",
  "apiProviderEndpoint": "https://devnet-api.elrond.com"
}
```

It is an example of the default API endpoint for the devnet. You can do the same for the testnet and mainnet.

When you need to use the Gateway instead API, you can configure it like that:

```
{
  "chain": "devnet",
  "gatewayProviderEndpoint": "https://devnet-gateway.elrond.com"
}
```

It is an example with the default Gateway endpoint for the devnet. You can do the same for the testnet and mainnet.

Important! When nothing is provided, the CLI will use the default, public Elrond API endpoint (api.elrond.com, devnet-api.elrond.com, testnet-api.elrond.com). When the `gatewayProviderEndpoint` is set, it will always overwrite the `apiProviderEndpoint`.

### How to use allowlist

The allowlist is usually required for the first batch of tokens to distribute them only to chosen addresses. It can be a list of eligible addresses.

There are three endpoints and commands which help with that. First you would need to have the listof addresses.

Then you need a file called `allowlist.json` in the root directory. It should have the list of addresses in such a form:

```json
[
  "erd1.......",
  "erd1.......",
  "erd1.......",
  "erd1.......",
]
```

There should be a maximum of 320 addresses per transaction. You can make a couple of transactions if you need to. But remember to update the file on each.

You can populate the list without the file, then the CLI will request it through a prompt where you need to provide them one by one, separated using a comma.

Let's see what it looks like in both cases:

Example:
```bash
elven-tools nft-minter populate-allowlist
 
Populating addresses from the allowlist.json file: 
 
✔ Are you sure that you want to proceed?
 › Yes
Transaction: https://devnet-explorer.elrond.com/transactions/4a3b63edc1cf00c8025c025926db033964e4625fa5ddcd316b880787f3c8094f
```

Example:
```bash
elven-tools nft-minter populate-allowlist
 
There is no allowlist.json file with the addresses.
You will be providing addresses by hand.
 
✔ Are you sure that you want to proceed?
 › Yes
✔ Provide the list of addresses. Max 320 addresses per one transaction.
You can add more by sending more transactions. Separate them with comma (","):
 … erd1puseeussfftajfj92ezqtfp0ca6u0s2thu7n64cyw6m37ef8dh0sekwt27, erd18yxxeuf2fkwlwgrnc3chjyf4gl3429qpp5fqynhzf2gn6hs3h8dqu7zt7n
Transaction: https://devnet-explorer.elrond.com/transactions/f8bf7de010629e32008bebb1ba5681a008f23afaf949e0e565ea3bbf41bd80fd
```

Remember that you will always need to enable the allowlist after populating it. Otherwise, it will be ignored. You can enable and disable it using: `elven-tools nft-minter enable-allowlist` and `elven-tools nft-minter disable-allowlist`.

You can also use a couple of SC queries. This allows to get the current size of the allowlist, check if the address is there, or check if the allowlist is enabled. These are:

```
elven-tools nft-minter get-allowlist-size
elven-tools nft-minter is-allowlist-enabled
elven-tools nft-minter get-allowlist-address-check
```

You will be able to clear the allowlist with:
```
elven-tools nft-minter clear-allowlist
```

It will clear the whole allowlist because the process is quite heavy. The best is to keep max 1300 addresses in the allowlist at a time. Of course, if only you plan to clear it later. If you keep more and want to clear it, you can reach the gas limit for a transaction. So it would be best to split the allowlist per drop, keep it as small as possible and clear it each time.

You can also remove a single address by:
```
elven-tools nft-minter remove-allowlist-address
```

Remember that you can always use the functionality without using the CLI tool, then you would need to call the same endpoints. You will find all commands for the CLI [here](/docs/cli-commands.html) and all SC endpoints [here](/docs/sc-endpoints.html). Also, check the longer article about [possible workflows](/docs/elven-tools-workflows.html).

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/rdg6s7KHFt0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### How to use drops

The drops are, in simple words, batches of tokens to mint. You don't have to use them, but it is usually required because most projects usually split the collection into 'waves' of distribution.

Now let's see how to define a drop in which we will mint only 2500 of the whole 10k collection. You would need to use `elven-tools nft-minter set-drop` when using the CLI tool. You will be asked to provide how many tokens per drop it should mint. After that, it will pause the minting process. You can also pause the minting at any time you want by `elven-tools nft-minter pause-minting`. You can also unset the drop by `elven-tools nft-minter unset-drop`. You'll find all the commands [here](/docs/cli-commands.html).

Example:
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

There are also SC queries that allow checking a couple of things. These are: 

```
elven-tools nft-minter get-drop-tokens-left
elven-tools nft-minter get-minted-per-address-per-drop
elven-tools nft-minter get-tokens-limit-per-address-per-drop
elven-tools nft-minter is-drop-active
```

They are self-explanatory, but you will find all descriptions under the links below.

Remember that you can always use the functionality without using the CLI tool, then you would need to call the same endpoints. You will find all commands for the CLI [here](/docs/cli-commands.html) and all SC endpoints [here](/docs/sc-endpoints.html). Also, check the longer article about [possible workflows](/docs/elven-tools-workflows.html).

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/ZERCb-c-BP4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### How to use the giveaway

The `giveaway` functionality is helpful when you want to give some tokens to a particular address. It can be because they are the team members or someone you want to thank. Remember that with Elven Tools, you can't choose the specific token. It will still be randomly selected and minted. When using this functionality, there is no payment—only transaction fees.

You can give some tokens using the CLI's command `elven-tools nft-minter giveaway`. You would need to provide the address to which you would like to send the NFTs and the amount of the tokens to give.

You can provide addresses by hand in the CLI prompt, separating them from the coma. But you can also provide the file: `giveaway.json`. The structure looks like this:

```json
[
  "erd1...",
  "erd1...",
  "erd1...",
]
```

You can use this even when the minting process is paused, which is usable for the giveaway before the official minting is started.

As always, you can call the giveaway endpoint without the CLI. Check them in the SC endpoints section.

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/lQUVEd-9ZhA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### How to claim dev rewards

In the Elrond ecosystem, each Smart Contract will get the share of the fees as a development reward. So the developer of the contract will get some share because this is an open source Smart Contract. It will generate these rewards for everyone who deploys it. You can claim them by using: `elven-tools nft-minter claim-dev-rewards`. Remember that this will only work for the owner of the Smart Contract.

As always, you can call the giveaway endpoint without the CLI. Check them in the SC endpoints section.

### How to claim royalties and other funds

The Smart Contract is payable by default, so in theory, it is possible to transfer EGLD funds to its address. By definition, this is how marketplaces should send the royalties. There is an `elven-tools nft-minter claim-sc-funds`, which will allow getting all the funds locked on the contract. Of course, only for the owner of the contract.

There will also be a dedicated endpoint/command which will call the marketplaces Smart Contracts to claim the royalties because not all of them will send them automatically.

As always, you can call the giveaway endpoint without the CLI. Check them in the SC endpoints section.

### How to get owners addresses using the collection ticker

From version 1.6.0 there is additional command `elven-tools collection-nft-owners`. It will allow getting owners' addresses, using only the collection ticker. It is useful, for example, when you want to do some promotional giveaway. The functionality will save the addresses in the `nft-collection-owners.json` where the command is triggered.

Additionally, you can also filter by metadata JSON file name. It is an optional step.

**Important**: It will work only with the API endpoint, not the gateway. Elven Tools CLI, by default, uses the API endpoint. So it should work by default, but you need to remember that.

How to use it? You need to use at least version 1.6.0 of the CLI. You can check it by `elven-tools -v`, and you would need to use the command `elven-tools collection-nft-owners`. Then there are prompts. You would need to provide the collection ticker and answer two questions about whether you want to filter smart contract addresses.

Because of how the API works, we need to do calls with a max size of 100 items. Here we also have calls that are limited to 5 per second. You can change this limit in the configuration file. Check how [here](/docs/cli-introduction.html#custom-configuration-options). If you need to change this setting, in the config file, there should be an entry:

```
{
  "chain": "mainnet",
  "collectionNftOwners": {
    "apiCallsPerSecond": 5
  }
}
```

When is the address not unique? It is when one address will have more than one NFT token from the collection. See the example below:

```
elven-tools collection-nft-owners
✔ Provide the collection ticker
 … EAPES-8f3c1f
✔ Do you want to exclude smart contract addresses?
 › Yes
✔ Do you want to filter by metadata JSON file name? Provide names without the extension separated by a comma (example: 123,555,9999) [you can ommit that, just confirm empty]
 … 
There are 10000 tokens in that collection.
Done, 1042 addresses saved. Without smart contract addresses.
```

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/4vM_y25uaq8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

**You can also do filtering by metadata JSON filename:**

```
elven-tools collection-nft-owners

✔ Provide the collection ticker
 … EGG-6ee076
✔ Do you want to include only unique addresses?
 › No
✔ Do you want to exclude smart contract addresses?
 › No
✔ Do you want to filter by metadata JSON file name? Provide names without the extension separated by a comma (example: 123,555,9999) [you can ommit that, just press enter]
 … 1390,827

There is 1000 tokens in that collection.
Done, 2 addresses saved.
```

If you are interested in generating a **CSV** file, you can use the [elven-tools-collection-owners-csv](https://github.com/ElvenTools/elven-tools-collection-owners-csv) script, which will do that. The input file is the output of the `elven-tools collection-nft-owners`. You'll find the input and output examples in the [data](https://github.com/ElvenTools/elven-tools-collection-owners-csv/tree/main/data) folder.

### How to distribute tokens to NFT owners

From version 1.12.1, it is possible to automatically reuse the `nft-collection-owners.json` so the output from the `elven-tools collection-nft-owners` and distribute EGLD, ESDT, SFT or MetaESDT tokens to the collection NFT owners.

The functionality is based on the currently used PEM key file. It works without connection to the NFT minter smart contract or any other custom smart contract.

You can use it with any PEM wallet file. You can also do this not only with your collection.

How does it work?

1. You need to run the `elven-tools collection-nft-owners` and generate the `nft-collection-owners.json` as in the section above.
2. You would need to run the `elven-tools distribute-to-owners` command.
3. Choose the token type (EGLD, ESDT, SFT, MetaESDT)
4. Provide the token id in case of ESDT or MetaESDT
5. Provide the amount per address

After all, you will get the `distribution-log.json` with all transactions, addresses, and status. 

Remember that you need to be sure that you use the proper chain type (devnet, testnet, mainnet) and that you have an adequate amount of the token on the wallet corresponding to the PEM file. Use `elven-tools derive-pem` to derive the PEM file.

To change the chain type, use the configuration file. Create a `.elventoolsrc` config file and add:

```json
{
  "chain": "mainnet"
}
```

There is a rate limit when distributing the tokens. It is five calls per second. You can increase that by using the configuration file, add:

```json
{
  "distributeToOwners": {
    "apiCallsPerSecond": 5
  }
}
```

Check [here](/docs/recipes.html#how-to-use-the-configuration-file) how to work with the config file.

From version 1.15.2, you can use an optional multiplier functionality. When distributing the amount will be multiplied by the number of NFTs owned by an address.

Alternatively, if you haven't used the `elven-tools collection-nft-owners` to generate the `nft-collection-owners.json` and have addresses from some other source, then you can prepare a file with the same name and the same structure. You can omit 'tokens' and 'tokensCount' there. It should still work. The structure will be:

```json
[
  { "owner": "erd1....", "tokensCount": 3 },
  { "owner": "erd1....", "tokensCount": 1 },
  { "owner": "erd1....", "tokensCount": 1 }
]
```

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/SreoFeyOUPY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

```bash
elven-tools distribute-to-owners

✔ What do you want to distribute? Choose the token type.
 › EGLD
✔ Please provide the amount of the EGLD to send per one address (ex. 1 is 1 EGLD)
 … 1
? You can multiply the amount to distribute by the number of NFTs tokens owned. Do you want to do that? › - Use arrow-keys. Return to submit.
❯   No
    Yes
```

### CLI for a buyer

You can also use the CLI tool when you are only a buyer, not an owner of the Smart Contract. To do so, you would need to go through 4 steps.

1. Install the CLI: `npm install elven-tools -g`
2. Derive the PEM file of your wallet: `elven-tools derive-pem` You would need to pass your seed phrase here. No worries, you work on your computer. If it is safe, nothing leaves it because of the CLI too. Never share seed phrases and PEM files with anyone.
3. Create a configuration file in the same directory as the generated walletKey.pem file. The configuration file should be named `.elventoolsrc`. Inside add:

```
{
  "nftMinterSc": {
    "deployNftMinterSC": "<nft_minter_smart_contract_address_here>",
    "tokenSellingPrice": "<price_of_the_nft_here>"
  }
}
```

You would need only these two settings to be able to buy. Of course, the contract owner should prepare everything and start the minting process.

The `tokenSellingPrice` here is a format with 18 zeros. So 1 EGLD is 1000000000000000000.
The `deployNftMinterSC` here is an address of the contract. The owner should share it.

4. The last would be to call the mint command: `elven-tools nft-minter mint`. You will be asked about the number of tokens to mint. There will be limits. You would know them. You can [query the contract to check them](/docs/sc-endpoints.html#smart-contract-queries).

### What is an output.json file

The `output.json` file will be created as temporary storage, which keeps the created Smart Contract address, the information about the collection token, and the token price. It is required in further operations. This file is created automatically when deploying the Smart Contract using the CLI. So it is mostly there for the owner of the Smart Contract. It looks like that: 

```json
{
  "nftMinterScAddress": "erd1qqqqqqqqqqqqqpgq7a0cq90r2kqymtaqysxp7umrcyp04jgmgtkscelhmp",
  "nftMinterScCollectionSellingPrice": "1000000000000000"
}
```

You don't have to think about it much.

### Why do we need the shuffle endpoint

The endpoint will set the following index to mint. It is important here that it will randomly select it from the indexes left to mint. This endpoint is also public, so everyone can call the transaction and change the following index to mint. It assures that the process is random, and everyone can impact that.

When using the CLI you can always run `elven-tools nft-minter shuffle`.