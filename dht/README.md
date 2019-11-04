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
* [bitswap](./bitswap.md)

### more reading

* [s-kademlia ppt](https://pdfs.semanticscholar.org/3165/2823ca71520038773346b6e5bbfadc5c8419.pdf)
* [Broose: a Practical Distributed Hashtable based on the De-Bruijn Topology](http://www.cs.kent.edu/~javed/class-IAD06S/papers-2004/gai.pdf)
* [IPFS issue: DHT 2.0](https://github.com/ipfs/notes/issues/291)
* [Thoughts on the next level of content routing for IPFS](https://github.com/ipfs/notes/issues/162)
