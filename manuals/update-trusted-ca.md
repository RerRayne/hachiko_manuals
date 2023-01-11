# Update Trusted Certificate Authority

*Short guide on updating trusted CA from scratch*

## Obtaining of a Root Certificate

There are multiple ways to get a certificate of CA (aka Certificate Authority).
The only limitation is that certificate should be obtained over protected
communication channel from a trusted source.

1. Fetch certificate directly from PKI (aka Public Key Infrastructure).
   ```shell
   curl -k -o Skoltech_CAIT_Root_CA.der \
       https://vault.skoltech.ru/v1/pki/root/ca
   openssl x509 -in Skoltech_CAIT_Root_CA.der -inform der > Skoltech_CAIT_Root_CA.crt
   ```
2. Fetch certificate from Hachiko Manuals repo.
   ```shell
   curl https://github.com/RerRayne/hachiko_manuals/raw/master/ca/Skoltech_CAIT_Root_CA.crt
   ```
3. Download root certificate manually or ask a friend (e.g. from this repo).

From here and onwards, we assume that certificate's filename is
`Skoltech_CAIT_Root_CA.crt`. One can verify certificate signature with the
following command. All fields have to match.

```shell
$ openssl x509 -in Skoltech_CAIT_Root_CA.crt -noout -text
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            14:50:c7:f2:6b:04:eb:4c:f9:18:77:5e:7d:2d:28:a3:70:47:97:2b
        Signature Algorithm: ecdsa-with-SHA384
        Issuer: C = RU, L = Moscow, O = Skoltech CAIT, CN = Skoltech CAIT Root CA
        Validity
            Not Before: Dec 31 23:48:38 2022 GMT
            Not After : Dec 28 23:49:08 2032 GMT
        Subject: C = RU, L = Moscow, O = Skoltech CAIT, CN = Skoltech CAIT Root CA
        Subject Public Key Info:
            Public Key Algorithm: id-ecPublicKey
                Public-Key: (384 bit)
                pub:
                    04:d5:42:0f:a8:78:74:2b:10:2d:e1:d5:c3:74:7f:
                    19:ed:98:47:28:5c:8d:66:f8:6c:5a:36:84:01:2f:
                    af:ef:e7:0e:fb:78:2c:c2:20:81:a3:68:87:b3:2a:
                    3e:95:f0:28:c1:87:05:9c:c0:02:a7:6a:02:7c:12:
                    b1:4d:65:4e:8c:31:60:0c:6c:a4:4e:8a:2d:70:00:
                    04:56:61:14:25:cb:0d:60:4d:d3:ac:45:8e:20:cf:
                    51:64:5d:0e:48:c0:aa
                ASN1 OID: secp384r1
                NIST CURVE: P-384
        X509v3 extensions:
            X509v3 Key Usage: critical
                Certificate Sign, CRL Sign
            X509v3 Basic Constraints: critical
                CA:TRUE
            X509v3 Subject Key Identifier:
                9D:48:E2:66:14:70:79:10:FE:24:09:E4:2E:E9:AF:90:40:65:7C:BB
            X509v3 Authority Key Identifier:
                9D:48:E2:66:14:70:79:10:FE:24:09:E4:2E:E9:AF:90:40:65:7C:BB
    Signature Algorithm: ecdsa-with-SHA384
    Signature Value:
        30:66:02:31:00:b8:f1:1f:08:0d:e2:e1:72:da:8d:07:52:f3:
        70:d0:6b:30:6d:7c:f9:8b:1b:d2:c4:7b:a6:12:52:8f:aa:7f:
        5d:1e:e4:38:b2:23:d3:b3:ae:00:a0:ed:76:b7:e3:03:48:02:
        31:00:db:85:d9:3a:cd:a7:5f:02:b8:87:cb:32:a5:08:af:34:
        c6:69:0c:f6:1c:42:ce:7f:1e:c3:57:be:91:ec:0e:2a:5b:f9:
        b1:f2:8c:b3:b7:92:d1:2c:85:f2:1e:a1:6b:42
```

## Fedora-based toolkit (Fedora, Arch, etc)

These Linux distros uses `p11-kit` tool to manage trusted certificates (see
`man p11-kit`) for details). So, run the following command as root.

```shell
sudo trust anchor --store Skoltech_CAIT_Root_CA.crt
```

And check that it is among trusted certificates.

```shell
trust list --filter pkcs11:id=%9D%48%E2%66%14%70%79%10%FE%24%09%E4%2E%E9%AF%90%40%65%7C%BB
pkcs11:id=%9D%48%E2%66%14%70%79%10%FE%24%09%E4%2E%E9%AF%90%40%65%7C%BB;type=cert
    type: certificate
    label: Skoltech CAIT Root CA
    trust: anchor
    category: authority
```

## Debian-based toolkit (Ubuntu, Mint, etc)

Others Linux distros uses `update-ca-certificates` tool for trusted
certificates management (see `man update-ca-certificates` for details). In
order to add Skoltech's root CA as trusted system-wide, one should run the
following lines as an example.

```shell
sudo mkdir -p /usr/local/share/ca-certificates
sudo cp Skoltech_CAIT_Root_CA.crt /usr/local/share/ca-certificates/Skoltech_CAIT_Root_CA.crt
sudo update-ca-certificates
```

Verification could be done with direct listing of a directory of trusted
certificates as follows.

```shell
$ ls /etc/ssl/certs/Skoltech_CAIT_Root_CA.pem
/etc/ssl/certs/Skoltech_CAIT_Root_CA.pem
```

## MacOS

MacOS (Monterey and Ventura) has its own tooling. Importing a certificate into
system keychain can be down as follows.

```shell
sudo security add-trusted-cert -d -r trustAsRoot \
    -k /Library/Keychains/System.keychain \
    Skoltech_CAIT_Root_CA
```

## Final Notes

If everything was successful then one can access an internal resource without
correct SSL check. For example, one can access `doge`.

```shell
$ curl -I 'https://doge.skoltech.ru'
HTTP/2 302
server: nginx/1.18.0 (Ubuntu)
date: Sun, 01 Jan 2023 17:14:14 GMT
content-type: text/html; charset=utf-8
cache-control: no-cache
...
```

From now on, closed lock or green lock have to be in address line of your
browser.
