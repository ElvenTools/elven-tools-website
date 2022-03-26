---
layout: 'docs'
title: 'Use of IPFS in the Elrond NFT ecosystem'
publicationDate: '2022-03-26'
tags:
  - articles
excerpt: "IPFS storage is a crucial part of every NFT ecosystem, not only the Elrond. It allows storing and accessing data in a decentralized and trustless way."
ogTitle: "Use of IPFS in the Elrond NFT ecosystem"
ogDescription: "IPFS storage is a crucial part of every NFT ecosystem, not only the Elrond. It allows storing and accessing data in a decentralized and trustless way."
ogUrl: "https://www.elven.tools/docs/use-of-ipfs-in-the-elrond-nft-ecosystem.html"
twitterTitle: "Use of IPFS in the Elrond NFT ecosystem"
twitterDescription: "IPFS storage is a crucial part of every NFT ecosystem, not only the Elrond. It allows storing and accessing data in a decentralized and trustless way."
twitterUrl: "https://www.elven.tools/docs/use-of-ipfs-in-the-elrond-nft-ecosystem.html"
---

IPFS storage is a crucial part of every NFT ecosystem, not only the Elrond. I found that there is a lot of misunderstanding about why it is required and how it works. I won't describe the IPFS in detail, and it doesn't make sense because there are many excellent articles about it on the Internet that I am about to link. What I would like to do is to explain the basics in the context of Elrond NFTs.

### What we will tackle here:

- IPFS basic intro.
  - Why is IPFS required?
  - How are the files handled?
  - What is a CID?
  - Pinning, why it is essential?
  - What is an IPFS gateway?
  - Where can I learn more about IPFS?
- How is it used in the Elrond ecosystem?
- Helpful IPFS services and tools.

### IPFS basic intro.

The InterPlanetary File System is a peer-to-peer hypermedia protocol. It allows storing and accessing data in a decentralized and trustless way. You are the owner of your data stored on many different nodes located in various places in the world. It can be an image, website, or any other data.

**Why is IPFS required?**

It is essential to have decentralized storage for the assets of your NFT token. The assets can't be stored on-chain for the main reason: the size and cost of keeping it on-chain. When using IPFS, you are not dependent on centralized corporations like Amazon, Microsoft, or Google to store your assets (images, movies, music). You don't want your NFT token to depend on a third-party company, even if it is only assets hosting. On-chain metadata, plus assets hosted in a decentralized way, seems like an obvious way of doing that.

**How are the files handled?**

One of the main concepts of the IPFS is content addressing. In the IPFS network, the identifier of the content is built based on the content, not the location. You can't change the address of the same content. It is possible, for example, using AWS, where you can change addresses to the same content by changing the domain name, etc. We don't want that for our NFTs because someone could move the assets somewhere else and change the address to them. Then the metadata information on-chain would be wrong, and the saved URL would not show the asset. 

When someone changes the content on the IPFS, it will get a different identifier and, in fact, always a different address. The old content can't be changed, deleted, or moved. So this is ideal. Our saved URL on-chain will always point to the same asset on the IPFS.

You can learn a lot more about the topic here: 
- [proto.school/content-addressing](https://proto.school/content-addressing).
- [docs.ipfs.io/concepts/how-ipfs-works/#content-addressing](https://docs.ipfs.io/concepts/how-ipfs-works/#content-addressing)

Ok, so how the address/url to such content looks. Let's jump to the next topic from the list.

**What is a CID?**

The CID (Content Identifier) is a foundation of the content address on the IPFS. It doesn't tell where the content is located, but it defines the content. For example, it could be built based on one image or the directory of images. The main concept is that the CID will be different when anything is changed.

The final CID form depends on the content and not on its size. It is a cryptographic hash of the content. The CID helps to find the nearest source of our content. This way, we will be able to get it from one of many nodes/peers in the network which could store it.

Ok, let's not dig deeper because these topics are complex. I will leave links where you will find more information.

To sum up. It is worth remembering that it is the main and the only identifier we need to locate our content. 

Read more about the CIDs here:
- [proto.school/anatomy-of-a-cid](https://proto.school/anatomy-of-a-cid)
- [docs.ipfs.io/concepts/content-addressing/#identifier-formats](https://docs.ipfs.io/concepts/content-addressing/#identifier-formats)

Let's jump to the next crucial topic. 

**Pinning, why it is essential?**

Pinning in the IPFS world is comparable to pinging some service to keep it 'alive'. It is very similar. The content on the IPFS network isn't stored forever if it isn't needed anymore. There are special 'garbage collector' services that will remove the contents which are not needed anymore. And what does it mean? It means that there have been no requests for such content since the last request, so that nodes won't store it anymore.

An IPFS node can protect data from garbage collection using a so-called pinning service. Of course, you could run your node locally and pin the data, but usually, it is done by using a third-party service that runs many nodes and can provide pinning for you. I will focus on two of such services at the end of the article, so keep reading.

When it comes to the NFTs, even when the collection author provided pinning for all assets by default (and they should), you can also pin the assets as a buyer by providing the CID. I will describe how to do this later in the article.

You can read more about pinning and persistence here: [docs.ipfs.io/concepts/persistence/#persistence-versus-permanence](https://docs.ipfs.io/concepts/persistence/#persistence-versus-permanence)
Let's see how to get our assets using the CID.

**What is an IPFS gateway?**

When you know the CID of your content on the IPFS, you can get it in many different ways. You can use the CLI tools, the desktop apps, or the most straightforward way - special web services called IPFS gateways.

IPFS gateway is a standard web service that will locate your content and serve it in the browser. It doesn't matter which gateway you will use. For the same CID, all of them should return the same content. Let's take, for example, two of them as an example: 

- [https://ipfs.io/ipfs/bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png](https://ipfs.io/ipfs/bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png)
- [https://bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea.ipfs.dweb.link/7894.png](https://bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea.ipfs.dweb.link/7894.png)

As you can see, these are different web services, but when we use the same CID of the directory and the same file name, we will still get the same image.

What is also worth mentioning is that you can use the IPFS URI schema in a Brave browser to get the same image. It is supported only in the Brave browser for now. It will look like this:

- [ipfs://bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png](ipfs://bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png)

You will find a list of gateways [here](https://ipfs.github.io/public-gateway-checker/). Remember that also Elrond provides a custom IPFS gateway. See the same example below: 

- [https://media.elrond.com/nfts/asset/bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png](https://media.elrond.com/nfts/asset/bafybeigdsbu4tkfzn23ufjugvzo4ht7myazyxl6gtecywtj4vlyvekqxea/7894.png)

The IPFS gateways are probably the simplest way to access, download or preview your content. Read more about the topic here: [docs.ipfs.io/concepts/ipfs-gateway/#overview](https://docs.ipfs.io/concepts/ipfs-gateway/#overview).

**Where can I learn more about IPFS?**

Besides all links from previous chapters, I will leave a couple of links below. The IPFS is a broad and complex topic, but it is worth reading about it and learning more. Let's see where you will find more information:

- Official docs: [https://docs.ipfs.io/](https://docs.ipfs.io/)
- Tutorials: [https://proto.school/](https://proto.school/)
- Youtube channel: [https://www.youtube.com/c/IPFSbot](https://www.youtube.com/c/IPFSbot)
- Awesome IPFS GitHub repo: [https://github.com/ipfs/awesome-ipfs](https://github.com/ipfs/awesome-ipfs)

### How is it used in the Elrond ecosystem?

Finally, let's jump into the Elrond ecosystem and see how we can use the IPFS when creating the NFTs on the Elrond chain.

The main concept of the NFT token on the Elrond blockchain is that it is the ESDT token, so the standard Elrond token, but with additional metadata. 

There are no strict rules on what your NFT token should look like. I mean, what structure its attributes should have. The main field for keeping the data on-chain is the 'attributes' field. I won't focus much on how NFTs work on the Elrond blockchain because it is a topic for many different articles, and it was already covered partially. Also, see the [official docs on it](https://docs.elrond.com/developers/nft-tokens/).

When preparing the NFT, we need to split the data of our NFT token into the small batch, which will be kept on-chain, and all other stuff that will be kept off-chain using IPFS decentralized storage. 

On Elrond, for on-chain, we will keep only the information about the CIDs for the metadata JSON file with all additional data like traits, description, etc., and the actual asset CID and probably file names. Let's take a closer look and take the example from Elven Tools.

Here is the example of the NFT minted using the Elven Tools: [https://devnet-explorer.elrond.com/nfts/FTDD-743ba3-06](https://devnet-explorer.elrond.com/nfts/FTDD-743ba3-06]).

You will see that we have two assets linked using the IPFS gateway. The most popular gateway. The JSON file is the metadata for our token. You can preview its content, but this isn't important for now. The metadata file is added there, but this isn't a standard. The Elven Tools allows choosing if you want it there or not. It isn't required because the information about the metadata CID is located in the attributes. They are not displayed in the explorer directly. But when you preview the API response for this token, you will find that attributes are a base64 encoded string that after decoding will give you something like that: `'metadata:bafybeifjntwejc7k7dedfaavravhnosc7xe4ceu5zmobjhhbob32uyu57m/25.json'`. So the same CID and file name as in the assets in the explorer.

Based on that, the Elrond API services will prepare additional data for your token. Like media and metadata objects. So it is essential to have such entry in your attributes field.

For now, the only supported decentralized storage seems to be IPFS, but I think this is ok. IPFS is the most popular way of storing content in a decentralized manner. But Elrond's services for that will probably be extended in the future. For example, with the Arweave support.

To sum up. Metadata, images, and all other assets should be kept off-chain using IPFS because it is much cheaper. The CID for the metadata and assets is critical in how Elrond API services work. The CID and file name for the metadata file should be provided in the 'attributes' field with the defined format and encoded with base64. This will open the door to proper operations on the NFT data and prepare appropriate API responses. It is also used for thumbnails generation and optimizations for assets serving. The metadata JSON file CID in the assets section is optional. Some of the marketplaces require that.

### Helpful IPFS services and tools.

Last is the section about essential services commonly used for uploading and managing the assets on IPFS. There are a couple of them, but I want to focus on two here. These are:

- [https://www.pinata.cloud/](https://www.pinata.cloud/)
- [https://nft.storage/](https://nft.storage/)

The Pinata is a top-rated service where you can upload a whole directory, and it will be pinned automatically for you. You will get your CID which you can use for your NFTs.

The Pinata has free and paid plans. You can choose whatever suits your needs.

I don't use Pinata much, but I like their pinning service for CIDs, which are not generated by their service. You could secure your assets even if you didn't upload them using Pinata. It is something that should always be done when you buy NFTs. Just in case.

The nft.storage service is my preferred one. The main reason is that it is free, and they also use Filecoin to secure the contents. You can read more about it on their website. And still, all is free.

Nft.storage allows uploading single files or CAR files, similar to standard TAR files. The functionality is identical to the Pinata. You will get your CID file, whether it will be a single file or directory/CAR. 

Both services allow uploading using their web interface or many different tools. The web interface won't be enough when you want to upload a massive set of data because of the browser's limitations. In such a case, you would need to use the CLI tool or any other provided. For example, nft.storage has an excellent [JavaScript client SDK for their API](https://nft.storage/docs/client/js/).

Another important thing is to keep in mind that even if you, as the collection creator, have uploaded the files and there is an option to remove them, this doesn't mean that when you remove the files, they will disappear from IPFS. As I mentioned, you can't remove or modify already uploaded content. It can only disappear when it is garbage-collected, which in the case of nft.storage will be hard because the content will also land on the Filecoin. But of course, as the creator, you should keep the files pinned there. Also, every buyer can pin their assets using, for example, Pinata and CIDs.

### Summary

Hopefully, I was able to explain some basics and show you the path where you could start learning about decentralized storage and IPFS. The Elven Tools is prepared to consume the IPFS and keep the Elrond best practices so feel free to play around and test things.

If you want to contact me, you will find all communication channels here: [www.elven.tools/about.html](www.elven.tools/about.html).
