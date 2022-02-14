---
layout: 'docs'
title: 'Elven Tools workflows'
publicationDate: '2022-01-25'
tags:
  - articles
excerpt: "How exactly should one work with the Elven Tools? Let's see the options and how you could sell and distribute your NFTs."
ogTitle: "Elven Tools workflows"
ogDescription: "How exactly should one work with the Elven Tools? Let's see the options and how you could sell and distribute your NFTs."
ogUrl: "https://www.elven.tools/docs/elven-tools-workflows.html"
twitterTitle: "Elven Tools workflows"
twitterDescription: "How exactly should one work with the Elven Tools? Let's see the options and how you could sell and distribute your NFTs."
twitterUrl: "https://www.elven.tools/docs/elven-tools-workflows.html"
---

Many possible endpoints on the [Smart Contract](/docs/sc-introduction.html). There is also a lot of documentation [here](/docs/jump-start.html) and [there](/docs/cli-introduction.html). But how exactly should one work with the Elven Tools? Let's see the options and how you could sell and distribute your NFTs.

### What we will tackle here

1. What you can do and what you can't do with the first version of Elven Tools.
2. Examples of the scenarios and how to configure them.

All scenarios can be modified and improved. These are probably the most often used scenarios on how to run the collection using Elven Tools.

### What is possible and what's not

The first version of the Smart Contract works on the trendy principle of a 'candy machine'. You can read more about it here: [Tips on buying NFTs on the Elrond blockchain](/docs/tips-on-buying-nfts-on-the-elrond-blockchain.html). 

In general, you pay, and you get randomly selected NFT. In the article linked above, you will find some more thoughts about the pros and cons of such a solution, but here let's focus on exactly what you can do and what you can't.

**You can:**
- you can receive the EGLD, randomly mint the NFT and send it to the buyer
- you can split the whole collection into minting 'waves', called 'drops' here
- you can give away tokens to chosen addresses (this is also randomly minted)
- you can prepare an 'allowlist' and allow only eligible addresses to mint, then you can enable or disable it at any given time
- you can start and pause the minting at any given time
- you can change prices at any given time (of course should be appropriately planned and communicated)
- you can change the tokens limit per one address at any given time in total
- you can claim royalties sent to the Smart Contract from a marketplace
- you can claim the developer rewards (as an owner of the Smart Contract, you will get the rewards too, it is 30% of the fee of each Smart Contract call)

**You can't:**
- you can't postpone sending the NFT token to the buyer's wallet
- you can't send the NFT token with hidden assets
- you can't take other currency than EGLD (at least for now, there are plans to implement that)
- you can't disable the random minting functionality - it is essential for fair distribution

There is another version of the contract planned, or it is better to say, a new Smart Contract that will implement another approach to fair distribution. You can read about it in the article linked above. Ok, enough theory, let's see the practical scenarios to use.

### Examples of scenarios 

Please keep in mind that these are only my ideas, you don't have to do this that way, and you can mix all possible endpoint calls to achieve your perfect flow. These are just examples to explain why all the endpoints are there. I will also describe how to prepare all of that using the Elven Tools CLI because it is simpler and faster. But you could also prepare the Smart Contract without it, for example, using [erdpy](https://docs.elrond.com/sdk-and-tools/erdpy/erdpy).

**Let's list all of my ideas on how we can do this first:**

1. Simple minting - all at once.
2. Simple minting with allowlist - all at once with allowlist.
3. Minting is divided into drops with different prices.
4. Minting with a giveaway.
5. A little bit of everything.

Remember that all of the described below transactions are owner only, which means that the only owner of the Smart Contract can run it. So the wallet which deploys the Smart Contract.

**Simple minting - all at once**

Elven Tools allows mint without configuring other stuff like allowlist, drops, etc. You need to go through the required steps after deployment and start the minting process. You'll find all info about how to deploy and configure initial stuff here: [Elven Tools Jumpstart](/docs/jump-start.html).

When you deployed and ran all required transactions, you will be able to start minting. Let's see how.

To start minting, you have to run the command:

```
elven-tools nft-minter start-minting
```

Of course, we assume that the Smart Contract is correctly deployed, the collection token is issued, it has proper roles, and the shuffle endpoint was called at least once. Again, you will find all about it here: [Elven Tools Jumpstart](/docs/jump-start.html). Please let me know if something there is still not clear. I will improve the docs.

That's it. Now your community can freely buy and mint the tokens till the end of the collection. You don't have to do anything more. Of course, you can still pause the minting:

```
elven-tools nft-minter pause-minting
```

And you can do whatever you need. You can even change the price. This isn't like you need to decide on one scenario. Remember about that. But for simplicity, I want to focus on examples.

Pros of such an approach:
- simplicity - you don't have to care about additional promotion and setup
- if a project is quite popular, the collection will be probably sold out in a couple of minutes or hours

Cons of such approach:
- you won't have many tools to build the community and hype around it,
- it can be heavy for your dapp, so it should be well prepared in such a case. Don't rely on public API or build the website with cache solutions. But generally, don't rely on public API if you can ;)

It is a straightforward scenario and probably not very often used. Let's see what more we can do.

**Simple minting - all at once with allowlist**

This scenario is the same as the one above. What is added here is the 'allowlist'. A list of prepopulated addresses on the Smart Contract will be the only ones that can mint if the 'allowlist' is enabled. Let's see what we need to make it happen.

First, you would need to populate the 'allowlist' with addresses. You can do this using the JSON file with a max of 250 addresses per one transaction or providing them by hand using a CLI prompt.

If you can, please prepare the `allowlist.json` file and put it in the `sc/nft-minter` relative to where you keep your walletKey.pem file and from where you run the `elven-tools` commands.

You need to run the command:

```
elven-tools nft-minter populate-allowlist
```

The CLI will detect it and ask you if you want to continue. 

If you have more than 250 addresses, please repeat the operation. Remember to replace old addresses with new ones in the allowlist.json file. If you send the same addresses again, nothing will happen, there is no way to have duplicates on the smart contract, but you will lose some EGLD on the transaction fees.

To provide addresses by hand, you would need to run the same command but remove or change the name of the `allowlist.json` file. Then the CLI will ask you to provide the addresses by hand. You can use commas to separate them.

When the list is populated, you need to enable the 'allowlist'. You can do this by running:

```
elven-tools nft-minter enable-allowlist
```

From now on, only eligible addresses can mint. You would probably handle it in your dapp, but generally, if someone tries to mint and their address isn't on the list, the transaction will fail.

You can disable the allowlist at any given time by:

```
elven-tools nft-minter disable-allowlist
```

Then standard minting starts, and every address can mint.

It is important that the 'allowlist' does not keep the information about how many tokens a particular address can mint. The Smart Contract will respect global settings, total limits per the whole collection, and limits per drop. These limits can be changed at any given time. Please refer to the [docs](/docs/cli-commands.html) on how to do that.

Ok, now we know how to use the 'allowlist' to promote and organize the presale for only eligible addresses.

Pros of such an approach:
- all the pros from the previous scenario
- allowlist lets you organize the presale. You can also change prices after allowlist is disabled

Const of such approach:
- all the cons from the previous scenario
- you need to handle this in your dapp not to confuse users. There are queries available on the Smart Contract, which will allow checking if the 'allowlist' is enabled and also to check if an address is on the list

**Minting divided into drops with different prices**

As I wrote before, you can mix all of the scenarios. You can also use the 'allowlist' here. Here let's focus only on the 'drops' functionality.

The 'drops' functionality is optional. You don't have to use these to mint/sell. It is useful to divide your process into 'waves' spread in time. You have 9999 tokens in a collection, and you would like to have three drops/waves of minting each of 3333 NFTs. You can prepare the whole marketing for that and also the price strategy.

What is essential here, and for many, it is a con of such a Smart Contract, is that when you distribute the first drop, it will for sure land on the second market. But it isn't always bad. You could check how prices form around that and adjust your fees for the next drop. Of course, it is better not to reveal prices for the following drops in such a case.

Ok, so how to configure these?

First, you would need to set the first drop:

```
elven-tools nft-minter set-drop
```

You will be asked how big is the drop, so with our example, it will be 3333 tokens, and what is the limit per one address per one drop. The limit per drop can be different than the total limit per collection, but it should always be smaller than the total limit. That's all that you need to do. Then you would need to start minting. After all 3333 tokens are sold, the Smart Contract will pause the minting process automatically. Of course, you would need to handle this on the dapp. Some queries will return how many tokens are already minted by drop and minted per one particular address. Please check all [here](/docs/cli-commands.html).

If needed, you can also unset/disable the actual drop.

```
elven-tools nft-minter unset-drop
```

You can also set another one at any time, which will overwrite the previous one. You won't select the amount bigger than tokens left to mint.

What is important here is the possibility to set different prices for every drop. When the drop is sold out, you can change the price without starting the minting:

```
elven-tools nft-minter set-new-price
```

Then when the time comes, you can just set a new drop and start minting. Or you can even begin minting without setting the next drop.

Pros of such a solution:
- all from the previous scenarios
- you will have a lot more control over the marketing and planning in time

Const of such solution:
- all from the previous scenarios
- it is simpler for a mistake. You could start at the wrong moment or begin with the old price. Of course, you can pause it at any given time, but some tokens could be minted already
- a lot of more planning is required and tests on the devnet

**Minting with giveaways**

The following interesting functionality is a `giveaway`. This is something which is used very often. It allows the operator to give randomly selected NFTs to any addresses they want. It could even be their address. Usually, it is used for marketing and rewarding in many different contests and lotteries in a project's community. 

You can use the giveaway endpoint at any given time. There will be no payment in this case. In most cases, it will probably be used initially, even before the process starts. But you can also use it in the middle of the process, but it is advisable to be careful when a drop is defined and active. It could affect the drop's final available amount of tokens if the drop is the last one, and there won't be any tokens left after using the giveaway. So use it at the beginning, the best even before the process starts or in between drops when the process is paused.

Ok, let's see how to use it:

```
elven-tools nft-minter giveaway
```

You will be asked to provide the addresses in the CLI prompt. You can give/mint the tokens in this special case even when the whole minting process is paused.

Remember that they will still be minted randomly. In the spirit of fair distribution, there is no way to choose a particular one to send.

Pros of such a scenario:
- all from the previous scenarios
- you will be able to thank anyone you need to thank and send them the NFTs for free

Cons of such scenario:
- some general cons from the previous scenarios
- basically, no additional cons if you are using it properly

###  A little bit of everything type scenario

In the last section of this article, I would like to focus on a custom scenario with which I would probably go.

For example, purposes let's say I have a collection of 3333 NFTs.

Let's start with a 'giveaway' process. I would probably prepare a list of addresses of people I want to thank. It could be a designer, or developer, or my friend. I would probably do this before even starting the whole process. Let's say I want to give 33 tokens at the beginning. I would use the `elven-tools nft-minter giveaway` command. So, now I have 3300 tokens left. I can check that using the query `elven-tools nft-minter get-total-tokens-left` can be run by everyone, not only by the owner of the Smart Contract.

The following step would be to prepare the 'allowlist'. I could get addresses from closed discord groups or Twitter, competitions, and lotteries. Preparation of such a list would probably take some time, so I could also prepare some marketing and social media communication. I can populate the Smart Contract storage with addresses when the list is ready. I would use the `elven-tools nft-minter populate-allowlist`. 

I will prepare the drop to be adequate to the 'allowlist' addresses when the list is in place. So, for example, if I would like to have three tokens per address per drop, and my 'allowlist' has 100 addresses, I would set the drop to 300 tokens max. 

<div class="docs-info-box">
<strong>Important!</strong> The first version of the allowlist is not clearable. All added addresses will always stay there until minting the whole collection. So be careful with drops and allowlist. I recommend adding only one allowlist without drops and waiting till all addresses are claimed or till the allowlist is disabled, or creating only one allowlist for the first drop. 
</div>

<div class="docs-info-box">
<strong>Important</strong> Also, please remember that each drop can have its limits per address, but a single address won't be able to mint more than the overall limit per token per the whole collection even if there is still room for that in current drop. Always be careful and plan it that way that everything sums up. You can change the global limit per address by: `elven-tools nft-minter set-new-tokens-limit-per-address`.
</div>

Let's go back to our custom scenario. So when you have the drop set to 300 tokens, we can set up the price. It will probably be something low as for the start and allowlist. You can do this by: `elven-tools nft-minter set-new-price`.

Then we can start the minting for only eligible addresses from the allowlist. All other attempts will fail. You can always check how many tokens are left by: `elven-tools nft-minter get-drop-tokens-left`. The Smart Contract will pause the minting process when all 300 tokens are minted.

When all tokens from the first drop are minted, I will prepare all the marketing for the next drop. I would probably not reveal the price yet. I would like to know what is happening with the first 333 tokens on the secondary market. What is the price, etc.? I would probably plan the next giveaway. Let's say I would give 100 tokens. Then I would prepare the next drop. Now I have 2900, so I would probably go with 2000 and 900 drop. You need to repeat the steps. Remember always to look out in which state the Smart Contract is. Remember about changing prices, and adequately stop and start minting.

<div class="docs-info-box">
Please keep in mind that this is a quick idea for example purposes. Do it as you think it will be best for your project. It is all quite elastic.
</div>

### Summary

Here are a couple of ideas on preparing the Smart Contract to sell the NFT collection on the Elrond blockchain.

Hopefully, it will be helpful, and the examples will help better understand the idea behind all the existing endpoints on the Smart Contract.

There will probably be more improvements. Please let me know if you will find a bug or have some ideas to improve the toolset. You can write to me directly: [Twitter](https://twitter.com/JulianCwirko) and [Telegram](https://t.me/JulianCwirko). Or you can report an issue on GitHub for the Smart Contract [here](https://github.com/juliancwirko/elven-nft-minter-sc/issues) and the CLI [here](https://github.com/juliancwirko/elven-tools-cli/issues).
