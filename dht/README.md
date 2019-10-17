# dht research
> [rust-p2p/s-kademlia](https://github.com/rust-p2p/s-kademlia)

The networking layer uses an implementation of [`s/kademlia`](https://www.researchgate.net/publication/4319659_SKademlia_A_practicable_approach_towards_secure_key-based_routing) to foster secure key-based routing. This variant of kademlia prevents sybil attacks on the address space by requiring a minimum work threshold for node generation (storage NodeId generation requires *trailing* bits of 0s `=>` slows down process of adding new nodes).

## why kademlia?

The symmetricity of the XOR metric ensures that disjoint converge to a single path. This provides more robust security against eclipse attacks by allowing for multiple lookups at once (to mitigate the probability that all lookups are intercepted by an attacker).

## building a dht framework

We are exploring how this work could be made into a framework for building DHTs. Some things we're considering:
* partition the network based on latency and use a random xor metric within that partition
* use chord to **embed latency** rather than relying on some distance-oblivious nodeId generation algorithm: *see [Towards a Framework for DHT Distributed Computing](https://scholarworks.gsu.edu/cgi/viewcontent.cgi?article=1108&context=cs_diss)*
* chord distance metric may be able use the rtt estimator required by delay-based congestion policies

### more reading

* [Broose: a Practical Distributed Hashtable based on the De-Bruijn Topology](http://www.cs.kent.edu/~javed/class-IAD06S/papers-2004/gai.pdf)
* [Introducing KFS: a local file store inspired by Kademlia](https://storj.io/blog/2016/09/introducing-kfs-a-local-file-store-inspired-by-kademlia/)
* [Redundancy on Swarm](https://swarm-guide.readthedocs.io/en/latest/architecture.html#redundancy)

