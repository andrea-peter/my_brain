# Openssl

### How to

#### Generate key pair

```
openssl genrsa -out rsa_private.key 4096
```

#### Generate certificate signing request

```
openssl req -new -key rsa_private.key -out rsa_csr.csr
```

#### Create self-signed certificate

```
openssl req -new -x509 -days 365 -key rsa_private.key -out rsa_certificate.crt
```
