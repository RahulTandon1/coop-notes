
> [!NOTE] Control vs Data Plane 
> Src: https://www.cloudflare.com/learning/network-layer/what-is-the-control-plane/
Plane - where things happen
> Control plane - manage how data is forwarded
> Data plane (aka forwarding plane) - actually forwards data
>
> Software Defined Networking is enabled by this separation into Control and Data plane.
 
 
> [!info] MTU
> I probably shouldn't have looked this up. 
> L3 stuff. Differs with IPv4 and IPv6. Relation ICMP being used to inform/provide feedback to routers about whether things worked or not.
> Includes any headers as part of the size.
> Ipv4 has a `do not forward thing`
> 
> L4: MSS - Maximum segment size.

> ![info] Optical Switching
> - Control light signals using light signals. Requires what's called a non-linear 
> - Benefit: no heating; no power loss in converting back and forth between light-to-electrical signals.
> src: https://physics.duke.edu/introduction-all-optical-switching

----

## Page 1
- QKD establishes a symmetric key between 2 parties such that it cannot be broken by even a quantum computer.
- problem they're solving: how do you get QKD to scale for an enterprise-IT environment.
- how they're solving it:
	- Key Management Service which works in 4 layers and lets 2 parties across multiple "sites" create multiple sessions between each other.

## Page 2
- KMS features: data encryption scheme, network protocol
- Conventional public key crypto gets broken (Quantum threat)
- Why QKD?
	- Harvest now decrypt later attacks
	- Algorithmic advances
- Note on state of QKD
	- trusted node
	- need to answer P2P -> Network

> [!WARNING] Levels of security
> Information theoretic, theoretically secure, computationally secure ?





---
Questions:
- For simplicity we can assume that the topology of the classical network between all these nodes is the exact same as the quantum network between them. But what happens when the topologies are different. Does the process and security get affected if in the classical network there are routers, switches and other non-OpenQKDNetwork nodes in between these nodes (A, B, ... E)?


End goal: Key K is established between A and E.

I want to list all the steps required for establishing key K between A and E in detail:
0. A and B establish Keystream $K_{AB}$ over their quantum channel
1. B chooses key K by taking a subset from keystream $K_{AB}$
	1. B encrypts K using $K_{AB}$ as a one-time pad. We call this $E_{AB}(K)$.
	2. B sends this over the classical network to A.
	3. A decrypts this using $K_{AB}$. A now has the K in plaintext.
	4. Keystream $K_{AB}$ is now destroyed.
2. B and C establish keystream $K_{BC}$
	1. B encrypts K using $K_{BC}$ as a one-time pad . We call this $E_{BC}(K)$.
	2. B sends this over the classical network between itself and C.
	3. C decrypts this using $K_{BC}$. C now has K in plaintext.
	4. Keystream $K_{BC}$ is now destroyed.
3. C and D establish keystream $K_{CD}$
	1. C encrypts K by using $K_{CD}$ as a one-time pad . We call this $E_{CD}(K)$.
	2. C sends this over the classical network between itself and D.
	3. D decrypts using $K_{CD}$. D now has K in plaintext.
	4. Keystream $K_{CD}$ is now destroyed.
4. D and E establish keystream $K_{DE}$
	1. D encrypts K by using $K_{DE}$ as a one-time pad. We call this $E_{DE}(K)$
	2. D sends this over the classical network between itself and E.
	3. E decrypts this using  $K_{DE}$. E now has K in plaintext.
	4. Keystream $K_{DE}$ is now destroyed.
Since  both A and E now have K in plaintext they can communicate securely over the conventional network such that even a future quantum computer cannot break the encryption.