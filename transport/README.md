# Transport

TCP has a number of problems including but not limited to:
* threeway handshake to initiate communication
* head-of-line blocking on packets (and an inability to foster multiple streams over a single connection)
* exponential backoff set by TCP's timeout and retransmission mechanism, see [chen's blog](https://goalsharp.com/the-points-of-tcp-retransmission-you-must-know/)

> Martin Seemann's talk on [QUIC in libp2p](https://youtu.be/4FvMed5iCb4?t=14) discusses these problems at greater length

## EFCP

[EFCP](https://ieeexplore.ieee.org/document/8685905) is part of the RINA effort to create a more reliable, robust, and extensible internet.

[`rust-p2p/efcp`](https://github.com/rust-p2p/efcp) strives to make EFCP available in user space for applications tied to the existing TCP/UDP/IP infrastructure.

## Disco

Rather than layering EFCP with TLS for encryption, this transport will opt for lightweight, yet robust cryptography with [`rust-p2p/disco`](https://github.com/rust-p2p/disco). David Wong gave a good talk about permutation-based cryptography at Black Hat 2018: [Fed Up Getting Shattered and Log Jammed? A New Generation of Crypto is Coming](https://www.youtube.com/watch?v=bTGLO4obxco&feature=youtu.be&t=1).