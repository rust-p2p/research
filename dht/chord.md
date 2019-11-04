# Chord: A Scalable P2P Lookup Service
> [paper](https://pdos.csail.mit.edu/6.824/papers/stoica-chord.pdf), [blog post by oskar](https://oskarth.com/notes-on-chord/)

Chord uses *consistent hashing* to enforce even distribution of keys, even in the presence of high node churn.

The network topology is a ring of nodes. The lookup algorithm returns a node recursively until it reaches the node storing the value. If a node does not have the value, it points in the right direction, thereby leading to the eventual recovery of the value.