# libp2p

## provider abstraction

*bitswap*

## reputation overlay
* [PR #1178: Fixes #1335](https://github.com/libp2p/rust-libp2p/pull/1178)

* Each node holds a topology, containing the nodes that are known to be part of the network. The topology is cached on the disk, and is loaded on startup if it exists. Each node in the topology has a reputation ranging from 0 to 100. Keep in mind that a node’s reputation value is local, as each node posesses its own local topology. On startup, bootstrap nodes are added to the topology with a score of 100. * Each node tries to maintain 25 outgoing connections by picking the nodes with the highest score. If multiple nodes have the same score, which one is picked is random.
* Each node also accepts up to 25 ingoing connections, after which new connection attempts are denied.
* Each node we are connected to gains 1 reputation for every 10 seconds we have been connected to it.
* After 5 seconds, and then every 45 seconds, a node performs a Kademlia iterative query on a random node ID with the purpose of filling the topology with new nodes. The responses to this iterative query are added to the topology with either 15 reputation or 10 reputation, depending on whether or not one of the Kademlia-answering nodes is connected to the reported node.
* If a node misbehaves on the chain-specific protocol layer, it loses 10 reputation and its public key is disabled for 5 minutes. If a node cannot be reached, it loses 1 reputation. If a node reaches a reputation of 0, it gets disabled for 5 minutes after which it is removed from the topology and will be added back if it gets discovered again. An exponential time-off system exists in order to avoid hammering nodes with connection requests and making them quickly drop to 0.
