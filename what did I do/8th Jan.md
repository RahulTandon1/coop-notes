- [https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/ETSI_QUANTUM2021_kaiduan-xie.pptx](https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/ETSI_QUANTUM2021_kaiduan-xie.pptx)  
- [https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/OpenQKD-Network-2020-10-10.pptx.pdf](https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/OpenQKD-Network-2020-10-10.pptx.pdf)  
- The OpenQKDNetwork code
	- [https://github.com/Open-QKD-Network/qkd-net/tree/disable-spring-auth](https://github.com/Open-QKD-Network/qkd-net/tree/disable-spring-auth)  
	- [https://github.com/Open-QKD-Network/openssl/tree/openqkd/openqkd](https://github.com/Open-QKD-Network/openssl/tree/openqkd/openqkd)  

  The IETF draft
[https://datatracker.ietf.org/doc/draft-ietf-tls-hybrid-design/](https://datatracker.ietf.org/doc/draft-ietf-tls-hybrid-design/)
---
Terminology
- ECDH - Elliptic Curve Diffie Hellman
- FIPS Compliance - Federal Information Protection Standard


Takeaways:
> The PQC algorithms are used to generate keys and encrypt information in a way that is safe against quantum computers, while the QKD systems manage and distribute said keys among a network in a secure way.

QKD systems are managing keys created by PQC algos in a network.

4 layers
- User layer
- Key management service
	- multiple nodes
	- "policy engine" for keys
	- key pool
- Q. Network layer
	- "control plane" technology suite
	- "data plane" technology suite
	- multiple nodes
- Q. Link Layer