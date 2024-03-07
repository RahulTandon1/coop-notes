Client has 2 questions:
- Is is a valid cert?
- Is the sender (server) the true owner of the cert. Equiv. to asking do they have the corresponding private key?

**Valid cert question**
- Browser and/or OS has a list of self-signed certs of CAs that it trusts. We learnt that a cert has the subject's public key. We client has the public key of the root CA.


**CAs**: There are CAs in the middle which form a chain using the subject-issuer relationship. Intermediate CA aka Subordinate CA aka.

Why do we have intermediate CAs?
- security of private key of root CA. Least usage funda.
- Easier to make changes if a cert auth goes bad. Software updates funda.

*Which certs get sent to the client?*


Basic Constraints
- even if something down stream intentionally/unintentionally ends up giving `CA=true` credentials, things upstream can limit this.
- 2 params: path length, ca = true/false.


**Types of Certificates** (DV, OV, EV)
- Domain validation
	- can be automated (Let's Encrypt)
	- challenge: email, expose a webpage on a certain path etc.
- Organization Validation -> in addition to domain validation, checks tax/legal/official documents to ensure domain owned by org
- Extended Validation

**Certificate Revocation**
overall problem: if private key gets erased, oopsie.
- CRL - too slow. Google Chrome didn't  follow it.
- OCSP  - 
	- problem: client's search history + ocsp server needs to be crazy good. 200k requests/s rate mentioned for Google.
- OCSP Stapling 
	-  better but not perfect. Burden of proof back on server.

DOUBTS: So to establish a HTTPS connection, I need SSL/TLS. In the OSCP case, I need to make an HTTP connection to check the validity of a certain cert...so I can make an HTTPS connection. Does that make sense? Speed?


