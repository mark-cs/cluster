# CA Certificate

[cfssl](https://github.com/cloudflare/cfssl) is used to generate CA certificates.

The CA certificate configuration is stored in `ca.json`.

Generate the key and certificate by running:

```bash
cfssl gencert -initca ca.json | cfssljson -bare ca
```

This will output:
 - ca.csr - certificate signing request for the CA
 - ca.pem - CA certificate in PEM format.
 - ca-key.pem - CA key in PEM format.