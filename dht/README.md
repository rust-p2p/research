# dht research
> [rust-p2p/s-kademlia](https://github.com/rust-p2p/s-kademlia)

The networking layer uses an implementation of [`s/kademlia`](https://www.researchgate.net/publication/4319659_SKademlia_A_practicable_approach_towards_secure_key-based_routing) to foster secure key-based routing.

## why kademlia?

The symmetricity of the XOR metric ensures that disjoint lookups converge to a single path. This makes it harder to successfully execute eclipse attacks by, in general, encouraging nodes to ask more peers.

## building a dht framework

We are exploring how this work could be made into a framework for building DHTs. Some things we're considering:
* partition the network based on latency and use a random xor metric within that partition
* use chord to **embed latency** rather than relying on some distance-oblivious nodeId generation algorithm: *see [Towards a Framework for DHT Distributed Computing](https://scholarworks.gsu.edu/cgi/viewcontent.cgi?article=1108&context=cs_diss)*
* chord distance metric may be able use the rtt estimator required by delay-based congestion policies

### bitswap

talks
* [jeromy coffee talks - bitswap](https://www.youtube.com/watch?v=9UjqJTCg_h4)
* [london hack week - grapnsync improvements and modular architecture](https://www.youtube.com/watch?v=6GKKwcG630M)

code/specs
* [js-ipfs](https://ipfs.github.io/js-ipfs-bitswap/#intro)
* [golang-ipfs](https://github.com/ipfs/go-bitswap#implementation)

### more reading

* [s-kademlia ppt](https://pdfs.semanticscholar.org/3165/2823ca71520038773346b6e5bbfadc5c8419.pdf)
* [Broose: a Practical Distributed Hashtable based on the De-Bruijn Topology](http://www.cs.kent.edu/~javed/class-IAD06S/papers-2004/gai.pdf)
* [Introducing KFS: a local file store inspired by Kademlia](https://storj.io/blog/2016/09/introducing-kfs-a-local-file-store-inspired-by-kademlia/)
* [Redundancy on Swarm](https://swarm-guide.readthedocs.io/en/latest/architecture.html#redundancy)

#### videos (basics)

* [XOR Distance and Basic Routing](https://www.youtube.com/watch?v=w9UObz8o8lY)
* [How are Routing Tables built?](https://www.youtube.com/watch?v=mJgN3PzepqI)
* [Building Decentralized Systems using DHTs](https://www.youtube.com/watch?v=BCksQYqU5ok)
