
## reviewing what works
### openqkdnet key exchange
In my first week we got this [Disable Spring Auth branch of qkd-net](https://github.com/Open-QKD-Network/qkd-net/tree/disable-spring-auth) to work. This involved ensuring that the two computers were reachable using netcat. We got the keys stuff to work.

[[week 1 - getting openqkdnet running]]

---


- 3 things need to come together: openssl, liboqs, and openqkdnet

hybrid kx: `apps/openssl s_client -groups p521_kyber1024 -CAfile ./ecdsa_CA.crt`

- but you need to build `libqkd.a` first

**Branches to use**:
- qkdnet: `disable-spring-auth`
- Open-QKD-Network's OpenSSL: `openqkdnetwork-clean`
- OpenQKDNetwork's LibOQS: `openqkdnetwork-clean`


need to make two changes:
1) in openssl/s_cb.c to add call back to call openqkdnetwork, please refer the change in s_cb.c in [https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5#diff-f03f8bc179a721051a6d4[…]8aaaffe192eb834c7a17eb324de](https://github.com/Open-QKD-Network/openssl/commit/2c0073f5d56b428cd3c7ea6ca28721391e160ee5#diff-f03f8bc179a721051a6d46e2c768652bec7618aaaffe192eb834c7a17eb324de) for how to add call back
2) make change as needed in /[https://github.com/Open-QKD-Network/qkd-net/blob/disable-spring-auth/applications/api/openqkd.c](https://github.com/Open-QKD-Network/qkd-net/blob/disable-spring-auth/applications/api/openqkd.c)

**The Task**
Need to make changes in `openqkdnetwork-clean` branch. (I think OpenSSL)

**Understanding**
### in OpenSSL -> `openqkd-bc` branch -> s_cb.c
file - callback functions used by s_client and s_server.
3 functions
```c

int oqkd_new_key_url_callback(char** url, int *len); // used s_client.c
int oqkd_new_key_callback(char* new_key_url, char** key, int *key_len, char ** get_key_url); //  s_server.c
int oqkd_get_key_callback(get_key_url, key, key_len); // s_client.c
```


**Testing Changes**
- OpenSSL s_client / s_server


## understanding code
all the 3 repos are those of OpenQKDNetwork

libopenqkd (src:`qkd-net/applications/api/openqkd.c`) has the following interface
```
oqkd_get_new_key_url
oqkd_new_key
oqkd_get_key
```

---
---
> learning how openssl generates the name group and key share extensions in the source code
> source code: 
> - OpenQKDNet's OpenSSL repo. `openqkdnetwork-clean` branch
> - `openssl/ssl/statem/extensions_clnt.c
> - functions to read: `tls_construct_ctos_supported_groups`, `add_key_share`

We made new functions:
```C
void SSL_set_oqkd_new_key_url_callback(SSl *s, int (*callback) (char **url, int* len))

void SSL_set_oqk_oqkd_get_key_callback(
SSL *s, 
int (*callback) (char* get_key_url, char ** key, int* keylen)
)

void SSL_set_oqkd_new_key_callback(SSL *s, int (*callback)(char * new_key_url, char** key, int* keylen, char** get_key_url))
```

