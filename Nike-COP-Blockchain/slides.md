# Intro

* Blockstack

---

## Background

> What is blockstack?

Note:
1) Blockstack is a new decentralized Internet where users own their data and apps run locally.
2) Blockstack is an open source layer to the bitcoin blockchain that enables identity, storage, and discovery.
3) Built to be blockchain agnostic

---

> Identity

[Blockstack id](https://blockstack.org/posts/blockchain-identity)

[Onename](https://onename.com)

Note:
1) Register id via the blockstack browser or CLI.
2) .id namespace on bitcoin blockchain
3)

---

> Storage
[Gaia] (https://github.com/blockstack/blockstack-core/blob/rc-0.14.2/docs/gaia.md)

Note:
1) Turns existing storage providers into dumb datastores (privacy, encryption)
2) Uses familiar filesystem concepts such as inodes, getFile, putFile
3)

---

> Discovery
[Atlas] (?? whitepaper maybe ??)
Note:
1) DHT
2) Each node maintains a full copy of zone hashes
3)

---

> Demo

Note: ToDo Demo

---

> Build

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
