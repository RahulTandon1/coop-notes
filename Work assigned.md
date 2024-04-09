- Read the powerpoint sent by Kaiduan
- read documentation on liboqs
- [https://github.com/open-quantum-safe/openssl?tab=readme-ov-file#tls-demo](https://github.com/open-quantum-safe/openssl?tab=readme-ov-file#tls-demo)
- [https://github.com/open-quantum-safe/openssl](https://github.com/open-quantum-safe/openssl)
- [https://openquantumsafe.org/](https://openquantumsafe.org/)
- [https://github.com/open-quantum-safe/liboqs/blob/main/tests/example_kem.c](https://github.com/open-quantum-safe/liboqs/blob/main/tests/example_kem.c)
- Crystals-Kyber PDF
- Image of how KEM functions
- Read the [Hybrid Key Exchange in TLS 1.3 IETF draft](https://datatracker.ietf.org/doc/draft-ietf-tls-hybrid-design/
- Learn GDB
- learning how openssl generates the name group and key share extension in the source code
	- [https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L195](https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L195)
	- [https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L609](https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L609)
- [Hybrid Key Exchange . md](https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/hybrid_key_exchange.md)
- try to understand the hybrid key exchange code change
- Kaiduan sent image of OpenSSL, OpenQKDNet integration
- [https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md](https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md)

- build OpenSSL static
- build `libqkd.a` first
- read openqkd.c code first
- use test program in api directory to test changes.
- read all code in tls-kms-demo
- read changes in s_cb.c to add callback to OpenQKDNet [https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5#diff-f03f8bc179a721051a6d4[…]8aaaffe192eb834c7a17eb324de](https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5#diff-f03f8bc179a721051a6d46e2c768652bec7618aaaffe192eb834c7a17eb324de)
- read through the following:
- [https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_client.c#L1995](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_client.c#L1995)

[https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_server.c#L2299](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_server.c#L2299)

[https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1004](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1004)

[https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1021](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1021)

[https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1047](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1047)


- read CQPToolkit OpenQKD Integration PDF
- [https://www.qkdnetworkcanadauk.com/webinar](https://www.qkdnetworkcanadauk.com/webinar)
- https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/ETSI_QUANTUM2021_kaiduan-xie.pptx


- tcpdump, wireshark
- `curl_easy_setopt(handle, CURLOPT_SSL_EC_CURVES, "p521_kyber1024");` used for HTTPS connection to OpenQKDNet node.
- [etsi standard]([https://www.etsi.org/deliver/etsi_gs/QKD/001_099/014/01.01.01_60/gs_qkd014v010101p.pdf](https://www.etsi.org/deliver/etsi_gs/QKD/001_099/014/01.01.01_60/gs_qkd014v010101p.pdf)
-  Port code from issue-34's libopenqkd code to disable-spring-auth branch.
- Write my own documentation to help my understanding
- think about defence for the brute force attack
- start reading ETSI standard and find the difference between UW API standard and ETSI standard. Find potential issue in ETSI standard
- think about modifications to QNL layer to use ETSI REST API
- OpenQKDKey flow.pdf
- learn netstat, netcat
- [https://tls13.xargs.org/](https://tls13.xargs.org/)
- https://qkdwinter24.slack.com/archives/D06D4VCRP98/p1705600854847679?thread_ts=1705597578.361479&cid=D06D4VCRP98
- [https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/oqs-template/generate.yml](https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/oqs-template/generate.yml)
- google make vs make -j and why we get an error
-  openssl/liboqs/openqkdnetwork integration: [liboqs-openssl-openqkdnet integration.pdf]([https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/oqkd-liboqs-ssl-integration.pdf](https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/oqkd-liboqs-ssl-integration.pdf)
- read the change in s_cb.c: [https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5](https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5). openqkd-bc branch
- `!2010` style bash history command
- [https://github.com/Open-QKD-Network/openssl/commit/a1cdf9e5ed1e8dc02d1391c24b4cb5166b74cfd1](https://github.com/Open-QKD-Network/openssl/commit/a1cdf9e5ed1e8dc02d1391c24b4cb5166b74cfd1)
- [https://github.com/Open-QKD-Network/openssl/commit/7acd1f6e0a0a8615d34034175d37c581eb3998ef](https://github.com/Open-QKD-Network/openssl/commit/7acd1f6e0a0a8615d34034175d37c581eb3998ef)
	- need to make change in s_cb.c in openqkdcleanup branch
	- 
- [https://github.com/Open-QKD-Network/openssl/blob/openqkd/ssl/statem/extensions_clnt.c#L678](https://github.com/Open-QKD-Network/openssl/blob/openqkd/ssl/statem/extensions_clnt.c#L678)
- hy