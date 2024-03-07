- 3 players / stakeholders
	- client
	- server
	- certificate authority
- Overall flow:
	- CA has the following private key (sk), public key (pk) and self-signed certificate.
	- Server also has a private key (sk) and public key (pk)
	- Server requests a cert from CA through a Certificate Signing Request (CSR). It contain's Server's public key.
	- CA **somehow verifies/validates** the information and sends a certificate signed by it (CA) to the server.
	- Summary: Server gets a cert signed by CA.
**Contents of a Certificate**
```
certificate data
---
signature algorithm
---
signature
```

certificate data has 7 pieces of data in it:
1. subject's public key
	1. rsa: modulus (product of primes from the previous module), exponent ("public key" from the math in the previous module)
	2. elliptic curve: public key, name of curve
2. issuer and subject in Distinguished Name format. Must include Common name (CN). If issuer = subject then we call it a self-signed certificate. CN used by browsers
3. x509 Version. 0 - Indexed 
4. validity: not before, not after
5. signature algorithm
6. extensions (v3)
7. Serial Number. Specific to a CA. Can ask a CA about it. Related to Open Certificate Status Protocol, Certificate Revocation List

signature algorithm:
- hashing algo used
- asymmetric encryption algo used for generating private and public key. **I THINK, BUT I'M NOT SURE THAT THIS ALGO ALSO SPECIFIES HOW HASH WAS ENCRYPTED.**

- Inspecting Certs
	- Summary, not explanation: Used OpenSSL to get reddit's cert and saw it in plaintext using openssl.


**creating a CA and certs**
- rsa key file had 8 things: modulus, public & private exponents, prime 1 & 2, exponent 1 & 2, coefficient
- 
