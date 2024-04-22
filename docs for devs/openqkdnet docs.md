**Assumptions about the reader**
You're a fullstack developer.

So what's the point of all of this?
Communication on the internet happens through networking protocols. We *secure* communication we usually rely on a protocol called TLS. This protocol adds the S in HTTPS. With the advent of Quantum Computers, the current mechanisms that TLS uses for security become obsolete. If you read through the NSERC grant proposal, you'll realize that we think there are broadly 3 approaches to this:
- Post Quantum Cryptography
- Information Theoretic Cryptography
-- Quantum Key Distribution.

Our team's approach is an AND not an XOR. We want PQC + QKD.

Note that I italicized "secure" in the paragraph above. By "secure" communication we usually refer to the following attributes:
- Confidentiality - only the 2 parties Alice and Bob know what's being talked
- Integrity -  @rahul
- Authentication - 
This is sometimes referred to as the CIA of security.


**Quick recap**: We want to make the future's web communication quantum-safe. Our take is PQC + QKD. We want to integrate this idea into TLS since it's the protocol that's used the most (think any HTTPS connection on the internet).
So how do we make use PQC and QKD in TLS?
The answer is somewhat coupled with some implementation details of TLS.

To secure communication, TLS does 2 broad steps:
1. Use asymmetric (aka Public Key Cryptography) to establish a shared secret
2. Use that shared secret for symmetric encryption.

That step 1 is what quantum computers will break. So we want to make it quantum-safe.
> Task: Somehow establish a shared secret in a quantum-safe way using PQC and QKD. Use it in the TLS handshake.

tl;dr we obtain 3 secrets on both sides:
- The normal shared secret TLS generates
- a shared secret from a PQC algorithm
- a shared secret from a QKD connection / network

We just concatenate the 3 and voila: we've got our quantum-safe shared secret.
The fact this this concatenation works and surrounding caveats exists are mentioned in Dr. Stebila's hybrid TLS Key Exchange RFC
---

**So what is OpenQKDNetwork**
We base our work on Professor Mosca's paper. The problem we solve is "how do we take QKD from a point-to-point to a network setup?" We don't implement all the features from the paper in our code, but certainly implement enough for a proof-of-concept.

**Re-iterating content from the paper**
- we use 4 layers for a separation of concerns:
-- application layer: this is the (OpenQKDNet's) user's code.
-- KMS layer: 
-- network layer: routing keys between nodes
-- link layer: actually talking to the hardware and getting keys.
 
---

**Getting to the code**
triple_key_encode thing
the SSL handshake
TLS 1.3 handshake. TLS comes in flavours.



---

What problem are we trying to solve?
What's our solution? Any lines of reasoning behind design decisions. Where are we in the current process?
What are the next tasks?
 

Description of attack
Setup:
- Hosts A and C are connected to site Alpha (OpenQKDNetwork node).
- Host B is connected to site Beta (OpenQKDNetwork Node).
- Host C knows that Host A is connected to site Alpha and host B is connected to site Beta. 
- Assume the index number associated with a key has a small upper limit - say 10. 
- Security of channels:
	- Host A and B are connected via HTTP (public channel).  // [this assumption might need revision]
	- A and Alpha are connected via HTTPS where the S = TLS is secured by PQC.
	- Similarly, C and Alpha are .... (same as above point)
	- Similarly, B and Beta are .... (same as above point)

Process:
Host A initiates a PQC+QKD TLS handshake with Host B.  
Host A sends its siteID (Alpha) in the TLS ClientHello message.
Upon receiving this, Host B requests a new key from site Beta's KMS by providing the siteID. B receives the `{key, its blockID and index number}`. To enable Host A to obtain the same key, host B sends these 3 pieces of information to Host A in ServerHello {blockID, index number, site ID}.

Since host C is already connected to site Alpha, it can make requests to Alpha's KMS.
Since index number is a small number, guessing it in not very difficult for C.

Question: In between site Alpha's KMS receiving the key from Beta's KMS, and host A requesting for it from site Alpha, can Host C brute force the blockID of the key meant for host A via requests to site Alpha's KMS?
If it can, then host C can act fake being host A in communication between A and B.


**Possible solutions**
#### Nonce/Transaction ID
Host A creates a transaction ID (nonce). In Client Hello it sends this nonce to B in the ClientHello. B hash

###
Additional Assumptions: 
- site Alpha (OpenQKDNetwork node) assigns a unique ID to each host connected to it. Note these IDs are local to a site/OpenQKDNetwork node and not unique across the entire network. Assume Alpha assigns unique IDs: A <-> 1, C <-> 2 and Beta assigns B <-> 1.

Revised flow:
- In ClientHello, A sends to B both `{siteID=alpha, hostID=1}`.
- B calls Beta's OpenQKDNet API `newkey(siteID=alpha, hostID=1)`. Note: we've added a param called hostID to the API. Beta gives B the `{blockNumber, index, key}`.
- In ServerHello: B returns to A: `{blockNumber, index, siteID=Beta}`. 
- A 


---

What's the end goal of OpenQKDNet? Extend QKD from a point-to-point connection to a network.


---
### How does the triple key exchange take place?
Client application registers libopenqkd's helper functions with OpenSSL at runtime.
Server application does the same with their copy of OpenSSL.
The OpenSSL that the client and server use have been modified to incorporate both QKD and PQC. OpenSSL <- OpenSSL + liboqs

When the client wants to establish a TLS 1.3 connection with the server the following happens


```
ctx = SSL_CTX_NEW() // defined in ssl_lib.c
SSL_new(ctx)
```

we have modified the `struct ssl_st` to contain new fields which are functions. (see `ssl_local.h`)


`SSL_set_oqkd_new_key_url_callback` in `ssl.h`

Also in `ssh_local.h`: oqkd_peer_msg in `ssl3_state_st`





# Key Flow
where is `RESP_GET_KP_BLOCK_INDEX` set as respOpID
and opID = REQ_POST_ALLOC_KP_BLOCK


