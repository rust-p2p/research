An asynchronous, replicated database with nuanced consistency guarantees based on underlying data properties. The distributed storage layer will be incentivized by robust, yet intentionally simple network economics. Read how [below](#intro).

## why not ipfs?

[ipfs](https://ipfs.io/docs/) introduced some good theoretical ideas (like object immutability), but made many implementation mistakes. In practice, many features still suck; for example, it is slow and buggy for something as simple as fetching files.

There are many basic bugs that haven't been fixed because of an obsession with modularity and abstraction at the networking layer ([libp2p](https://github.com/ipfs/go-ipfs)). 

Currently, it connects to bootstrap nodes and tries to discover peers asynchronously. The handshake with bootstrap nodes fails before it discovers peers`=>` it waits another 1-5 minutes depending on the setting to (re-)attempt discovery after the handshake fails. This causes startup to take a few minutes (and [this issue](https://github.com/ipfs/go-ipfs/issues/5953) has been open since May)...

## bddb <a name = "intro"></a>

**bddb doesn't rely on libp2p**. This design choice alone contributes to increased simplicity `=>` maintainability, testability, optimization in context, and much more ;)

### networking

The networking layer consists of three main parts:

1. An implementation of [`s/kademlia`](https://www.researchgate.net/publication/4319659_SKademlia_A_practicable_approach_towards_secure_key-based_routing) fosters secure key-based routing. This variant of kademlia prevents sybil attacks on the address space by requiring a minimum work threshold for node generation (storage NodeId generation requires *trailing* bits of 0s `=>` slows down process of adding new nodes). This implementation is in-progress at [rust-p2p/s-kademlia](https://github.com/rust-p2p/s-kademlia). *See ongoing, related research in [dht](./dht)*

2. NAT traversal

3. Transport layer uses [disco](https://github.com/rozbb/disco-rs), which consists of `strobe + noise` over tcp

*[Fed Up Getting Shattered and Log Jammed? A New Generation of Crypto is Coming](https://www.youtube.com/watch?v=bTGLO4obxco)*

### persistent database

**[sled](https://github.com/spacejam/sled/)**, thanks `spacejam` :)

### consistency

* [hashgraph](https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf)
* [red-blue](https://www.usenix.org/system/files/conference/osdi12/osdi12-final-162.pdf)

### incentives

* [Robust incentive techniques for peer-to-peer networks](https://zoo.cs.yale.edu/classes/cs426/2012/bib/feldman04robust.pdf)
* [An incentive mechanism for p2p networks](http://dna-pubs.cs.columbia.edu/citation/paperfile/18/ICDCS04.pdf)
* [`troublescooter/incentives`](https://github.com/troublescooter/incentives)