
### Week 1 (Jan 8th - Jan 12th)
- Learnt about `netcat` and `netstat` linux networking commands.
- Got OpenQKDNet running on the 2 Dells (both of which run Ubuntu).
We run OpenQKDNet and got alice and bob working. The end result looked something like this:

![[media/Screenshot from 2024-02-09 16-26-50.png]]


### Week 2 (Jan 15th - Jan 19th)

Assigned tasks:
- TLS handshake [https://github.com/open-quantum-safe/openssl?tab=readme-ov-file#tls-demo](https://github.com/open-quantum-safe/openssl?tab=readme-ov-file#tls-demo)
- Open wireshark to understand the handshake
- https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/hybrid_key_exchange.md
- [https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/oqs-template/generate.yml](https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/oqs-template/generate.yml)
- to learn TLS 1.3: [https://tls13.xargs.org/](https://tls13.xargs.org/)

What I did:
- Tried doing a Cryptography 101 by running through the Practical Networking [Practical TLS youtube playlist](https://www.youtube.com/playlist?list=PLIFyRwBY_4bTwRX__Zn4-letrtpSj1mzY)
- In order to understand KEMs I tried reading a bit of Real World Cryptography's chapter on Asymmetric Encryption & Hybrid encryption but it went over my head. Kaiduan gave me a clarifying diagram for how KEMs work.
- Learnt about GDB. Used it to debug through the main method of OpenSSL (compiled with liboqs). This was for demonstration purposes & getting familiar with GDB rather than solving an issue.
- Got introduced to the overall project & the NSERC alliance.
- Used wireshark
![[Screenshot from 2024-01-18 15-16-40.png]]

![[Screenshot from 2024-01-18 15-15-03.png]]
### Week 3 (Jan 22nd - Jan 26th)

**Assigned tasks**
- learn how openssl generates the name group and key share extension in the source code
	- https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L195: function `tls_construct_ctos_supported_groups`
	- https://github.com/Open-QKD-Network/openssl/blob/openqkdnetwork-clean/ssl/statem/extensions_clnt.c#L609: function `add_key_share`
- Understand how we modified the original OpenSSL implementation of the TLS key exchange in the OQS fork of OpenSSL

**Work I did**
- Learnt how to use OpenSSL from the [OpenSSL Cookbook](https://www.feistyduck.com/library/openssl-cookbook/online/). Earlier I was just copy-pasting commands from readmes. Here, I was trying to understand how to use OpenSSL & what interface it provides.
- Ran into a compiler error when compiling Open-QKD-Network fork of OpenSSL
- Got the OQS fork of OpenSSL to work. Used GDB to get a call stack for `tls_construct_ctos_supported_groups`. 
- Attended the first Act2Qrypt presentation.
- 

### Week 4 (Jan 29th - Feb 2nd)
**Work assigned**
**Triple Key Exchange**
- read openqkd.c code to understand what change I need to make
- test my change using the test program in the api directory
- then integrate with openQKDNetwork and OpenSSL/libOQS
	- build`libqkd.a`
	- then build OpenSSL statically
- Helpful link: [https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md](https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md)
- Read through this [OQKD-libOQS-SSL integration document](https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/oqkd-liboqs-ssl-integration.pdf)
- need to run: `apps/openssl s_client -groups p521_oqkd_kyber1024 -CAfile ./ecdsa_CA.crt` for the triple key exchange.

**Non Triple Key Exchange**
- get the bob and alice file transfer working with OpenQKDNetwork disable-spring-auth branch
> reflecting: I initially misunderstood that I was required to do the file transfer using the triple key exchange. Figuring out what I had to do was the tough part.

- read as much code of the [tls-kms-demo](https://github.com/Open-QKD-Network/qkd-net/tree/disable-spring-auth/applications/tls-kms-demo/src) as possible
- read a bit of [LSRPRouter.java]([https://github.com/Open-QKD-Network/qkd-net/blob/disable-spring-auth/qnl/key-routi[…]ervice/src/main/java/com/uwaterloo/iqc/qnl/lsrp/LSRPRouter.java](https://github.com/Open-QKD-Network/qkd-net/blob/disable-spring-auth/qnl/key-routing-service/src/main/java/com/uwaterloo/iqc/qnl/lsrp/LSRPRouter.java#L164)) in order to understand what might've gone wrong with Karlo's OpenQKDNet installation.
- learn Java JSON reader API: `com.google.gson.Gson` and `com.google.gson.stream.JsonReader`.



| Day                 | Work done                                                                                                                                    |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, 29th Jan    | - Got introduced to how OpenSSL talks to OpenQKDNet for the triple key exchange in a meeting with Kaiduan.<br><br>                           |
| Tuesday, 30th Jan   | Got the Alice & Bob demo working after the weekly meeting.                                                                                   |
| Wednesday, 31st Jan | Kaiduan and I had a meeting with Karlo from the University of Zagreb to help him debug an issue.                                             |
| Thursday, 1st Feb   | - Had another meeting with Karlo.<br>- Got OpenQKDNetwork to work in the office. We got a new UW-Lab wifi set up with the UW IST's help.<br> |
| Friday, 2nd Feb     |                                                                                                                                              |


### Week 5 (Feb 5th - Feb 9th)
**Assigned work**
- Continue working on triple key exchange (OpenSSL/OpenQKDNetwork/LibOQS integration)
- understand the OpenSSL call back to interact with OpenQKDNetwork (section 7 & 8 of the integration document)
- read change to `s_bc.c` in [this commit](https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5)
- Make two changes 
	1) in openssl/s_cb.c to add call back to call openqkdnetwork. Refer to the commit linked above.
	2) as required in [openqkd.c](https://github.com/Open-QKD-Network/qkd-net/blob/disable-spring-auth/applications/api/openqkd.c)
- refer to the following pieces of code for the changes:
	- [a particular line in s_client.c of openqkd-bc branch of OpenQKDNet's OpenSSL fork](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_client.c#L1995
	- [particular line of s_server.c of same branch](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_server.c#L2299)
	- [implementation of oqkd_new_key_url_callback in s_cb.c](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1004)
	- [impl. of oqkd_new_key_callback (same file)](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1021)
	- [impl. of oqkd_get_key_callback](https://github.com/Open-QKD-Network/openssl/blob/openqkd-bc/apps/s_cb.c#L1047)

**Work I did**
- Meeting with UCalgary team on Thursday Feb 8th
- Tried following the instructions in [openqkd.md]([https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md](https://github.com/Open-QKD-Network/openvpn/blob/pqcrypto/openqkd.md)) given in the previous week. Ran into an issue when compiling `openqkd.c`. Kaiduan clarified which branches I need to be working on.
- Got a lot of clarifying instructions from Kaiduan for next week.

### Week 6 (Feb 12th - Feb 16th)
**Assigned work**
- [BasQuaNa webinar](https://www.qkdnetworkcanadauk.com/webinar)
- [Kaiduan's 2021 ETSI slide deck](https://github.com/Open-QKD-Network/openssl/blob/openqkd/openqkd/ETSI_QUANTUM2021_kaiduan-xie.pptx)
- (optional; for my curiosity): cqp-openqkd integration.pdf

**Work I did**
- I thought I got the sample chat app (s_client & s_server) to work using the triple key exchange on Monday night, but I found out in Wednesday's meeting that wasn't the case. OpenQKDNet wasn't being called at all.
- Tuesday: learnt how to use tcpdump; generated packet captures (pcap) of key exchange & inspected them in Wireshark. Wrote out an explanation (in slack messages) which explained the client & server key_shares. Wrote [a file]([https://gist.github.com/RahulTandon1/df63681158811d8318441c88cca861fa](https://gist.github.com/RahulTandon1/df63681158811d8318441c88cca861fa)) of the (somewhat incorrect) steps I followed. 
- Wednesday: Kaiduan linked me to [Issue 34's openqkd.c]([https://github.com/Open-QKD-Network/qkd-net/blob/issue-34/applications/api/openqkd.c](https://github.com/Open-QKD-Network/qkd-net/blob/issue-34/applications/api/openqkd.c))
- Thursday & Friday - travelled to Montreal. Tried getting the triple key exchange to work. Honestly didn't do a lot of work. Made up for it after coming back.
Met with Dr. Stebila in order to figure out what I'm required to do/present next week.
### Week 7 (Feb 19th - Feb 23rd)

| Day       | Work                                                                                                                                                                                                                                                                                              |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday    | Family day. Travelled to Calgary.                                                                                                                                                                                                                                                                 |
| Tuesday   | - Attended the Academic Investigators Meeting at UCalgary <br>- Prepared for it by attempting to read through Professor Mosca's [4 Layer architecture paper](https://arxiv.org/abs/1712.02617)<br>- Discovered that MDI QKD has a third untrusted node that OpenQKDNet might need to account for. |
| Wednesday | Quantum Days - Day 1<br>Informed Kaiduan about the Charlie issue. Concluded that we can treat it as a black box.                                                                                                                                                                                  |
| Thursday  | Quantum Days - Day 2.<br>Prepared for a meeting with Dr. Oblak's team, but unfortunately got cancelled as we discovered a conflict of interest.<br>We concluded that we'll both build to the ETSI QKD standard.                                                                                   |
| Friday    | Quantum Days - Day 3. Returned to Waterloo.                                                                                                                                                                                                                                                       |
### Week 8 (Feb 26th - March 1st)

| Day                 | Work                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, 26th Feb    | - Ran into the same bug as Week 6 when compiling openqkd.c. Commented out `curl_easy_setopt(handle, CURLOPT_SSL_EC_CURVES, "p521_kyber1024");`<br>- Talked to Kaiduan and realized I shouldn't be building a shared library. ( I had gotten confused by the instructions in openqkd.md)                                                   |
| Tuesday, 27th Feb   | - Kaiduan sent me a very well written explanation of the overall triple key exchange. Also shared the [ETSI API standard](https://www.etsi.org/deliver/etsi_gs/QKD/001_099/014/01.01.01_60/gs_qkd014v010101p.pdf)<br>- Tried the 3 key ex. by building a static library. Realized that the basic OpenQKDNet tls-kms-demo was not working. |
| Wednesday, 28th Feb | - Debugged and realized I hadn't stopped jicofo & jitsi.                                                                                                                                                                                                                                                                                  |
| Thursday, 29th Feb  | - Sent an email to the Calgary team to inquire about ETSI API support.<br>- Continued work on triple key exchange                                                                                                                                                                                                                         |
| Friday, 1st March   | - Ran into an issue with s_client not working. Had a call with Kaiduan. I wasn't passing the IP addr/port number to s_client.<br>- Talked about a possible brute force attack by a fellow host within the same site to another host.                                                                                                      |

### Week 9 (March 4th - March 8th)
Work assigned:
- Port code from issue-34's libopenqkd code to disable-spring-auth branch.
- Write my own documentation to help my understanding
- think about defence for the brute force attack
- start reading ETSI standard and find the difference between UW API standard and ETSI standard. Find potential issue in ETSI standard
- think about modifications to QNL layer to use ETSI REST API
- understand OpenQKDNet properly

| Day                  | Work                                                                                                                                                                                                                                      |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, 4th March    | - Finally got triple key exchange to work & showed it to Kaiduan on a call.<br>- Discussed the possible attack<br>- Ported the`issue-34` openqkd.c to `disable-spring-auth`                                                               |
| Tuesday, 5th March   |                                                                                                                                                                                                                                           |
| Wednesday, 6th March | - Had a meeting with Kaiduan and Sarah on the possible attack.<br>- Sent a written explanation of the attack on Slack. Kaiduan pointed out a grave error in the phrasing of the explanation and told me to ensure I understand OpenQKDNet |
| Thursday, 7th March  | Revisited my understanding of OpenQKDNet                                                                                                                                                                                                  |
| Friday, 8th March    | Asked questions regarding trusted node relays from the 4 layer architecture paper.                                                                                                                                                        |

### Week 10 (March 11th - March 15th)

| Day                   | Work                                                                                                                                                                                                                                                                                        |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, 11th March    | - Asked a lot of questions related to the ETSI standard in Slack.<br>- Continued reading the 4 layer arch. paper; in particular`High level Procedures in the Communication Systems` section.                                                                                                |
| Tuesday, 12th March   | - Discussed the questions with Kaiduan in my weekly meeting.<br>- Next tasks: <br> > read the OpenQKD Key flow document; find the mapping to the code<br> > Got a book on Netty to read for the changes to the QLL/QNL.<br>                                                                 |
| Wednesday, 13th March | - Got a clarification on SAEs & KMEs behaviour (security-wise) from Dr. Lütkenhaus: all SAEs connected to a KME act nicely, so they won't attack each other.                                                                                                                                |
| Thursday, 14th March  | Reading the Preface of Netty in Action made me realize I should know multithreading in Java. Found a course on it.<br>Speed running through [Mosh's Advanced Java course](https://codewithmosh.com/p/ultimate-java-part-3) to get familiar with Multi threading & asynchronous programming. |
| Friday, 15th March    | Continuing the course.                                                                                                                                                                                                                                                                      |

### Week 11 (March 18th - March 22nd)
Doing the course entails: watching the video, taking some notes, experimenting with some examples on my laptop to get my hands dirty.

| Day                        | Work                                                                                      |
| -------------------------- | ----------------------------------------------------------------------------------------- |
| Monday, Tuesday, Wednesday | Finished the course.                                                                      |
| Thursday                   | Started reading the book [Netty in Action](https://www.manning.com/books/netty-in-action) |
| Friday                     | Continued reading the book.                                                               |

### Week 12 (March 25th - March 29th)

| Day                                                               | Work Done                                                                                                                                                                                                                                                                                                         |
| ----------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, Tuesday, Wednesday                                        | Still reading through the book & taking some notes.                                                                                                                                                                                                                                                               |
| Thursday, 28th April                                              | - Prep for meeting with Dr. McCarthy: reading through the [4 layer architecture paper](https://arxiv.org/abs/1712.02617)                                                                                                                                                                                          |
| Friday, 29th March                                                | Good Friday. Holiday.                                                                                                                                                                                                                                                                                             |
| Sunday, 31st March<br>(making up for slow progress with the book) | Got some sample netty code from the book running on my laptop. This is different from the passive reading I had been doing before this. It's also different from directly running examples from the book's [github repo](https://github.com/normanmaurer/netty-in-action/). I got my hands dirty with `pom.xml`s. |

### Week 13 (April 1st - April 5th)

| Day                 | Work Done                                                                                                                                                                                                                                                                                                                                   |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, 1st April   | - Revisiting key flow to brainstorm architecture change. <br> -> debugged through key flow by adding log statements, pushing to [my github](https://github.com/RahulTandon1/annotated-qkd-net), pulling the Computer Science Club's VMs and using them to debug.<br><br>- Work on presentation (slides, video, pcap) for Wednesday meeting. |
| Tuesday             | After 11 AM: preparing for the presentation the next day.                                                                                                                                                                                                                                                                                   |
| Wednesday           | Spent the day preparing the presentation for the bi-monthly Act2Qrypt.                                                                                                                                                                                                                                                                      |
| Thursday, 5th April | Ended the day by realizing that all the keys from the qll are hardcoded in `.qkd/qnl/qll/keys`.                                                                                                                                                                                                                                             |
| Friday, 5th April   | - Re-read a small section of the ETSI standard.<br>- Brainstormed possible solutions. Realized I wasn't solving the right problem<br>- Had a call with Kaiduan which brought clarity about the problem I'm meant to solve. I think it might be a variation of the Two General's Problem.                                                    |

### Week 14 (April 8th - April 12th)
Started at 9:34 

| Day                   | Summary                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Monday, April 8th     | - Did a cursory reading through the [Two General's Problem](https://en.wikipedia.org/wiki/Two_Generals%27_Problem), and [TCP's wikipedia page](https://en.wikipedia.org/wiki/Transmission_Control_Protocol) to confirm that our problem might be impossible to solve perfectly.<br>- Used TCP's closing mechanism as inspiration to suggest a possible mechanism for us<br>- Filled the early parts of this document by going through Slack messages. |
| Tuesday, April 9th    | - Finished filling the incomplete parts of the Work Log before the weekly meeting.                                                                                                                                                                                                                                                                                                                                                                    |
| Wednesday, April 10th |                                                                                                                                                                                                                                                                                                                                                                                                                                                       |


### Week 15 (April 15th - April 19th)
Wednesday - sped through Netty in Action. Need to modify the encoding & decoding of QNL Requests & Responses. Also want to come up with a better dev workflow, instead of git push, git pull, recompile, run qkd-net, run sample app, check logs.

Task for tomorrow:
- speed run bytebuf section
- figure out how to mock a QNLREs/response and use it to test ChannelHandlers.

Thursday
- Took me like all day to read through the bytebuf section. In retrospect maybe this was unnecessary.
- Got started on writing a test for RequestDecoder. I think there might be a bug in the decoder. Got partway through a fix but got into errors related to how maven is configured.

### Week 16 (April 23rd - April 26th)