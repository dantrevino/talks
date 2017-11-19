<section data-background="white">
![BlockStack](https://media.githubusercontent.com/media/blockstack/designs/master/logo/external/RGB/logo/blockstack-logo-vertical-bug%402x.png)


#### cop-blockchain

Note:

</section>

---

<section data-background="#270f34">

## What Is Blockstack? ##

<img src="pillars.png"/>

Note:
1) Blockstack is a new decentralized Internet where users own their data and apps run locally.

2) Blockstack is an open source development layer for the bitcoin blockchain that enables identity, storage, and discovery.

3) Built to be blockchain agnostic

</section>

---

<section data-background="#270f34">
## Identity ##

[Blockstack id](https://blockstack.org/posts/blockchain-identity)

[Onename](https://onename.com)

Note:
1) Register id via the blockstack browser or CLI.

2) .id namespace on bitcoin blockchain

</section>

---

<section data-background="#270f34">
## Storage ##

[Gaia](https://github.com/blockstack/blockstack-core/blob/rc-0.14.2/docs/gaia.md)

Note:
1) Turns existing storage providers into dumb datastores (privacy, encryption)

2) Uses familiar filesystem concepts such as inodes, getFile, putFile

</section>

---

<section data-background="#270f34">
## Discovery ##

[Atlas](https://blockstack.org/whitepaper.pdf)

Note:
1) DHT-like. Works like DHT, but is definitely not a DHT.  The Atlas peer network is _unstructured_, unlike DHTs, which makes it more resilient to individual edges in the peer graph failing.

2) Each peer has a 100% replica of all the system's zone files, so all your routing lookups are locally-handled (no Dyn DNS-like DDoS attacks are possible)

3) As long as the peer network graph is connected (doesn't matter how), every peer will eventually get 100% of the zone files.  

4) Just works!

</section>

---

<section data-background="#270f34">
## Demo ##

```bash
npm install -g yo generator-blockstack
mkdir hello-blockstack && cd $_
yo blockstack
npm start
```

Note:

1) Install Yeoman and the blockstack app generator using npm.

2) Create a new directory and `cd` into it.

3) Generate your Blockstack app.

4) Start the development server.

</section>

---

<section data-background="#270f34">
## Blockstack Your Own App in 5 Minutes ##

Terminal Here -->

Note:

1) Install Hello-Blockstack

2) Overwrite index.html

3) Add app.js and bundle.js

4) Identify elements for:
  * signin-button
  * signout-button
  * avatar-image
  * heading-name

5) show require.js

</section>

---

<section data-background="#270f34">

## Find Us ##

* Slack - chat.blockstack.org
* Twitter - <i class="fa fa-twitter" aria-hidden="true"></i>@Blockstack
* GitHub - github.com/blockstack/
* Meetup - meetup.com/Blockstack-Portland

Note:

</section>
