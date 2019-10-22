# Perlin Network Implementation Notes

notes on the Perlin network structure to build a Rust version of skademlia...

## why?

For the Rust implementaton:

At this point, I'm most interested in the `node_id` generation code and how that is conflated with the key type definitions. This influences the topology of the network as well as the friction associated with joining the network (exacerbated by additional requirements to mitigate DoS-esque sybil attacks on the network). 

The spec says that the best approach is `H (public_key)`. Useful for authentication, key exchange, and signing messages...

Instead of relying on a centralized certificate authority, I want to go the alternative route...

### signature

* `weak (timestramp, ip, port)` `=>`used for `PING` and `FIND_NODE` messages
* `strong (message)` `=>` used for DHT storage messages

### other considerations at time of writing

I want to design the cache as a table of `node_id`s with a TTL strategy for eviction, but I also want to separate the eviction logic from the table structure itself.

### RPCs

* `FIND_NODE` and `PING` needed for key-based routing

