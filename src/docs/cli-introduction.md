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

For now it is designed to deploy the contract: [elven-nft-minter-sc](https://github.com/ElvenTools/elven-nft-minter-sc).

### How does it work? 

**General how to:**

- `npm install elven-tools -g`
- `elven-tools --version` or `elvent-tools -v`
- `elven-tools --help` or `elven-tools -h` - for getting the commands on the root level
- `elven-tools nft-minter --help` or `elven-tools nft-minter -h` - for getting all the commands for the subcommand

**Steps for deploying and interacting with the Smart Contract:**

Check the detailed steps here: [Jump start section](/docs/jump-start.html).

Be aware that, by default, all will happen on the devnet. See [here](/docs/recipes.html#how-to-use-the-configuration-file) how to change it.

Check all commands [here](/docs/cli-commands.html)

### Custom configuration options

**All of the configuration options are set by default, so you don't have to configure them if you will accept the defaults.**

Below is an example of a `.elventoolsrc` config file with default values. You don't have to change the `config.ts` file. It is for library usage. `.elventoolsrc` is the only config file that should be used. It is not required if you will work on the devnet. In other cases, you would need to have it. It should be located in the same directory from which the `elven-tools` commands are triggered—the same directory as the one where the `walletKey.pem` file is located.

```json
{
  "chain": "devnet",
  "apiProviderEndpoint": "https://devnet-api.elrond.com",
  "gatewayProviderEndpoint": "https://devnet-gateway.elrond.com",
  "nftMinterSc": {
    "version": "{tag version here or branch name, for example: v1.2.0}",
    "deployNftMinterSC": "<nft_minter_smart_contract_address_here> when you want to switch between chains or you want to use the cli as buyer",
    "tokenSelingPrice": "<price_of_the_nft_here> when you want to switch between chains or you want to use the cli as buyer",
    "deployGasLimit": 120000000,
    "issueCollectionTokenGasLimit": 80000000,
    "issueValue": "0.05",
    "assignRolesGasLimit": 80000000,
    "issueTokenFnName": "issueToken",
    "setLocalRolesFnName": "setLocalRoles",
    "mintBaseGasLimit": 12500000,
    "tokenSellingPrice": "",
    "mintFnName": "mint",
    "giveawayBaseGasLimit": 12500000,
    "giveawayFnName": "giveaway",
    "setDropFnName": "setDrop",
    "setUnsetDropGasLimit": 5000000,
    "unsetDropFnName": "unsetDrop",
    "pauseUnpauseGasLimit": 4500000,
    "pauseMintingFnName": "pauseMinting",
    "unpauseMintingFnName": "startMinting",
    "setNewPriceGasLimit": 4500000,
    "setNewPriceFnName": "setNewPrice",
    "shuffleFnName": "shuffle",
    "shuffleGasLimit": 5000000,
    "getTotalTokensLeftFnName": "getTotalTokensLeft",
    "getProvenanceHashFnName": "getProvenanceHash",
    "getDropTokensLeftFnName": "getDropTokensLeft",
    "getNftPriceFnName": "getNftPrice",
    "getNftTokenIdFnName": "getNftTokenId",
    "getNftTokenNameFnName": "getNftTokenName",
    "getCollectionTokenNameFnName": "getCollectionTokenName",
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
    "allowlistBatchSize": 320,
    "populateAllowlistFnName": "populateAllowlist",
    "populateAllowlistBaseGasLimit": 6000000,
    "getAllowlistFnName": "getAllowlistSize",
    "isAllowlistEnabledFnName": "isAllowlistEnabled",
    "getAllowlistAddressCheckFn": "getAllowlistAddressCheck",
    "enableAllowlistFnName": "enableAllowlist",
    "disableAllowlistFnName": "disableAllowlist",
    "enableDisableAllowlistGasLimit": 6000000,
    "isDropActiveFunctionName": "isDropActive",
    "tokensPerOneTx": 95,
    "clearAllowlistFnName": "clearAllowlist",
    "clearAllowlistBaseGasLimit": 5000000,
    "removeAllowlistAddressFnName": "removeAllowlistAddress",
    "removeAllowlistAddressLimit": 5000000,
    "isMintingPausedFnName": "isMintingPaused",
    "getTotalSupplyFnName": "getTotalSupply",
    "getTotalSupplyOfCurrentDropFnName": "getTotalSupplyOfCurrentDrop"
  },
  "minterDapp": {
    "version": "{tag version here, for example: v1.0.3}"
  },
  "collectionNftOwners": {
    "apiCallsPerSecond": 5
  }
}
```

**Whole config with default values:** [config.ts](https://github.com/ElvenTools/elven-tools-cli/blob/main/src/config.ts)

Remember, you don't have to change the `config.ts` file. It is for library usage. You don't have to clone the repository to change the configuration. `.elventoolsrc` is the only config file that should be used.

### Limitations and caveats

- there are main limitations related to the Smart Contract. Remember that it is most likely that this CLI tool won't be used only in a way that everyone would want to, be aware that you can always change the names of the endpoints in the Smart Contract. Then you can also use the config file and change them here in the CLI
- Smart Contract in version 1 doesn't have many mechanisms which will strongly limit unwanted behaviors. It only implements random minting, but in version 2, there will be more mechanisms for fair launches.

### Issues and ideas

Please post issues and ideas [here](https://github.com/ElvenTools/elven-tools-cli/issues).

### Contact

- [Telegram](https://t.me/juliancwirko)
- [Twitter](https://twitter.com/JulianCwirko)
- julian.cwirko@gmail.com