---
layout: "docs"
title: "Jump start"
publicationDate: "2022-01-25"
tags:
  - intro
excerpt: "The Elven Tools includes smart contracts, CLI tool, and Minter Dapp for NFT/SFT launches. Every part of it can be used as a separate tool."
ogTitle: "Elven Tools CLI tool - jump start!"
ogDescription: "The Elven Tools includes smart contracts, CLI tool, and Minter Dapp for NFT/SFT launches. Every part of it can be used as a separate tool."
ogUrl: "https://www.elven.tools/docs/jump-start.html"
twitterTitle: "Elven Tools CLI tool - jump start!"
twitterDescription: "The Elven Tools includes smart contracts, CLI tool, and Minter Dapp for NFT/SFT launches. Every part of it can be used as a separate tool."
twitterUrl: "https://www.elven.tools/docs/jump-start.html"
githubUrl: "https://github.com/ElvenTools/elven-tools-website/edit/main/src/docs/jump-start.md"
---

<div class="docs-info-box">Remember that the CLI uses public API endpoints by default. You can switch to the custom ones. Read more how to do this <a href="/docs/recipes.html#custom-api-endpoints">here</a>.</div>

### NFT Minter TL;DR

1. `npm install -g elven-tools` -> install the npm library (you would need to have Node configured on the system)
2. `elven-tools derive-pem` -> provide the seed phrase, the walletKey.pem file will be generated
3. `elven-tools deploy nft-minter` -> provide all the data. There will be a couple of prompts
4. `elven-tools nft-minter issue-collection-token` -> provide the name and ticker. You can also provide a separate name for NFTs. You can also opt-out of adding the edition number to the name.
5. `elven-tools nft-minter set-roles` -> roles for the issued token
6. `elven-tools nft-minter start-minting` -> starts the minting. By default, it is paused at start
7. `elven-tools nft-minter mint` -> mint tokens, provide the amount, be careful. There will be custom limits per address

There is also a video which shows it. So I recommend you to check it out:

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/Jou5jn8PFz8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

Then you can also initialize the Minter Dapp template by using `elven-tools init-dapp`.
Check how to start with it here: [How to start with the Dapp](/docs/how-to-start-with-the-dapp.html).

- Check longer explanation here: **[CLI NFT Workflow](/docs/cli-nft-workflow.html)**

### SFT Minter TL;DR

1. `npm install -g elven-tools` -> install the npm library (you would need to have Node configured on the system)
2. `elven-tools derive-pem` -> provide the seed phrase, the walletKey.pem file will be generated
3. `elven-tools deploy sft-minter` -> deploy the SFT minter smart contract from GitHub directly or from local file system
4. `elven-tools sft-minter issue-collection-token` -> provide collection token name and ticker
5. `elven-tools sft-minter set-roles` -> required roles for the issued token
6. `elven-tools sft-minter create` -> create SFT token and provide all required data using prompts
7. `elven-tools sft-minter start-selling` -> start the selling process, you can also pause it with `pause-selling`
7. `elven-tools sft-minter buy` -> buy an amount of SFT tokens, it will respect max tokens per address limit

There is also a video which shows it. So I recommend you to check it out:

<div class="embeded-media-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/rMF3ItijHUA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
<div>

- Check longer explanation here: **[CLI SFT Workflow](/docs/cli-sft-workflow.html)**
