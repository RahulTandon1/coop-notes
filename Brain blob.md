**What "things" (protocols) make the Internet secure?**
- IPSec
- TLS (was called SSL) & DTLS
- Kerberos
- Simple Network Management Protocol

These operate at different levels of the OSI model - just a framework for thinking about networks in general. The idea being that we want abstraction. Devices & protocols at different layers have different purposes:
- transporting bits // Layer 1 Physical
- ensuring I can send bits to a particular direct peer node. // Layer 2 Data Link
- ensuring I can send data to a non-direct peer node // Layer 3 Network
- ensuring I can send data to a particular application running on a non-direct peer node. // Layer 4 Transport
- just let applications do their thing // Layer 5 Application.
 (Not getting into the layers 5, 6 and 7). 


