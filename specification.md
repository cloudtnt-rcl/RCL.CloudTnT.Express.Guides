---
title: Specification
description: This specification outlines the technical requirements for Wallet and Issuer applications.
has_children: false
nav_order: 6
---

# Specification for Wallet and Issuer applications

## 1.0 Introduction

1.0.1 This specification outlines the technical requirements for Wallet and Issuer applications. 

1.0.2 Applications that interchange data must follow the requirements of this specification. Such applications may include Issuer applications that create digital credentials that are to be stored in Wallet applications.

## 1.1 Issuer Application

1.1.1 An Issuer application is used by Issuers to issue digital credentials to Holder following the requirements of the [W3C Verifiable Credentials](https://www.w3.org/TR/vc-data-model-2.0/) and [Open Badges 3](https://www.imsglobal.org/spec/ob/v3p0) requirements.

## 1.2.1 Wallet Application

1.2.1 A Wallet application is used by Holders to store and share their digital credentials with Verifiers.

## 1.3 Roles

### 1.3.1 Issuer

1.3.1.1 An Issuer issues digital credentials to Holders to recognize their achievement. Examples : training provider, organization, assessor.

### 1.3.2 Holder

1.3.2.1 A Holder earns a digital credential as a recognition of his/her achievement. Examples : student, apprentice, employee.

### 1.3.3 Verifier

1.3.3.1 A Holder will share their digital credential with a verifier who will make a determination on the validity of the credential. Example : employer. 

## 1.4 Decentralized Identifiers

1.4.1 [W3C Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-1.1/) are used to uniquely identify Issuers and Holders.

1.4.2 DIDs are created using the [did:jwk method](https://github.com/quartzjer/did-jwk/blob/main/spec.md). This is the ony method supported.

1.4.3 When creating a did:jwk, the [RSA](https://datatracker.ietf.org/doc/html/rfc8017) cryptographic algorithm should be used with a 2048 bit key size. Only RSA asymmetric keys are supported. 

1.4.4 A **DID document** will be generated from the did:jwk.

1.4.5 The public key of the DID owner should be directly obtainable from the DID document as a [Json Web Key (JWK)](https://datatracker.ietf.org/doc/html/rfc7517). The JWK must iclude the public key parameters and should not reference the key from an external source such as a website.

1.4.6 A ``kid`` will be ignored in a JWK. 

1.4.7 A DID should be in the form of a text (.txt) file. Issuers and Holders should be allowed to download and save thier DID, as well as, the associated private key.

1.4.8 Where an Issuer application creates a DID for a Holder. the Holder should be able to download the DID and the asscoiated private key to add it to their DID store in a Wallet application.

1.4.9 Where an Issuer application does not create a DID for a Holder, the Issuer must request the DID from the Holder to create the Holder's credential. The Issuer must verify that the Holder owns the DID by performing a DID verification using the Holder's private key.

### Sample did:jwk

```bash
did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ
```

### Sample public Json Web Key (jwk) used to create the did:jwk

```json
{
  "kty": "RSA",
  "n": "puXouQKUakkv_bTed8vCX-OELmcS8jCmCXOVdZvoyysL1Mc21fFK0q1pH7WLEMa9AawXPJMlrGDvg1OAbKXtNC0ghG14vw5jAzbzWloqwsnchiPFND5kzi3_Rcic9qfZFRswiGcRCmDsJRyj_n808UfCFvDgaVsV9M5Ra2cY0yXBBC3omFJI5pdLA2I1EDVn1bdO1ZEt-PV7gw41aPdwa77vq0MFACi3rKL-LGsZCqbZ5CFl62E1cX1NJfguwph02G0GQJ6H2xAHWgSpdUKWq3PurkYYwTi0LRWGMy2NlK7pULO2QpzmF7kVFgamn_oEN0YaVJ1mX3TM6PEGW6Et1Q",
  "e": "AQAB"
}
```

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

## 1.5 Private Keys

1.5.1 In an Issuer or Wallet application, the DID private key for the Holder should not be stored in a database or other storage system. The private should be controlled soley by the Holder. No external party should have access to the Holder's private key.

1.5.2 When a Holder adds a DID to an Issuer or Wallet application, they must upload the DID as a text (.txt) file, as well as, use their private key to verify that they own the DID. The Wallet application should only use the private key to verify the DID and should not store the private key in the database.

1.5.3 In the Issuer application, the DID private key for the Issuer can be stored in the application's database once the issuer has full and sole control of the Issuer application. No external party should have access to the Issuer's private key.

1.5.4 Private key should be provided as ``.txt`` files that can be downloaded.

### Sample Private Key

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

## 1.6 Credential Data Model

1.6.1 A digital credential contains data related to the credential itself, the Issuer of the credential and the Holder of the credential. The data model is shown below:

### 1.6.2 AchievementCredential

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| @context         | List of strings   | Yes      | 
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| issuer           | Profile           | Yes      |
| validFrom        | string            | Yes      |
| validUntil       | string            | Yes      |
| credentialSubject| AchievementSubject| Yes      |
| iss              | string            | Optional |
| jti              | string            | Optional |
| sub              | string            | Optional |

### 1.6.3 Profile

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| name             | string            | Yes      |

### 1.6.4 AchievementSubject

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| achievement      | Achievement       | Yes      |
| name             | string            | Optional |
| image            | string            | Optional |

### 1.6.5 Achievement

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| name             | string            | Yes      |
| description      | string            | Yes      |
| criteria         | Criteria          | Yes      |

### 1.6.6 Criteria

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Optional |
| narrative        | List of strings   | Optional |

### Example Credential

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.3.json"
  ],
  "id": "b08d340b24f64fe2b1a4b8af6e9458bc",
  "type": [
    "VerifiableCredential",
    "OpenBadgeCredential"
  ],
  "issuer": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdwam9FRDlPQk9sazhFZy1IU095QXVkc0FrcXpLcjNwRzIyWUVGY2NGZ0E2N1UzakxGbHQxcERoMmpzbzlYWkVLS1JrclYwS2ZTYmJVM1ZHS2hYOHZTVjB4WmNkZ2pHTEZfZGJJakh0WExDaFF4ZEl3MFU2dVVkODU3VGt6LXNyQVhISXkxeWNueGdMQWlucXkzTDhTZ01iSVZSdEJfZjFMYTNXVlkydVMyVjNUNGJwYkd5VVBRZmk3SkZmR2hqcG5BOTctR0IwZWgzMHoxbkJqZTZTdERGRk1abmJRUXlPWkljemVLS0JfdkNobjBOMGJOMVhtaGIzdER5Y1UxdFRMZEZaVDZLUDFRZVExMGc3OC1RIiwiZSI6IkFRQUIifQ",
    "type": [
      "Profile"
    ],
    "name": "Ray Consulting Limited"
  },
  "validFrom": "2025-05-19T00:00:00Z",
  "validUntil": "2030-05-19T00:00:00Z",
  "credentialSubject": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ",
    "type": [
      "AchievementSubject"
    ],
    "achievement": {
      "id": "015301207aa74f5fa548ac55bb884996",
      "type": [
        "Achievement"
      ],
      "name": "Sample Verifiable Credential",
      "description": "This credential is an example of a Verifiable Credential.",
      "criteria": {
        "narrative": "To achieve this credential, a user can download this Verifiable Credential and use it for demonstration purposes."
      }
    }
  },
  "iss": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdwam9FRDlPQk9sazhFZy1IU095QXVkc0FrcXpLcjNwRzIyWUVGY2NGZ0E2N1UzakxGbHQxcERoMmpzbzlYWkVLS1JrclYwS2ZTYmJVM1ZHS2hYOHZTVjB4WmNkZ2pHTEZfZGJJakh0WExDaFF4ZEl3MFU2dVVkODU3VGt6LXNyQVhISXkxeWNueGdMQWlucXkzTDhTZ01iSVZSdEJfZjFMYTNXVlkydVMyVjNUNGJwYkd5VVBRZmk3SkZmR2hqcG5BOTctR0IwZWgzMHoxbkJqZTZTdERGRk1abmJRUXlPWkljemVLS0JfdkNobjBOMGJOMVhtaGIzdER5Y1UxdFRMZEZaVDZLUDFRZVExMGc3OC1RIiwiZSI6IkFRQUIifQ",
  "jti": "b08d340b24f64fe2b1a4b8af6e9458bc",
  "sub": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ"
}
```

## 1.7 Credential Format

1.7.1 Credentials should be presented as a [Json Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519). Conceptually, the JWT contains the following sections :

```bash
[header].[payload].[signature]
```

1.7.2 The header of the JWT should include the JWK defined in the Issuer's DID. The JWK should contain the Issuer's public key parameters. The ``kid``, if included, will be ignored.

### Example JWT decoded Header

```json
{
  "alg": "RS256",
  "typ": "JWT",
  "jwk": {
    "kty": "RSA",
    "n": "xICdahlIZ5Zenx2yR8Tr_9gVJ-eqEg82gJwzaLWdhHwCfHqIcXSmBcWl8jJMYdDnjQtgpjoED9OBOlk8Eg-HSOyAudsAkqzKr3pG22YEFccFgA67U3jLFlt1pDh2jso9XZEKKRkrV0KfSbbU3VGKhX8vSV0xZcdgjGLF_dbIjHtXLChQxdIw0U6uUd857Tkz-srAXHIy1ycnxgLAinqy3L8SgMbIVRtB_f1La3WVY2uS2V3T4bpbGyUPQfi7JFfGhjpnA97-GB0eh30z1nBje6StDFFMZnbQQyOZIczeKKB_vChn0N0bN1Xmhb3tDycU1tTLdFZT6KP1QeQ10g78-Q",
    "e": "AQAB"
  }
}
```

1.7.3 The payload of the JWT should contain the Holder's credential.

### Example JWT decoded Payload

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.3.json"
  ],
  "id": "b08d340b24f64fe2b1a4b8af6e9458bc",
  "type": [
    "VerifiableCredential",
    "OpenBadgeCredential"
  ],
  "issuer": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdwam9FRDlPQk9sazhFZy1IU095QXVkc0FrcXpLcjNwRzIyWUVGY2NGZ0E2N1UzakxGbHQxcERoMmpzbzlYWkVLS1JrclYwS2ZTYmJVM1ZHS2hYOHZTVjB4WmNkZ2pHTEZfZGJJakh0WExDaFF4ZEl3MFU2dVVkODU3VGt6LXNyQVhISXkxeWNueGdMQWlucXkzTDhTZ01iSVZSdEJfZjFMYTNXVlkydVMyVjNUNGJwYkd5VVBRZmk3SkZmR2hqcG5BOTctR0IwZWgzMHoxbkJqZTZTdERGRk1abmJRUXlPWkljemVLS0JfdkNobjBOMGJOMVhtaGIzdER5Y1UxdFRMZEZaVDZLUDFRZVExMGc3OC1RIiwiZSI6IkFRQUIifQ",
    "type": [
      "Profile"
    ],
    "name": "Ray Consulting Limited"
  },
  "validFrom": "2025-05-19T00:00:00Z",
  "validUntil": "2030-05-19T00:00:00Z",
  "credentialSubject": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ",
    "type": [
      "AchievementSubject"
    ],
    "achievement": {
      "id": "015301207aa74f5fa548ac55bb884996",
      "type": [
        "Achievement"
      ],
      "name": "Sample Verifiable Credential",
      "description": "This credential is an example of a Verifiable Credential.",
      "criteria": {
        "narrative": "To achieve this credential, a user can download this Verifiable Credential and use it for demonstration purposes."
      }
    }
  },
  "iss": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdwam9FRDlPQk9sazhFZy1IU095QXVkc0FrcXpLcjNwRzIyWUVGY2NGZ0E2N1UzakxGbHQxcERoMmpzbzlYWkVLS1JrclYwS2ZTYmJVM1ZHS2hYOHZTVjB4WmNkZ2pHTEZfZGJJakh0WExDaFF4ZEl3MFU2dVVkODU3VGt6LXNyQVhISXkxeWNueGdMQWlucXkzTDhTZ01iSVZSdEJfZjFMYTNXVlkydVMyVjNUNGJwYkd5VVBRZmk3SkZmR2hqcG5BOTctR0IwZWgzMHoxbkJqZTZTdERGRk1abmJRUXlPWkljemVLS0JfdkNobjBOMGJOMVhtaGIzdER5Y1UxdFRMZEZaVDZLUDFRZVExMGc3OC1RIiwiZSI6IkFRQUIifQ",
  "jti": "b08d340b24f64fe2b1a4b8af6e9458bc",
  "sub": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ"
}
```

1.7.4 The signature of the JWT should be created by signing the JWT with the Issuer's private key.

1.7.5 In accordance with the JWT specification, the JWT should be derived from:

```bash
Y = Base64URLEncode(header) + '.' + Base64URLEncode(payload)

JWT token = Y + '.' + Base64URLEncode(RSASHA256(Y))
```

1.7.6 The JWT should be in the **compact** form. 

1.7.7 Only ``.jwt`` files for credentials are supported by the Issuer and Wallet applications. An image file with an embedded JWT is not supported.

### Example Crededential formatted as a JWT compact

```bash
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImp3ayI6eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdwam9FRDlPQk9sazhFZy1IU095QXVkc0FrcXpLcjNwRzIyWUVGY2NGZ0E2N1UzakxGbHQxcERoMmpzbzlYWkVLS1JrclYwS2ZTYmJVM1ZHS2hYOHZTVjB4WmNkZ2pHTEZfZGJJakh0WExDaFF4ZEl3MFU2dVVkODU3VGt6LXNyQVhISXkxeWNueGdMQWlucXkzTDhTZ01iSVZSdEJfZjFMYTNXVlkydVMyVjNUNGJwYkd5VVBRZmk3SkZmR2hqcG5BOTctR0IwZWgzMHoxbkJqZTZTdERGRk1abmJRUXlPWkljemVLS0JfdkNobjBOMGJOMVhtaGIzdER5Y1UxdFRMZEZaVDZLUDFRZVExMGc3OC1RIiwiZSI6IkFRQUIifX0.eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvbnMvY3JlZGVudGlhbHMvdjIiLCJodHRwczovL3B1cmwuaW1zZ2xvYmFsLm9yZy9zcGVjL29iL3YzcDAvY29udGV4dC0zLjAuMy5qc29uIl0sImlkIjoiYjA4ZDM0MGIyNGY2NGZlMmIxYTRiOGFmNmU5NDU4YmMiLCJ0eXBlIjpbIlZlcmlmaWFibGVDcmVkZW50aWFsIiwiT3BlbkJhZGdlQ3JlZGVudGlhbCJdLCJpc3N1ZXIiOnsiaWQiOiJkaWQ6andrOmV5SnJkSGtpT2lKU1UwRWlMQ0p1SWpvaWVFbERaR0ZvYkVsYU5WcGxibmd5ZVZJNFZISmZPV2RXU2kxbGNVVm5PREpuU25kNllVeFhaR2hJZDBObVNIRkpZMWhUYlVKalYydzRha3BOV1dSRWJtcFJkR2R3YW05RlJEbFBRazlzYXpoRlp5MUlVMDk1UVhWa2MwRnJjWHBMY2pOd1J6SXlXVVZHWTJOR1owRTJOMVV6YWt4R2JIUXhjRVJvTW1wemJ6bFlXa1ZMUzFKcmNsWXdTMlpUWW1KVk0xWkhTMmhZT0haVFZqQjRXbU5rWjJwSFRFWmZaR0pKYWtoMFdFeERhRkY0WkVsM01GVTJkVlZrT0RVM1ZHdDZMWE55UVZoSVNYa3hlV051ZUdkTVFXbHVjWGt6VERoVFowMWlTVlpTZEVKZlpqRk1ZVE5YVmxreWRWTXlWak5VTkdKd1lrZDVWVkJSWm1rM1NrWm1SMmhxY0c1Qk9UY3RSMEl3Wldnek1Ib3hia0pxWlRaVGRFUkdSazFhYm1KUlVYbFBXa2xqZW1WTFMwSmZka05vYmpCT01HSk9NVmh0YUdJemRFUjVZMVV4ZEZSTVpFWmFWRFpMVURGUlpWRXhNR2MzT0MxUklpd2laU0k2SWtGUlFVSWlmUSIsInR5cGUiOlsiUHJvZmlsZSJdLCJuYW1lIjoiUmF5IENvbnN1bHRpbmcgTGltaXRlZCJ9LCJ2YWxpZEZyb20iOiIyMDI1LTA1LTE5VDAwOjAwOjAwWiIsInZhbGlkVW50aWwiOiIyMDMwLTA1LTE5VDAwOjAwOjAwWiIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7ImlkIjoiZGlkOmp3azpleUpyZEhraU9pSlNVMEVpTENKdUlqb2ljSFZZYjNWUlMxVmhhMnQyWDJKVVpXUTRka05ZTFU5RlRHMWpVemhxUTIxRFdFOVdaRnAyYjNsNWMwd3hUV015TVdaR1N6QnhNWEJJTjFkTVJVMWhPVUZoZDFoUVNrMXNja2RFZG1jeFQwRmlTMWgwVGtNd1oyaEhNVFIyZHpWcVFYcGllbGRzYjNGM2MyNWphR2xRUms1RU5XdDZhVE5mVW1OcFl6bHhabHBHVW5OM2FVZGpVa050UkhOS1VubHFYMjQ0TURoVlprTkdka1JuWVZaelZqbE5OVkpoTW1OWk1IbFlRa0pETTI5dFJrcEpOWEJrVEVFeVNURkZSRlp1TVdKa1R6RmFSWFF0VUZZM1ozYzBNV0ZRWkhkaE56ZDJjVEJOUmtGRGFUTnlTMHd0VEVkeldrTnhZbG8xUTBac05qSkZNV05ZTVU1S1ptZDFkM0JvTURKSE1FZFJTalpJTW5oQlNGZG5VM0JrVlV0WGNUTlFkWEpyV1ZsM1ZHa3dURkpYUjAxNU1rNXNTemR3VlV4UE1sRndlbTFHTjJ0V1JtZGhiVzVmYjBWT01GbGhWa294YlZnelZFMDJVRVZIVnpaRmRERlJJaXdpWlNJNklrRlJRVUlpZlEiLCJ0eXBlIjpbIkFjaGlldmVtZW50U3ViamVjdCJdLCJhY2hpZXZlbWVudCI6eyJpZCI6IjAxNTMwMTIwN2FhNzRmNWZhNTQ4YWM1NWJiODg0OTk2IiwidHlwZSI6WyJBY2hpZXZlbWVudCJdLCJuYW1lIjoiU2FtcGxlIFZlcmlmaWFibGUgQ3JlZGVudGlhbCIsImRlc2NyaXB0aW9uIjoiVGhpcyBjcmVkZW50aWFsIGlzIGFuIGV4YW1wbGUgb2YgYSBWZXJpZmlhYmxlIENyZWRlbnRpYWwuIiwiY3JpdGVyaWEiOnsibmFycmF0aXZlIjoiVG8gYWNoaWV2ZSB0aGlzIGNyZWRlbnRpYWwsIGEgdXNlciBjYW4gZG93bmxvYWQgdGhpcyBWZXJpZmlhYmxlIENyZWRlbnRpYWwgYW5kIHVzZSBpdCBmb3IgZGVtb25zdHJhdGlvbiBwdXJwb3Nlcy4ifX19LCJpc3MiOiJkaWQ6andrOmV5SnJkSGtpT2lKU1UwRWlMQ0p1SWpvaWVFbERaR0ZvYkVsYU5WcGxibmd5ZVZJNFZISmZPV2RXU2kxbGNVVm5PREpuU25kNllVeFhaR2hJZDBObVNIRkpZMWhUYlVKalYydzRha3BOV1dSRWJtcFJkR2R3YW05RlJEbFBRazlzYXpoRlp5MUlVMDk1UVhWa2MwRnJjWHBMY2pOd1J6SXlXVVZHWTJOR1owRTJOMVV6YWt4R2JIUXhjRVJvTW1wemJ6bFlXa1ZMUzFKcmNsWXdTMlpUWW1KVk0xWkhTMmhZT0haVFZqQjRXbU5rWjJwSFRFWmZaR0pKYWtoMFdFeERhRkY0WkVsM01GVTJkVlZrT0RVM1ZHdDZMWE55UVZoSVNYa3hlV051ZUdkTVFXbHVjWGt6VERoVFowMWlTVlpTZEVKZlpqRk1ZVE5YVmxreWRWTXlWak5VTkdKd1lrZDVWVkJSWm1rM1NrWm1SMmhxY0c1Qk9UY3RSMEl3Wldnek1Ib3hia0pxWlRaVGRFUkdSazFhYm1KUlVYbFBXa2xqZW1WTFMwSmZka05vYmpCT01HSk9NVmh0YUdJemRFUjVZMVV4ZEZSTVpFWmFWRFpMVURGUlpWRXhNR2MzT0MxUklpd2laU0k2SWtGUlFVSWlmUSIsImp0aSI6ImIwOGQzNDBiMjRmNjRmZTJiMWE0YjhhZjZlOTQ1OGJjIiwic3ViIjoiZGlkOmp3azpleUpyZEhraU9pSlNVMEVpTENKdUlqb2ljSFZZYjNWUlMxVmhhMnQyWDJKVVpXUTRka05ZTFU5RlRHMWpVemhxUTIxRFdFOVdaRnAyYjNsNWMwd3hUV015TVdaR1N6QnhNWEJJTjFkTVJVMWhPVUZoZDFoUVNrMXNja2RFZG1jeFQwRmlTMWgwVGtNd1oyaEhNVFIyZHpWcVFYcGllbGRzYjNGM2MyNWphR2xRUms1RU5XdDZhVE5mVW1OcFl6bHhabHBHVW5OM2FVZGpVa050UkhOS1VubHFYMjQ0TURoVlprTkdka1JuWVZaelZqbE5OVkpoTW1OWk1IbFlRa0pETTI5dFJrcEpOWEJrVEVFeVNURkZSRlp1TVdKa1R6RmFSWFF0VUZZM1ozYzBNV0ZRWkhkaE56ZDJjVEJOUmtGRGFUTnlTMHd0VEVkeldrTnhZbG8xUTBac05qSkZNV05ZTVU1S1ptZDFkM0JvTURKSE1FZFJTalpJTW5oQlNGZG5VM0JrVlV0WGNUTlFkWEpyV1ZsM1ZHa3dURkpYUjAxNU1rNXNTemR3VlV4UE1sRndlbTFHTjJ0V1JtZGhiVzVmYjBWT01GbGhWa294YlZnelZFMDJVRVZIVnpaRmRERlJJaXdpWlNJNklrRlJRVUlpZlEifQ.S4VDYLi4SviluK8IBdeE4SLTUFCk1OMQLRmp6zI5RK8ZTM3TbgXUWeOTUX6C5NtO7EaNx0wXmbqEGUkoiU9kY_dutKF1Kv2DG4MTqwNcU_skivo2Dt9g1atBRlF5Al4aEpIqThRKf0U2LWe80dvKwODki2TI1_kxsochleNLPETzrbqB9bMbiQ6JcKOsvkV8puIuGzuDdlhmmyH7wG1ySFy4bsPq8DoiBW_hRMJSxuW1go71v4Di2HxoqZuV9nJUO-vNvApiGYw3eSTzwTvV-TH7mdBlvxEXa3-42FreJQiQ7bsK48WqQ1jllGVoJYYE1FKEV-0rpEWYlIl3Shx7lg
```

1.7.8 The file extension for the credential in JWT compact format should be ``.jwt``.

1.7.9 Holders should be able to download their credential as a ``.jwt`` file from an Issuer application.

1.7.10 The credential ``.jwt`` file can then be uploaded to a Wallet application. Alternatively, the credential file can be programtically saved to the Wallet application using the Wallet application's ``Credentials API``.

## 1.8 Wallet Credentials API

1.8.1 A Holder using an Issuer application can programtically save a credential file to a Wallet application using the Wallet application's ``Credentials API``.

1.8.2 A Wallet application must provide the ``Credential API`` URL to an Issuer application for credential data interchange.

## 1.9 Authorization Server

1.9.1 The Issuer application must use an authorization server to obtain an [OIDC Connect](https://openid.net/specs/openid-connect-core-1_0.html) ``id token`` to authorize with Wallet application's``Credentials API``. 

1.9.2 In an Issuer application, the Holder will first login to their account with the authorization server and obtain an ``id token``. The Holder must use the same login account that they use to login to the Wallet application. 

1.9.3 Authorization should follow the [OAuth 2](https://datatracker.ietf.org/doc/html/rfc6749) ``Authorization Code`` flow method.

## 1.10 POST Request from Issuer Application

1.19.1 The Issuer application will make a ``POST`` request to the ``Credentials API`` URL in the Wallet application to save a Holder's credentetial in a wallet application:

```bash
https://<wallet-api-endpoint>/api/v1/credentials
```

1.19.2 The hoster of the Wallet application must provide the ``Credentials API`` URL to the Issuer 

1.19.3 The ``POST`` request must inlcude the ``id token`` obtained from the authorization server in the Authorization header of the request as a bearer token.

1.19.4 The Issuer application should place the credential in JWT compact format should in the body of the ``POST`` request with the content type of ``text/plain``.

### Example POST Request from an Issuer Platform

```bash
POST /api/v1/credentials HTTP/1.1
Host: localhost:7028
Content-Type: text/plain
Authorization: eyJsjejdbbf.....
Content-Length: 4653

eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImp3ayI6eyJrdHkiOiJSU0EiLCJuIjoieElDZGFobElaNVplbngyeVI4VHJfOWdWSi1lcUVnODJnSnd6YUxXZGhId0NmSHFJY1hTbUJjV2w4akpNWWREbmpRdGdw
```

## 1.11 Response from Wallet Application

1.11.1 If the credential does not exist in the Wallet application, a new credential will be saved in the Wallet and a ``201`` response will be returned with the credential in jwt compact format in the body of the request with content type ``text plain``. The reposne will be sent to the Issuer application that made the ``POST`` request.

1.11.2 If the credential does exist, it will be updated and a ``200`` response will be returned in the response with the credential in the body. The reposne will be sent to the Issuer application that made the ``POST`` request.
