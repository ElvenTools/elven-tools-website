---
layout: 'docs'
title: 'CLI Introduction'
publicationDate: '2022-01-26'
tags:
  - cli tool
excerpt: "The CLI tools is a standard Node CLI program which you can install using the npm package manager."
ogTitle: "Elven Tools CLI tool - introduction"
ogDescription: "The CLI tools is a standard Node CLI program which you can install using the npm package manager."
ogUrl: "https://www.elven.tools/docs/cli-introduction.html"
twitterTitle: "Elven Tools CLI tool - introduction"
twitterDescription: "The CLI tools is a standard Node CLI program which you can install using the npm package manager."
twitterUrl: "https://www.elven.tools/docs/cli-introduction.html"
githubUrl: "https://github.com/juliancwirko/elven-tools-website/edit/main/src/docs/cli-introduction.md"
---

The CLI tools is a standard Node CLI program which you can install using the npm package manager. It is best to install it globally by:

```bash
npm install elven-tools -g
```

### What is it?

- The CLI tool helps to:
  - deploy the NFT minter Smart Contract on the Elrond blockchain
  - interact with the NFT minter Smart Contract on the Elrond blockchain

For now it is designed to deploy the contract: [elven-nft-minter-sc](https://github.com/juliancwirko/elven-nft-minter-sc).

### How does it work? 

**General how to:**

- `npm install elven-tools -g`
- `elven-tools --version` or `elvent-tools -v`
- `elven-tools --help` or `elven-tools -h` - for getting the commands on the root level
- `elven-tools nft-minter --help` or `elven-tools nft-minter -h` - for getting all the commands for the subcommand

**Steps for deploying and interacting with the Smart Contract:**

Be aware that, by default, all will happen on the devnet. See below how to change it. Also check out the [Jump start section](/docs/jump-start.html).

First steps:

1. `elven-tools derive-pem` - you would need to generate the PEM file for all further operations, do not share it with anyone. It works similar to `erdpy wallet derive`. It will take the keyphrase and generate the `walletKey.pem` file in the same directory.
2. `elven-tools deploy nft-minter` - by default, the tools will take the abi and wasm source code and deploy directly from the defined tag branch of the smart contract. There are two options to work with it, though. You can configure a different branch or tag, or you can download the files and work on them locally.
  - For changing the branch, for example to `development` create the `.elventoolsrc` file in the same directory where the `walletKey.pem` file is located, put there `{ "nftMinter": { "version": "development" } }`. It can be also a tag name of the release in this [GitHub repository](https://github.com/juliancwirko/elven-nft-minter-sc).
  - If you would like to work locally. For example, you cloned the Smart Contract and worked on your version. You can create a directory structure next to the `walletKey.pem`. It should look like: `sc/nft-minter`. Here you will need to put the .wasm and .abi.json files which you can get from the [output]() directory of the Smart Contract.
  - This command takes a couple of arguments asking for them with prompts.
3 When the Smart Contract (check it in the explorer) is deployed, you need to create your collection token. You can do this by `elven-tools nft-minter issue-collection-token`. You will be asked for the name and the ticker. Keep the name without spaces and the ticker short and capitalized.
4. Next step would be to add a 'create' role. You can do this by `elven-tools nft-minter set-roles`
5. Then you would need to call at least once the `elven-tools nft-minter shuffle` to choose the first index to mint.
6. Then you can start the minting `elven-tools nft-minter start-minting` or setup a drop `elven-tools nft-minter set-drop` where the minting will be split into 'waves'. The first version of the Smart Contract mints randomly on demand and sends the NFT to the buyer. More advanced logic will land in version 2.
7. You can also mint the tokens using the same or different `walletKey.pem` for that run `elven-tools nft-minter mint`.
8. You can list all the commands using `elven-tools nft-minter --help`; below, you'll find all of them with short descriptions.

Check all commands [here](/docs/cli-commands.html)

### Custom configuration options

Below is an example of a `.elventoolsrc` config file with default values. You don't have to change the `config.ts` file. It is for library usage. `.elventoolsrc` is the only config file that should be used. It is not required if you will work on the devnet with the defined tag branch of the Smart Contract. In other cases, you would need to have it. It should be located in the same directory from which the `elven-tools` commands are triggered—the same directory as the one where the `walletKey.pem` file is located.

```json
{
  "chain": "devnet",
  "customProxyGateway": "https://devnet-gateway.elrond.com",
  "nftMinter": {
    "version": "{tag version here or branch name, for example: v1.2.0}",
    "deployGasLimit": 120000000,
    "issueCollectionTokenGasLimit": 80000000,
    "issueValue": "0.05",
    "assignRolesGasLimit": 80000000,
    "issueTokenFnName": "issueToken",
    "setLocalRolesFnName": "setLocalRoles",
    "mintBaseGasLimit": 14000000,
    "tokenSelingPrice": "",
    "mintFnName": "mint",
    "giveawayBaseGasLimit": 11000000,
    "giveawayFnName": "giveaway",
    "setDropFnName": "setDrop",
    "setUnsetDropGasLimit": 12000000,
    "unsetDropFnName": "unsetDrop",
    "pauseUnpauseGasLimit": 5000000,
    "pauseMintingFnName": "pauseMinting",
    "unpauseMintingFnName": "startMinting",
    "setNewPriceGasLimit": 5000000,
    "setNewPriceFnName": "setNewPrice",
    "shuffleFnName": "shuffle",
    "shuffleGasLimit": 6000000,
    "getTotalTokensLeftFnName": "getTotalTokensLeft",
    "getProvenanceHashFnName": "getProvenanceHash",
    "getDropTokensLeftFnName": "getDropTokensLeft",
    "getNftPriceFnName": "getNftPrice",
    "getNftTokenIdFnName": "getNftTokenId",
    "getNftTokenNameFnName": "getNftTokenName",
    "getMintedPerAddressTotalFnName": "getMintedPerAddressTotal",
    "getTokensLimitPerAddressTotalFnName": "getTokensLimitPerAddressTotal",
    "getMintedPerAddressPerDropFnName": "getMintedPerAddressPerDrop",
    "getTokensLimitPerAddressPerDropFnName": "getTokensLimitPerAddressPerDrop",
    "changeBaseCidsFnName": "changeBaseCids",
    "changeBaseCidsGasLimit": 5000000,
    "setNewTokensLimitPerAddressFnName": "setNewTokensLimitPerAddress",
    "setNewTokensLimitPerAddressGasLimit": 5000000,
    "claimScFundsFnName": "claimScFunds",
    "claimScFundsGasLimit": 6000000,
    "populateIndexesBaseGasLimit": 5000000,
    "populateIndexesMaxBatchSize": 5000,
    "populateIndexesFnName": "populateIndexes"
  }
}
```

**Whole config with default values:** [config.ts](https://github.com/juliancwirko/elven-tools-cli/blob/main/src/config.ts)

Remember, you don't have to change the `config.ts` file. It is for library usage. You don't have to clone the repository to change the configuration. `.elventoolsrc` is the only config file that should be used.

### CLI for a buyer

You can also use the CLI tool when you are only a buyer, not an owner of the Smart Contract. To do so, you would need to go through 4 steps.

1. Install the CLI: `npm install elven-tools -g`
2. Derive the PEM file of your wallet: `elven-tools derive-pem` You would need to pass your seed phrase here. No worries, you work on your computer. If it is safe, nothing leaves it because of the CLI too. Never share seed phrases and PEM files with anyone.
3. Create a configuration file in the same directory as the generated walletKey.pem file. The configuration file should be named `.elventoolsrc`. Inside add:

```
{
  "nftMinterSc": {
    "deployNftMinterSC": "<nft_minter_smart_contract_address_here>",
    "tokenSelingPrice": "<price_of_the_nft_here>"
  }
}
```

You would need only these two settings to be able to buy. Of course, the contract owner should prepare everything and start the minting process.

The `tokenSelingPrice` here is a format with 18 zeros. So 1 EGLD is 1000000000000000000.
The `deployNftMinterSC` here is an address of the contract. The owner should share it.

4. The last would be to call the mint command: `elven-tools nft-minter mint`. You will be asked about the number of tokens to mint. There will be limits. You would know them. You can [query the contract to check them](/docs/sc-endpoints.html#smart-contract-queries).

### Limitations and caveats

- there are main limitations related to the Smart Contract. Remember that it is most likely that this CLI tool won't be used only in a way that everyone would want to, be aware that you can always change the names of the endpoints in the Smart Contract. Then you can also use the config file and change them here in the CLI
- Smart Contract in version 1 doesn't have many mechanisms which will strongly limit unwanted behaviors. It only implements random minting, but in version 2, there will be more mechanisms for fair launches.

### Issues and ideas

Please post issues and ideas [here](https://github.com/juliancwirko/elven-tools-cli/issues).

### Contact

- [Telegram](https://t.me/juliancwirko)
- [Twitter](https://twitter.com/JulianCwirko)
- julian.cwirko@gmail.com