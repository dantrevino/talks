---
title: BlockStack - Nike Blockchain COP
theme: theme/blockstack.css
---

![BlockStack](blockstack-logo-vertical-bug%402x.png)


<img src="blockstack-0308.svg" height="36px" width="36px" style="border:none;vertical-align:middle;"> dantrevino.id

<i class="mdi mdi-twitter"></i>@dantrevino

---

## What Is Blockstack? ##


Note:
1) Blockstack is a new decentralized Internet where users own their data and apps run locally.

2) Blockstack is an open source development layer for the bitcoin blockchain that enables identity, storage, and discovery.

3) Built to be blockchain agnostic

---

## Identity ##

[Blockstack id](https://blockstack.org/posts/blockchain-identity)

[Onename](https://onename.com)

Note:
1) Register id via the blockstack browser or CLI.

2) .id namespace on bitcoin blockchain

---

## Storage ##

[Gaia](https://github.com/blockstack/blockstack-core/blob/rc-0.14.2/docs/gaia.md)

Note:
1) Turns existing storage providers into dumb datastores (privacy, encryption)

2) Uses familiar filesystem concepts such as inodes, getFile, putFile

---

## Discovery ##

[Atlas](https://blockstack.org/whitepaper.pdf)

Note:
1) Works like DHT, but definitely not a DHT.  The Atlas peer network is _unstructured_, unlike DHTs, which makes it more resilient to individual edges in the peer graph failing.

2) Each peer has a 100% replica of all the system's zone files, so all your routing lookups are locally-handled (no DynDNS-like DDoS attacks are possible)

3) As long as the peer network graph is connected (doesn't matter how), every peer will eventually get 100% of the zone files.  

4) Just works!

---

## Demo ##

Note:
1) ToDo Demo - identity & storage

2) Identity

  a. Landing.vue

    i. blockstack.redirectToSignIn()

  b. App.vue

    i. blockstack.isUserSignedIn()

3) storage

  a. Dashboard.vue

    i. blockstack.putFile()

    ii. blockstack.getFile()

---

## Build ##

```bash
npm install -g yo generator-blockstack
mkdir hello-blockstack && cd $_
yo blockstack
npm run start
```

Note:

1) Install Yeoman and the blockstack app generator using npm.

2) Create a new directory and `cd` into it.

3) Generate your Blockstack app.

4) Start the development server.

---

## Find Us ##

<i class="mdi mdi-chat"></i> forum.blockstack.org

<i class="mdi mdi-twitter"></i> @Blockstack

<i class="mdi mdi-github"></i> github.com/blockstack/

<i class="mdi mdi-chat"></i> Blockstack-Portland

Note:
