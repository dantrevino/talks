---

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

[Discovery](https://blockstack.org/whitepaper.pdf)

[Storage](https://github.com/blockstack/blockstack-core/blob/rc-0.14.2/docs/gaia.md)

[Identity](https://blockstack.org/posts/blockchain-identity)


Note:  There are 3 main components to the BlockStack API:

1) Discovery encompasses Atlas and BNS (Blockstack Naming System).  Atlas is a peer network that enables discovery for the BlockStack Naming System.  

2) Storage (Gaia) - Gaia is a framework for managing user and application data tied to app/system keys and users.

3) Identity (Blockchain ID) is based on the Blockstack Naming System.  Users peg their identities to domains e.g. `jackzampolin.id`.

---

<section data-background="#270f34">
## Discovery - Blockstack Naming System ##

<img src="https://blockstack.org/images/visuals/blockstack-tx-diagram.png" width="500">

Note:

1) BNS provides total ordering of name operations on the blockchain.

2) Name information is maintained and distributed on the Atlas network.  This is the first implementation of a decentralized DNS system on top of the Bitcoin blockchain. It combines DNS functionality with public key infrastructure.

3) Atlas works like DHT, but defintely not a DHT.  The Atlas peer network is _unstructured_, unlike DHTs, which makes it more resilient to individual edges in the peer graph failing.

4) BNS will always be eventually consistent, because each peer has a 100% replica of all the system's zone files.  This has the advantage that all your routing lookups are locally-handled (no Dyn DNS-like DDoS attacks are possible, no central authority authorizing domains)

---

<section data-background="#270f34">
## Storage - Gaia ##

<img src="https://raw.githubusercontent.com/blockstack/gaia/master/figures/gaia-getfile.png" width="500">

Note:

1) Using BNS users point their domain name to a storage backend.

2) Access is granted to applications through the identity system.

3) Storage backend currently Dropbox. Adding support for S3 compatible backends (AWS, Google, Azure, Minio), as well as distributed systems like IPFS.

---

<section data-background="#270f34">
## Identity - Blockchain ID ##

[Blockstack id](https://blockstack.org/posts/blockchain-identity)

[Onename](https://onename.com)

Note:
1) IDs are 100% user owned, and can be registered via the Blockstack browser or CLI.

2) .id namespace currently on bitcoin blockchain and is currently the largest application usage of that network.

3) Virtualchain makes this identity blockchain agnostic

---

<section data-background="#270f34">
## Architecture ##

<img src="https://blockstack.org/images/visuals/blockstack-architecture-diagram.svg" width="500">

Note:
1) Lowest layer is the blockchain where which Blockstack uses to bootstrap trust in the network. Currently we run on BTC, but because of the implementation Blockstack can easily move to other blockchains. This is our Virtualchain technology.

2) With the Virtualchain we have built the Blockstack Naming system which is functionally similar to DNS

3) Using these names as a basis we built out the Storage, Discovery, and Identity applications on top.  

---

<section data-background="#270f34">
## Virtual Chain ##

[Whitepaper](https://blockstack.org/virtualchain_dccl16.pdf)

[Python Implementation](https://github.com/blockstack/virtualchain)

Note:

1) Virtualchain addresses scalability and latency concerns when using blockchain for applications as well as dependency on any single blockchain.

2) It is a logical layer for multiplexing multiple fork-consistent state transition journals on a blockchain.  Which is a fancy way of saying it allows multiple applications to maintain total ordering of operations.

3) Some implications:

  a) The BlockStack system is not dependant on any specific blockchain.  Drivers can be written to enable this development stack on any blockchain.  This is also smart because betting on any one blockchain this early in the evolution of the space is a losing bet. For example, this functionality was used during namecoin -> bitcoin chain migration of BNS.

  b) Applications can be updated, migrated, changed without dependency on blockchain

  c) Application transactions can occur outside of the blockchain, lessening impact on the blockchain network and improving overall performance.

---

<section data-background="#270f34">

## Find Us ##

* <i class="fab fa-slack"></i> chat.blockstack.org

* <i class="fab fa-twitter"></i> @Blockstack

* <i class="fab fa-github"></i> github.com/blockstack/

* <i class="fab fa-meetup"></i> Blockstack-Portland

Note:

1) Be sure to download and try the Blockstack Browser at blockstack.org/install

2) Whitepapers and more detailed technical information can be found at blockstack.org/papers

3) Join us at Blockstack-Portland

</section>
