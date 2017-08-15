<section data-background="white">
![BlockStack](https://media.githubusercontent.com/media/blockstack/designs/master/logo/external/RGB/logo/blockstack-logo-vertical-bug%402x.png)


###### @dantrevino

---

<section data-background="#270f34">

## What Is Blockstack? ##


Note:
1) Blockstack is a new decentralized Internet where users own their data and apps run locally.

2) Blockstack is an open source development API for the bitcoin blockchain that enables identity, storage, and discovery.

---

<section data-background="#270f34">
## BlockStack API ##

[Storage](https://github.com/blockstack/blockstack-core/blob/rc-0.14.2/docs/gaia.md)

[Discovery](https://blockstack.org/whitepaper.pdf)

[Identity](https://blockstack.org/posts/blockchain-identity)

Note:

1) Storage (Gaia)

a) Turns existing storage providers into dumb datastores (privacy, encryption)

b) Uses familiar filesystem concepts such as inodes, getFile, putFile

2) Discovery

a) Works like DHT, but defintely not a DHT.  The Atlas peer network is _unstructured_, unlike DHTs, which makes it more resilient to individual edges in the peer graph failing.

b) Each peer has a 100% replica of all the system's zone files, so all your routing lookups are locally-handled (no Dyn DNS-like DDoS attacks are possible)

c) As long as the peer network graph is connected (doesn't matter how), every peer will eventually get 100% of the zone files.  

---

<section data-background="#270f34">
## Identity ##

[Blockstack id](https://blockstack.org/posts/blockchain-identity)

[Onename](https://onename.com)

Note:
1) Register id via the blockstack browser or CLI.

2) .id namespace on bitcoin blockchain

3) Built to be blockchain agnostic

---

<section data-background="#270f34">
## Virtual Chain ##

[https://blockstack.org/virtualchain_dccl16.pdf](https://blockstack.org/virtualchain_dccl16.pdf)

Note:

1) Virtualchain is a logical layer for multiplexing multiple fork-consistent state transition journals on a blockchain.

a) a blockchain can fail

b) Application's journal can be forked and corrupted by the underlying blockchain

2) Used during namecoin to bitcoin chain migration

---

<section data-background="#270f34">
## Join Us! ##

* Slack - chat.blockstack.org
* Twitter - @BlockstackOrg
* GitHub - github.com/blockstack/
* Meetup - meetup.com/Blockstack-Portland
