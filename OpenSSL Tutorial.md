- use `genpkey` over `genrsa`
3 steps for getting a signed cert:
1. generate a private key
2. send a certificate signing request, get a certificate from CA
3. install CA on server.

**Generating a private key**
choices to make: 
- algo? 
- key size / curve
- password protection scheme

getting a certificate:
```bash
openssl \
s_client
-connect website.com:443
```

viewing a certificate in human-readable text:
```bash
openssl \
x509 \ # use the x509 subcommand
-in <file_path> \
-noout \ # do not give me the base 64 output
-text
```

viewing the private key: `openssl pkey -in <file> -text -noout`
viewing CSR: `openssl req -text -in fd.csr -noout`

`.csr` -> certificate signing request
`.cnf` -> config
