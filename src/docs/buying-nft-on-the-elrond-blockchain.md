---
layout: 'docs'
title: 'Buying NFT on the Elrond blockchain'
publicationDate: '2022-01-25'
tags:
  - articles
excerpt: "There is a couple of things that you should check when you are buying the NFTs on the Elrond blockchain. And a couple of differences in comparison with other chains."
ogTitle: "Buying NFT on the Elrond blockchain"
ogDescription: "There is a couple of things that you should check when you are buying the NFTs on the Elrond blockchain. And a couple of differences in comparison with other chains."
ogUrl: "https://www.elven.tools/docs/sc-introduction.html"
twitterTitle: "Buying NFT on the Elrond blockchain"
twitterDescription: "There is a couple of things that you should check when you are buying the NFTs on the Elrond blockchain. And a couple of differences in comparison with other chains."
twitterUrl: "https://www.elven.tools/docs/sc-introduction.html"
---

There is a couple of things that you should check when you are buying the NFTs on the Elrond blockchain. And a couple of differences in comparison to other chains. I don't want to focus on the supply and demand aspect because you should always do your own research before buying anything. I want to focus on the technological and communication-like elements here. 

### What we will tackle in the article:

1. Minting through the Smart Contract. How is it done?
2. The Smart Contracts on the Elrond blockchain are upgradeable by default.
3. Collection ticker and how to verify it.
4. Project website with the roadmap and people behind it.
5. Utility over 'art' unless not randomly generated.

Remember, these are just my opinions. You can always disagree, and I will like to see your point of view.

### Minting through the Smart Contract. How is it done?

Elrond blockchain treats the NFTs as native ESDT tokens with additional metadata, so it isn't required to have the Smart Contract to own them. And it isn't even needed to have a Smart Contract to mint them. 

Still, the minting process and distribution should be done using a Smart Contract because this is fair and trustworthy. The Smart Contract is a mediator between your EGLD and the NFT, which should be sent to you. Otherwise, some third-party wallet will be doing that, and in such a case, we need to trust the third party. So it is not a decentralized process.

The best would be to see the Smart Contract's code or at least be able to verify if the Smart Contract is the official one. Most projects will probably not show the Smart Contract's source code, and I understand it. But still, I think it would be possible to prepare the hash of a currently compiled Smart Contract's code and publish it in all communication channels. This way, the user will also know if the contract was upgraded or not. And if the team communicated it properly before taking action.

There are a couple of ways to prepare the minting and distribution process. All of them have pros and cons. 

**Let's take a look at two of them in the context of the Elrond blockchain:**

- 'Candy machine'
- 'Raffle'

The candy machine's method of minting works like a candy machine (surprise, surprise). The Smart Contract is usually preconfigured to manage the minting process. The buyer sends the amount of EGLD defined on the Smart Contract, and in exchange, they will get randomly minted NFT on their wallet. It is a relatively straightforward way of doing that, and it is ok. Its main pros are simplicity and transparent rules, so the buyers are not confused. They pay, and they see it on the wallet. It is also simpler to set up and maintain, and because of randomization in the minting process, even with automated scripts, it will be hard to snipe the best NFTs. In most cases, this is the way the projects mint.

The candy machine has its cons. The most important one is that when you want to mint in some batches spread in time, the first couple of NFTs will reveal the assets. At least in the Elrond ecosystem, it won't be possible to send the NFT and then change its assets URIs. The only option would be to upload the assets to the IPFS later, but this is a poor experience.

Is it a big problem? Some would say that even better because these NFTs can influence the price, and with the second batch of minting, the operator will know better what a new price should be for the next official drop. If the first 1000 NFTs are doing great on the secondary market and the price is high. Then the subsequent official minting can be better marketed, and the price can be managed better.

Other cons of the candy machine way of minting are that it is more prone to automated bots, and also, people from many different time zones will probably not have a chance to take part. 

There are a couple of solutions to these concerns. One would be not to send the tokens right away but to keep them and let the people claim them later after the whole collection is minted. Like with everything, this can be done with hybrid approaches, but most likely, it will be a Raffle minting process. Let's see how it could work on the Elrond blockchain and what the ideas are for it.

**The Raffle can work in two ways:**

- Locked EGLD as the ticket in a lottery
- SFT (Semi Fungible Token) as the ticket in a lottery

The simplest way would be to use EGLD and save all the addresses in the initial 'bidding/buying' phase. Such a phase can be spread in time. For example, it can be 48h long to allow all the people worldwide to participate. Then after some time, the operator can start the randomized claiming process, which will choose the winners. The winners will be able to claim the NFTs, and the losers will take back their EGLD.

The problem of revealing the assets will still be here unless the Smart Contract will keep the winning tickets till the end of the minting of the whole collection. This can be done so that winning addresses are moved to allowlist, and losing addresses can claim back their EGLD immediately after each batch of minting.

There is also a more entertaining way of doing that, incorporating the SFTs. Each SFT can look the same, for example, an egg for the dragons or a construction pack for robots, whatever you choose. Then each egg can be claimed after each batch of minting. So the winning addresses will also have something immediately, but not the real NFT yet. They can even sell these SFTs on the secondary market, similar to the candy machine incentive, but you don't operate on the real NFT.

Why sell the SFT on the secondary market? Because the owner will be able to swap it for the real NFT when the time is right. Remember that the operator should also correctly communicate it.

### The Smart Contracts on the Elrond blockchain are upgradeable by default.

It is worth mentioning that the Smart Contracts on the Elrond blockchain are by default upgradeable (and this is not only Elrond's specific case). What does it mean? It means that the operator can change the logic on the smart contract at every moment, even when the minting process is ongoing. In most cases, it is good because they will react quickly in case of bugs, and probably this is the way it will always work. But remember that it can also be used in a way that is not good for the participants. For example, some scam projects can release a proper Smart Contract, but then after the funds are on it, they can change its code and block all the funds. 

Ok, so what should you do with this kind of knowledge as a buyer? In most cases, projects won't show the Smart Contract's code anyway. So the best you can do is know about such possibilities and check how the project communicates them. Will they talk about changes or rather keep them in secret. It is why some kind of validation of the Smart Contracts is required, as I wrote before.

What can the project do to gain more trust? I will write more about the community's communication later, but how it is appropriately managed is through multisig. So there should be more than one person on the team to be able to upgrade the contract. There should be a requirement for multiple keys to authorize such a transaction. But let's be honest, the minting Smart Contracts and projects around them are usually relatively small, and probably no one will use that. Still, it is worth knowing about it, and it will be a perfect point in the marketing of a project.

How to check if a Smart Contract is upgradable or not? When you go to the Elrond Explorer and search for the project's Smart Contract, you will be able to see a badge. For example, let's take randomly one of the Smart Contracts on the mainnet: [explorer.elrond.com/accounts/erd1qqqqqqqqqqqqqpgqxwakt2g7u9atsnr03gqcgmhcv38pt7mkd94q6shuwt](https://explorer.elrond.com/accounts/erd1qqqqqqqqqqqqqpgqxwakt2g7u9atsnr03gqcgmhcv38pt7mkd94q6shuwt). There is a badge `UPGRADEABLE` under the properties section.

### Collection ticker and how to verify it.

On the Elrond blockchain, you would need to issue a collection token with a ticker in a short format, such as `ABCD-1a2e3`. It is an identifier for the NFT collection. For example, you can always check it in the Elrond Explorer, [explorer.elrond.com/collections/EGIRL-443b95](https://explorer.elrond.com/collections/EGIRL-443b95).

What is important here is that the project should always clearly communicate the official and only legit collection ticker. Because many scams will try to copy the collection, educating the buyers about that is always essential.

How will I check the collection ticker when I only have one NFT in my wallet? 
Each NFT will get a ticker that starts with the collection id first. So in the case of our example from above, the `EGIRL-443b95-0d8b` is a particular NFT ticker/id, so as you can see, the `EGIRL-443b95` prefix here is our collection id from the example. This way, you can always verify if this particular NFT comes from an actual collection and not a scammy one.

### Project website with the roadmap and people behind it.

Let's get into less technical and more communication-related topics. What is essential for me when I see the project is its website. It should be clean with good UI, and what is most important is that it should clearly describe the team and the vision. Most of the projects have only the Discord channel, but I don't find it professional. It is, of course, only my opinion and of course, having the Discord server isn't bad at all.

When I enter such a website, I would like to see the official collection ticker/id and the Smart Contract address. Of course, it isn't always possible because it depends on the process. Maybe there isn't a collection and Smart Contract yet, but I would like to get it when the process starts.

The team and roadmap are also critical. I saw that there are usually team members listed but nothing about them. They are just avatars with some nicknames. I think it is terrible, but of course, it is always good to be anonymous and earn some money ;) 

### Utility over 'art' unless not randomly generated.

I am not an artist, and I know nothing about art. But when we talk about randomly generated NFTs, it is for sure not about the art. I mean, maybe it is in some rare cases, but let's be honest, most of them are not even pretty ;)

It is not a problem at all because, in my opinion, it isn't their primary purpose. Knowing something more than the price is good if you want to get involved in a randomly generated avatar-like collection. There should be a utility to having such an NFT in your wallet. There are a couple of such use cases. Let's list a couple of them in general without specific examples and descriptions. You will find a lot about them on the Internet:

- NFT projects for the e-commerce industry.
- NFT projects for the gaming industry.
- NFT projects for the music industry.
- NFT projects for the medical industry.
- NFT projects for the real estate industry.
- NFT for academics and schools.
- NFT projects involved in charity.
- NFT projects for the VR/Metaverse.
- NFT as tickets.
- NFT in sports.
- NFT as the id and community platform access.

The list can probably go a lot further. There are many use cases, but we are all early, and it has to settle down a little bit. I intend to indicate that you should always look deeper and buy some good projects. Unless you are an NFT flipper, then buy everything as fast as you can ;) But I am not interested in such an activity.

### Summary

Hopefully, I explained a couple of the most important things when someone is interested in some NFT project on the Elrond Blockchain, but not only on the Elrond. Some of the guides are pretty universal.

Be aware that these are only my opinions. I am primarily a developer, so I'm not an expert in marketing, selling, and promoting stuff. I wrote from a developer's perspective and a person who would like to buy some NFTs at some moment in time.

[Contact me!](/about.html) 
Follow me on [GitHub](https://github.com/juliancwirko) and [Twitter](https://twitter.com/JulianCwirko).
