- Key exchange via asymmetric encryption

doblak@ucalgary.ca


## TLS 1.3 Key Exchange


### Pre Shared Key
- Implements the Session Resumption feature of TLS 1.2
- 3 variations of handshake possible
**Basic PSK Mode handshake**
problem: does not provide forward secrecy

**PSK + (EC)DHE Mode**
- Perform an DH Key Exchange in addition to using the PSK
- Provides Forward Secrecy
- Time: 1 RTT

PSK + Early Data
- no forward secrecy. Not delving into this
- Time: 0 RTT

**PSK + (EC)DHE Mode + Early Data**
- forward secrecy provided for application data but not early data. Attacks possible.
- Time: 0 RTT