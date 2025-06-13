---
title: DID
description: A Decentralized Identifier (DID) is used to uniquely identify a holder or issuer.
has_children: false
nav_order: 2
---

# Decentralized Identifier (DID)
**V1.0**

A Decentralized Identifier (DID) is used to uniquely identity the holder and issuer of a digital credential. The DID complies with the [W3C Specification for Decentralized Identifiers](https://www.w3.org/TR/did-1.1/).

# What is a DID

A DID is machine-readable and enables verifiable and decentralized identity. There are many DID methods that can be used to create the DID. These DID methods will outline the electronic format for the DID, how it is hosted and how it is resolved.  

# Cryptography

The foundation building block for a DID are Asymmetric Cryptographic Keys. A key pair is generated for the owner of a DID. A **private key** is securely held by the owner and a correspondent **public key** is distributed to the public. 

An owner of a DID will use their private key to digitally sign a digital file and send this file to a receiver's computer. The receiver's computer will then use the public key of the sender that is  publicly available  to verify the sender's signature on the digital file. When the digital signature is verified, the receiver's computer will deem the sigature valid and the digital file wll be accepted.

When a DID is created, a public and private key pair is generated for the owner. The owner will download and store the private key in a secure location. The public key will be embedded in the DID. Based on the particular DID method to be used, the public key will be made publicly available by resolving the DID. The public key can then be accessed in a DID document.

# The did:jwk Method

The applications identified in these guidance documents only support the [did:jwk](https://github.com/quartzjer/did-jwk/blob/main/spec.md) method. In this method, a public and private key pair is created for the owner of the DID. The cryptographic algorithm used to created the keys is [RSA](https://datatracker.ietf.org/doc/html/rfc8017) using a key size of 2048 bit. Only this cryptographic algorith is supported.

{: .warning }
The holder of the DID must download and save the private key in a secure location. The private key must not be shared with anyone. The holder must take the necessary precautions for the private key not be lost or stolen. A compromised private key will compromise a digital credential or a DID.

The private key will be formatted as a ``.txt`` file. If you open the text file on a computer you will see something like this:

## Sample Private Key

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpgIBAAKCAQEA9nb0krdWMR0AHXsv8vw72o3otfBCD/cKgzurcQsxF2rbRsay
VbWEeopFH93rCreGNzR2AAkLDofIfvAMZGlV9nVe221tRra85OoPGReXPZhviT6X
jWCkGcsySVXdsk//vGUMxatoaM3P5CW2D01lbRsTCUmD0nt3MfSYP6I3VqnIT9xe
Rh0idbPAqdRD+IWH43G0HlGBLyg7B3/NyQsf5odoRE6oCpgOluTwnHzJjmWO5G5F
ZaHvqfewXyxJnhVbaKSpQljTPZuIvP0DK/qoWXx0SXRN+nbnRLmhnP5D03IYztuG
RxES7v7OtndcbR9CKicZF3IuGh9+3u2Qtv9RSQIDAQABAoIBAQDGYGzvAp5fnaYQ
FK09eQR8H6jleGLUEtXlV0vhC08SODISv6+fCSF+uHh289pRn/Jp0NIBqUW7BlO8
yF5RG+/TFhmpqGRCfKeB4VsRqUlUjLOJ1lWJt/WdxU3OdUyiT33aF8O1/wdlA/OH
AUuO+Y7fyOEDoqZ17ma8UNGStnCwURe9vL+afJ8rZBGkX0Y5Tbg++qiss6ZnTpeH
MlTuoFQyMYIwZG4lXixvjRJ5DaOrLps3yM1me4p6zTOsnbFxY09FrsTQMv+Hb1sc
itGkSiUN4gzKXy74vQKWo/dqlDL5P7cLUFtcDyGpOeDDigH3pszbxaU2sWoD3Q7N
XCyoi74ZAoGBAP9TusTQYQ7lIvdzyFEedgSK8hHfeqmB6pj6u/w7sIQLTDiXlU7G
7SqY7rRa+Ry91n/nJxeR7emRAKS3PYb3rHtFIdiPnlU+FjpX/pSKmz3r4QGAP5bq
jB6SUCoXH+gFvPa3F1C/RidtIwZH7EKd7hHcZ9GmxWdrBxbefpjpXJRXAoGBAPcd
Pw0X1g+9jDCgzOAHXAnjnNJmnQ5sriSM25kYsv03YgdHNEtE3pshFMVV3h0SeNbW
WzJzWHh7o6/MOiDfSLw4mi9s86mseu/5NRE2f8x10q7RB3pUw1Tp8DApG9H4ElSP
VHB70Bg9wKx2I7kPWxjwLWZ/iqzIH1BWBwFUysNfAoGBAL51v/GGm5AX3vCFvty8
Az86Qn6QnRiK3+wDxWzPPcoR/2aLtIXSICJReGazIfaNqc85J9EOO1Gqp7c3NT9T
y6ccl7XK1Eo0CTK2ZyJ5DnqvVOXgvA6goatAa2oqW9OhTCchxtOmCvfoEmNiDVxY
ILnUFuGuLL0LentVt0vrb/L7AoGBAJsbkGf3fjWDFGuxgudbtzm91MF8Bzj2npfy
kiQWjMLD8JQA7aIRKGjW6uKycyhsX8z532RbYjy93pCJ8DKR9GWwYZdDG+50hPX7
xoN3YeBEVGnGapsueSzjag/QvdWdkGPjU20HSibtG/MkdGfEa7nLh7O+epzZQE58
sQj04BChAoGBAOfg1+NgQIkezTX2w/n87gqRW/C6QjnZw68Xgqs8T6ZwEEGiE8NJ
w7/aabORnrkSVL5B+Zy+1WGtSRH6StZb+HTN7g8jfqWDvifRccmEs3DVRzcNk2F7
47b6emNDaJg3RtCCF5vxvaMmDs0Z4sFuEtYjig6GKEMUIOUq2O15IuxW
-----END RSA PRIVATE KEY-----
```

Using the did:jwk method, the public key is embedded in the DID. The DID is formatted as a ``.txt`` file. If you open the text file on a computer you will see something similar to this:

## Sample DID using the did:jwk Method

```
did:jwk:eyJrdHkiOiJSU0EiLCJuIjoiOW5iMGtyZFdNUjBBSFhzdjh2dzcybzNvdGZCQ0RfY0tnenVyY1FzeEYycmJSc2F5VmJXRWVvcEZIOTNyQ3JlR056UjJBQWtMRG9mSWZ2QU1aR2xWOW5WZTIyMXRScmE4NU9vUEdSZVhQWmh2aVQ2WGpXQ2tHY3N5U1ZYZHNrX192R1VNeGF0b2FNM1A1Q1cyRDAxbGJSc1RDVW1EMG50M01mU1lQNkkzVnFuSVQ5eGVSaDBpZGJQQXFkUkQtSVdINDNHMEhsR0JMeWc3QjNfTnlRc2Y1b2RvUkU2b0NwZ09sdVR3bkh6SmptV081RzVGWmFIdnFmZXdYeXhKbmhWYmFLU3BRbGpUUFp1SXZQMERLX3FvV1h4MFNYUk4tbmJuUkxtaG5QNUQwM0lZenR1R1J4RVM3djdPdG5kY2JSOUNLaWNaRjNJdUdoOS0zdTJRdHY5UlNRIiwiZSI6IkFRQUIifQ
```

Computer systems that can read the DID will **resolve** the DID into a **DID Document**. You can use the [Universal Resolver]() provided by the [Decentralized Identity Foundation (DIF)](https://identity.foundation/) to resolve a DID. Just copy the DID into the ``did-url`` textbox and click the ``Resolve`` button. The DID will be resolved into a DID document in ``json`` format that looks something like this:

## Sample DID Document using the did:jwk Method

```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    {
      "@vocab": "https://www.iana.org/assignments/jose#"
    }
  ],
  "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoiOW5iMGtyZFdNUjBBSFhzdjh2dzcybzNvdGZCQ0RfY0tnenVyY1FzeEYycmJSc2F5VmJXRWVvcEZIOTNyQ3JlR056UjJBQWtMRG9mSWZ2QU1aR2xWOW5WZTIyMXRScmE4NU9vUEdSZVhQWmh2aVQ2WGpXQ2tHY3N5U1ZYZHNrX192R1VNeGF0b2FNM1A1Q1cyRDAxbGJSc1RDVW1EMG50M01mU1lQNkkzVnFuSVQ5eGVSaDBpZGJQQXFkUkQtSVdINDNHMEhsR0JMeWc3QjNfTnlRc2Y1b2RvUkU2b0NwZ09sdVR3bkh6SmptV081RzVGWmFIdnFmZXdYeXhKbmhWYmFLU3BRbGpUUFp1SXZQMERLX3FvV1h4MFNYUk4tbmJuUkxtaG5QNUQwM0lZenR1R1J4RVM3djdPdG5kY2JSOUNLaWNaRjNJdUdoOS0zdTJRdHY5UlNRIiwiZSI6IkFRQUIifQ",
  "verificationMethod": [
    {
      "id": "#0",
      "type": "JsonWebKey2020",
      "controller": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoiOW5iMGtyZFdNUjBBSFhzdjh2dzcybzNvdGZCQ0RfY0tnenVyY1FzeEYycmJSc2F5VmJXRWVvcEZIOTNyQ3JlR056UjJBQWtMRG9mSWZ2QU1aR2xWOW5WZTIyMXRScmE4NU9vUEdSZVhQWmh2aVQ2WGpXQ2tHY3N5U1ZYZHNrX192R1VNeGF0b2FNM1A1Q1cyRDAxbGJSc1RDVW1EMG50M01mU1lQNkkzVnFuSVQ5eGVSaDBpZGJQQXFkUkQtSVdINDNHMEhsR0JMeWc3QjNfTnlRc2Y1b2RvUkU2b0NwZ09sdVR3bkh6SmptV081RzVGWmFIdnFmZXdYeXhKbmhWYmFLU3BRbGpUUFp1SXZQMERLX3FvV1h4MFNYUk4tbmJuUkxtaG5QNUQwM0lZenR1R1J4RVM3djdPdG5kY2JSOUNLaWNaRjNJdUdoOS0zdTJRdHY5UlNRIiwiZSI6IkFRQUIifQ",
      "publicKeyJwk": {
        "kty": "RSA",
        "n": "9nb0krdWMR0AHXsv8vw72o3otfBCD_cKgzurcQsxF2rbRsayVbWEeopFH93rCreGNzR2AAkLDofIfvAMZGlV9nVe221tRra85OoPGReXPZhviT6XjWCkGcsySVXdsk__vGUMxatoaM3P5CW2D01lbRsTCUmD0nt3MfSYP6I3VqnIT9xeRh0idbPAqdRD-IWH43G0HlGBLyg7B3_NyQsf5odoRE6oCpgOluTwnHzJjmWO5G5FZaHvqfewXyxJnhVbaKSpQljTPZuIvP0DK_qoWXx0SXRN-nbnRLmhnP5D03IYztuGRxES7v7OtndcbR9CKicZF3IuGh9-3u2Qtv9RSQ",
        "e": "AQAB"
      }
    }
  ]
}
```

You can see the public key in the DID document inside the ``publicKeyJwk`` parameter. The public key is fomatted as a [JSON Web Key (JWK)](https://datatracker.ietf.org/doc/html/rfc7517). The JWK extracted from the DID document is shown below:

## Sample Public Key as a JSON Web Key (JWK)

```json
{
  "kty": "RSA",
  "n": "9nb0krdWMR0AHXsv8vw72o3otfBCD_cKgzurcQsxF2rbRsayVbWEeopFH93rCreGNzR2AAkLDofIfvAMZGlV9nVe221tRra85OoPGReXPZhviT6XjWCkGcsySVXdsk__vGUMxatoaM3P5CW2D01lbRsTCUmD0nt3MfSYP6I3VqnIT9xeRh0idbPAqdRD-IWH43G0HlGBLyg7B3_NyQsf5odoRE6oCpgOluTwnHzJjmWO5G5FZaHvqfewXyxJnhVbaKSpQljTPZuIvP0DK_qoWXx0SXRN-nbnRLmhnP5D03IYztuGRxES7v7OtndcbR9CKicZF3IuGh9-3u2Qtv9RSQ",
  "e": "AQAB"
}
```

# Distibuting a Public Key

When you provide your DID to a computer, the computer system would be able to resolve the DID and extract your public key from it. The computer can then use your public key to verify your digital signature when you sign a digital file with your private key.

# How DIDs are used

## Issuer

An issuer will use their private key to digitally sign a digital credential that they issue to a holder. The digital credential will contain the DID of the issuer embedded in the credential itself. A verifiyng computer system will then extract the public key from the issuer's DID and use it to verifiy the issuer's digital signature on the credential. If the signature is verified, the digital credential will be deemed valid by the computer system. 

## Holder

A holder of a credential will add their DID into a wallet application. Before they can add the DID, they must supply their private key to demonstrate that they own the DID. The wallet application will verify that the public key contained in the DID matches the correspondent private key supplied by the holder. If the keys match, the the wallet application will accept the holder's DID into the store. 

{: .warning }
A wallet application should not copy, share or store the holder's private key in any form. It should only use the private key to verify the holder's DID. The holder's private should only be controlled by and stored by the holder using the holder's choice of storage.

A credential will contain the DID of the issuer, as well as, the DID of the holder. A holder will only be able to store a credential in their wallet if the holder's DID in the credential matches the holder's DID in the wallet's DID store.  