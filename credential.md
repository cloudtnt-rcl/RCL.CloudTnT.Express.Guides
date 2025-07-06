---
title: Digital Credentials
description: Digital credentials are issued to holders who demonstrate their achievements and skills. They are machine-readable and are secured by cryptographic methods.
has_children: false
nav_order: 3
---

# Digital Credentials
**V1.0**

Digital credentials are issued to holders who demonstrate their achievements and skills. They are machine-readable and are secured by cryptographic methods making them difficult to copy or forge. They are shareable and portable as they can be interchanged among computer systems thus ensuring they are recognised by different sofware applications and platforms. 

# Specifications

## W3C Verifiable Credentials (VCs)

The [W3C Specification for Verifiable Credentials](https://www.w3.org/TR/vc-overview) outlines the technical specification that the digital credentials must comply with. This will ensure that digital credentials are secure and genuine.

## Open Badges 3.0 (OBs)

The [Open Badges 3.0](https://www.imsglobal.org/spec/ob/v3p0) specification is aligned to the W3C Specification for Verifiable Credentials and provides a data model and interchangeability mechanisms for digital credentials among computer systems. This will ensure the Digital Badges, which is a type of Digital Credential, are highly secure and verified across different software applications and platforms.

# Data Model

A digital credential contains data related to the credential itself, the issuer of the credential and the holder of the credential. The data model is shown below:

## Achievement Credential

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| @context         | List of strings   | Yes      | 
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| issuer           | [Profile](./credential.md#profile)           | Yes      |
| validFrom        | string            | Yes      |
| validUntil       | string            | Yes      |
| credentialSubject| [AchievementSubject](./credential.md#achievementsubject)| Yes      |
| iss              | string            | Optional |
| jti              | string            | Optional |
| sub              | string            | Optional |

## Profile

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| name             | string            | Yes      |

## Achievement Subject

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| achievement      | [Achievement](./credential.md#achievement)       | Yes      |
| name             | string            | Optional |
| image            | string            | Optional |

## Achievement

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Yes      |
| type             | List of strings   | Yes      |
| name             | string            | Yes      |
| description      | string            | Yes      |
| criteria         | [Criteria](./credential.md#criteria)          | Yes      |

## Criteria

| Property         | Type              | Required |
| -----------------| ------------------|----------|
| id               | string            | Optional |
| narrative        | List of strings   | Optional |


# Issuance

## JWT

The JSON Web Token (JWT) is a standard that oulines the format for the digital credential to ensure verification and autentication of the digital credential. A Digital Credential is issued by an issuer. The credential is issued in the format of a [JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519). Conceptually, the JWT contains the following sections :

```bash
[header].[payload].[signature]
```

The **payload** for the JWT, will comprise the credential containing the data following the model shown above and appropriately encoded.

The JWT must be digitally signed by the issuer using the issuer's private key. The **signature** is included in the JWT.

The cryptographic algorithm used to sign the JWT is specified in the **header** and appropriately encoded. In addition, the issuers public key must be included in the header as a [JSON Web Key](https://datatracker.ietf.org/doc/html/rfc7517). The application identified in these guides do not support a key id, ``kid`` , and requires that the actual public key be included in the header.

## Format of a JWT

The digital credential is issued as a ``.jwt`` file. This file can be opened with a text editor application, such as notepad. The content of the file will look something like this:

```bash
eyJqd2siOnsia3R5IjoiUlNBIiwibiI6IjluYjBrcmRXTVIwQUhYc3Y4dnc3Mm8zb3RmQkNEX2NLZ3p1cmNRc3hGMnJiUnNheVZiV0Vlb3BGSDkzckNyZUdOelIyQUFrTERvZklmdkFNWkdsVjluVmUyMjF0UnJhODVPb1BHUmVYUFpodmlUNlhqV0NrR2NzeVNWWGRza19fdkdVTXhhdG9hTTNQNUNXMkQwMWxiUnNUQ1VtRDBudDNNZlNZUDZJM1ZxbklUOXhlUmgwaWRiUEFxZFJELUlXSDQzRzBIbEdCTHlnN0IzX055UXNmNW9kb1JFNm9DcGdPbHVUd25IekpqbVdPNUc1RlphSHZxZmV3WHl4Sm5oVmJhS1NwUWxqVFBadUl2UDBES19xb1dYeDBTWFJOLW5iblJMbWhuUDVEMDNJWXp0dUdSeEVTN3Y3T3RuZGNiUjlDS2ljWkYzSXVHaDktM3UyUXR2OVJTUSIsImUiOiJBUUFCIn0sImFsZyI6IlJTMjU2IiwidHlwIjoiSldUIn0.eyJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvbnMvY3JlZGVudGlhbHMvdjIiLCJodHRwczovL3B1cmwuaW1zZ2xvYmFsLm9yZy9zcGVjL29iL3YzcDAvY29udGV4dC0zLjAuMy5qc29uIl0sImlkIjoiYzc5ZTgyNzJjODY5NGRiNGFmMzZkZmExNDMwZTI2NDAiLCJ0eXBlIjpbIlZlcmlmaWFibGVDcmVkZW50aWFsIiwiT3BlbkJhZGdlQ3JlZGVudGlhbCJdLCJpc3N1ZXIiOnsiaWQiOiJkaWQ6andrOmV5SnJkSGtpT2lKU1UwRWlMQ0p1SWpvaU9XNWlNR3R5WkZkTlVqQkJTRmh6ZGpoMmR6Y3liek52ZEdaQ1EwUmZZMHRuZW5WeVkxRnplRVl5Y21KU2MyRjVWbUpYUldWdmNFWklPVE55UTNKbFIwNTZVakpCUVd0TVJHOW1TV1oyUVUxYVIyeFdPVzVXWlRJeU1YUlNjbUU0TlU5dlVFZFNaVmhRV21oMmFWUTJXR3BYUTJ0SFkzTjVVMVpZWkhOclgxOTJSMVZOZUdGMGIyRk5NMUExUTFjeVJEQXhiR0pTYzFSRFZXMUVNRzUwTTAxbVUxbFFOa2t6Vm5GdVNWUTVlR1ZTYURCcFpHSlFRWEZrVWtRdFNWZElORE5ITUVoc1IwSk1lV2MzUWpOZlRubFJjMlkxYjJSdlVrVTJiME53WjA5c2RWUjNia2g2U21wdFYwODFSelZHV21GSWRuRm1aWGRZZVhoS2JtaFdZbUZMVTNCUmJHcFVVRnAxU1haUU1FUkxYM0Z2VjFoNE1GTllVazR0Ym1KdVVreHRhRzVRTlVRd00wbFplblIxUjFKNFJWTTNkamRQZEc1a1kySlNPVU5MYVdOYVJqTkpkVWRvT1MwemRUSlJkSFk1VWxOUklpd2laU0k2SWtGUlFVSWlmUSIsInR5cGUiOlsiUHJvZmlsZSJdLCJuYW1lIjoiUmF5IENvbnN1bHRpbmcgTGltaXRlZCJ9LCJ2YWxpZEZyb20iOiIyMDI1LTA2LTEzVDAwOjAwOjAwWiIsInZhbGlkVW50aWwiOiIyMDUwLTA2LTEzVDAwOjAwOjAwWiIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7ImlkIjoiZGlkOmp3azpleUpyZEhraU9pSlNVMEVpTENKdUlqb2ljSFZZYjNWUlMxVmhhMnQyWDJKVVpXUTRka05ZTFU5RlRHMWpVemhxUTIxRFdFOVdaRnAyYjNsNWMwd3hUV015TVdaR1N6QnhNWEJJTjFkTVJVMWhPVUZoZDFoUVNrMXNja2RFZG1jeFQwRmlTMWgwVGtNd1oyaEhNVFIyZHpWcVFYcGllbGRzYjNGM2MyNWphR2xRUms1RU5XdDZhVE5mVW1OcFl6bHhabHBHVW5OM2FVZGpVa050UkhOS1VubHFYMjQ0TURoVlprTkdka1JuWVZaelZqbE5OVkpoTW1OWk1IbFlRa0pETTI5dFJrcEpOWEJrVEVFeVNURkZSRlp1TVdKa1R6RmFSWFF0VUZZM1ozYzBNV0ZRWkhkaE56ZDJjVEJOUmtGRGFUTnlTMHd0VEVkeldrTnhZbG8xUTBac05qSkZNV05ZTVU1S1ptZDFkM0JvTURKSE1FZFJTalpJTW5oQlNGZG5VM0JrVlV0WGNUTlFkWEpyV1ZsM1ZHa3dURkpYUjAxNU1rNXNTemR3VlV4UE1sRndlbTFHTjJ0V1JtZGhiVzVmYjBWT01GbGhWa294YlZnelZFMDJVRVZIVnpaRmRERlJJaXdpWlNJNklrRlJRVUlpZlEiLCJ0eXBlIjpbIkFjaGlldmVtZW50U3ViamVjdCJdLCJhY2hpZXZlbWVudCI6eyJpZCI6ImI3MjFhMjJkNjI1MjQzMWM4YzVkYjQyZDhmYmNiMGE4IiwidHlwZSI6WyJBY2hpZXZlbWVudCJdLCJuYW1lIjoiU2FtcGxlIFZlcmlmaWFibGUgQ3JlZGVudGlhbCIsImRlc2NyaXB0aW9uIjoiVGhpcyBpcyBhIHNhbXBsZSB2ZXJpZmllZCBjcmVkZW50aWFsIGlzc3VlZCB0byBhIGhvbGRlci4iLCJjcml0ZXJpYSI6eyJuYXJyYXRpdmUiOiJUaGUgaG9sZGVyIHdpbGwgcmVjZWl2ZSB0aGUgc2FtcGxlIGNyZWRlbnRpYWwgd2hlbiB0aGUgc3VjY2Vzc2Z1bGx5IHVzZSB0aGUgd2ViIHdhbGxldCBhcHBsaWNhdGlvbi4ifX0sIm5hbWUiOiJBbmlsIFJpcGxhIn0sImlzcyI6ImRpZDpqd2s6ZXlKcmRIa2lPaUpTVTBFaUxDSnVJam9pT1c1aU1HdHlaRmROVWpCQlNGaHpkamgyZHpjeWJ6TnZkR1pDUTBSZlkwdG5lblZ5WTFGemVFWXljbUpTYzJGNVZtSlhSV1Z2Y0VaSU9UTnlRM0psUjA1NlVqSkJRV3RNUkc5bVNXWjJRVTFhUjJ4V09XNVdaVEl5TVhSU2NtRTROVTl2VUVkU1pWaFFXbWgyYVZRMldHcFhRMnRIWTNONVUxWllaSE5yWDE5MlIxVk5lR0YwYjJGTk0xQTFRMWN5UkRBeGJHSlNjMVJEVlcxRU1HNTBNMDFtVTFsUU5ra3pWbkZ1U1ZRNWVHVlNhREJwWkdKUVFYRmtVa1F0U1ZkSU5ETkhNRWhzUjBKTWVXYzNRak5mVG5sUmMyWTFiMlJ2VWtVMmIwTndaMDlzZFZSM2JraDZTbXB0VjA4MVJ6VkdXbUZJZG5GbVpYZFllWGhLYm1oV1ltRkxVM0JSYkdwVVVGcDFTWFpRTUVSTFgzRnZWMWg0TUZOWVVrNHRibUp1VWt4dGFHNVFOVVF3TTBsWmVuUjFSMUo0UlZNM2RqZFBkRzVrWTJKU09VTkxhV05hUmpOSmRVZG9PUzB6ZFRKUmRIWTVVbE5SSWl3aVpTSTZJa0ZSUVVJaWZRIiwianRpIjoiYzc5ZTgyNzJjODY5NGRiNGFmMzZkZmExNDMwZTI2NDAiLCJzdWIiOiJkaWQ6andrOmV5SnJkSGtpT2lKU1UwRWlMQ0p1SWpvaWNIVlliM1ZSUzFWaGEydDJYMkpVWldRNGRrTllMVTlGVEcxalV6aHFRMjFEV0U5V1pGcDJiM2w1YzB3eFRXTXlNV1pHU3pCeE1YQklOMWRNUlUxaE9VRmhkMWhRU2sxc2NrZEVkbWN4VDBGaVMxaDBUa013WjJoSE1UUjJkelZxUVhwaWVsZHNiM0YzYzI1amFHbFFSazVFTld0NmFUTmZVbU5wWXpseFpscEdVbk4zYVVkalVrTnRSSE5LVW5scVgyNDRNRGhWWmtOR2RrUm5ZVlp6VmpsTk5WSmhNbU5aTUhsWVFrSkRNMjl0UmtwSk5YQmtURUV5U1RGRlJGWnVNV0prVHpGYVJYUXRVRlkzWjNjME1XRlFaSGRoTnpkMmNUQk5Sa0ZEYVROeVMwd3RURWR6V2tOeFlsbzFRMFpzTmpKRk1XTllNVTVLWm1kMWQzQm9NREpITUVkUlNqWklNbmhCU0ZkblUzQmtWVXRYY1ROUWRYSnJXVmwzVkdrd1RGSlhSMDE1TWs1c1N6ZHdWVXhQTWxGd2VtMUdOMnRXUm1kaGJXNWZiMFZPTUZsaFZrb3hiVmd6VkUwMlVFVkhWelpGZERGUklpd2laU0k2SWtGUlFVSWlmUSJ9.2NT-u81MN5nmIeMNohnJnL7pVkLm2rB2YpV3njJFCTNBP0_PQNls8S6l4QJElfBMCZZ1cJUx11OaOQenHeNVAD5EGTQ9VRCv3b5WahdQYZRiQj-E6z4C2azz0OGn_xVL6Zz_-yTvElUszYnySgUwcVDjCmLvQAvm52c5mEtbQN_-toL4FbLTVaSzGcWHHUXMj7L1WdhUcJH-NSQU0leOpkwGJ5WttiXH7dh1wc3RJoLLpSqmrD1yWOsSlLGdv7bvDcHxOyyPXozB9AoWSkTPNTX1z055HTCEgDVR8Xa_0Prp-rRivDW4r7L5ytIShYrOQLdg7Zn-nB_bh8pGvv4F_w
```

The **header**, **payload** and **signature** sections of the JWT are shown above. The sections are separated with dots (.). The applications referenced in these guidance documents only support credentials formatted as a ``JWT``, JSON Web Token Proof Format, in the compact format.

## JWT Decoded

The JWT can de decoded using online tools such as [jwt.io](https://jwt.io/). Just paste the JWT in the application's text box and view the decoded digital credential. An authentic JWT will be recognised as valid. An incorrect or tampered JWT will not be decoded and will be recognised as invalid. 

### JWT Header Decoded

The decoded header is shown below:

```json
{
  "jwk": {
    "kty": "RSA",
    "n": "9nb0krdWMR0AHXsv8vw72o3otfBCD_cKgzurcQsxF2rbRsayVbWEeopFH93rCreGNzR2AAkLDofIfvAMZGlV9nVe221tRra85OoPGReXPZhviT6XjWCkGcsySVXdsk__vGUMxatoaM3P5CW2D01lbRsTCUmD0nt3MfSYP6I3VqnIT9xeRh0idbPAqdRD-IWH43G0HlGBLyg7B3_NyQsf5odoRE6oCpgOluTwnHzJjmWO5G5FZaHvqfewXyxJnhVbaKSpQljTPZuIvP0DK_qoWXx0SXRN-nbnRLmhnP5D03IYztuGRxES7v7OtndcbR9CKicZF3IuGh9-3u2Qtv9RSQ",
    "e": "AQAB"
  },
  "alg": "RS256",
  "typ": "JWT"
}
```

The crytographic algorith used for signing the jwt is ``RS256`` and the type of token is a ``JWT``.

The issuer's public key is provided within the ``jwk`` parameter. The key is in ``JSON Web Key (JWK)`` format and is shown below :

```json
{
  "kty": "RSA",
  "n": "9nb0krdWMR0AHXsv8vw72o3otfBCD_cKgzurcQsxF2rbRsayVbWEeopFH93rCreGNzR2AAkLDofIfvAMZGlV9nVe221tRra85OoPGReXPZhviT6XjWCkGcsySVXdsk__vGUMxatoaM3P5CW2D01lbRsTCUmD0nt3MfSYP6I3VqnIT9xeRh0idbPAqdRD-IWH43G0HlGBLyg7B3_NyQsf5odoRE6oCpgOluTwnHzJjmWO5G5FZaHvqfewXyxJnhVbaKSpQljTPZuIvP0DK_qoWXx0SXRN-nbnRLmhnP5D03IYztuGRxES7v7OtndcbR9CKicZF3IuGh9-3u2Qtv9RSQ",
  "e": "AQAB"
}
```

### JWT Payload Decoded

The decoded JWT payload is shown below:

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://purl.imsglobal.org/spec/ob/v3p0/context-3.0.3.json"
  ],
  "id": "c79e8272c8694db4af36dfa1430e2640",
  "type": [
    "VerifiableCredential",
    "OpenBadgeCredential"
  ],
  "issuer": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoiOW5iMGtyZFdNUjBBSFhzdjh2dzcybzNvdGZCQ0RfY0tnenVyY1FzeEYycmJSc2F5VmJXRWVvcEZIOTNyQ3JlR056UjJBQWtMRG9mSWZ2QU1aR2xWOW5WZTIyMXRScmE4NU9vUEdSZVhQWmh2aVQ2WGpXQ2tHY3N5U1ZYZHNrX192R1VNeGF0b2FNM1A1Q1cyRDAxbGJSc1RDVW1EMG50M01mU1lQNkkzVnFuSVQ5eGVSaDBpZGJQQXFkUkQtSVdINDNHMEhsR0JMeWc3QjNfTnlRc2Y1b2RvUkU2b0NwZ09sdVR3bkh6SmptV081RzVGWmFIdnFmZXdYeXhKbmhWYmFLU3BRbGpUUFp1SXZQMERLX3FvV1h4MFNYUk4tbmJuUkxtaG5QNUQwM0lZenR1R1J4RVM3djdPdG5kY2JSOUNLaWNaRjNJdUdoOS0zdTJRdHY5UlNRIiwiZSI6IkFRQUIifQ",
    "type": [
      "Profile"
    ],
    "name": "Ray Consulting Limited"
  },
  "validFrom": "2025-06-13T00:00:00Z",
  "validUntil": "2050-06-13T00:00:00Z",
  "credentialSubject": {
    "id": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ",
    "type": [
      "AchievementSubject"
    ],
    "achievement": {
      "id": "b721a22d6252431c8c5db42d8fbcb0a8",
      "type": [
        "Achievement"
      ],
      "name": "Sample Verifiable Credential",
      "description": "This is a sample verified credential issued to a holder.",
      "criteria": {
        "narrative": "The holder will receive the sample credential when the successfully use the web wallet application."
      }
    },
    "name": "Anil Ripla"
  },
  "iss": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoiOW5iMGtyZFdNUjBBSFhzdjh2dzcybzNvdGZCQ0RfY0tnenVyY1FzeEYycmJSc2F5VmJXRWVvcEZIOTNyQ3JlR056UjJBQWtMRG9mSWZ2QU1aR2xWOW5WZTIyMXRScmE4NU9vUEdSZVhQWmh2aVQ2WGpXQ2tHY3N5U1ZYZHNrX192R1VNeGF0b2FNM1A1Q1cyRDAxbGJSc1RDVW1EMG50M01mU1lQNkkzVnFuSVQ5eGVSaDBpZGJQQXFkUkQtSVdINDNHMEhsR0JMeWc3QjNfTnlRc2Y1b2RvUkU2b0NwZ09sdVR3bkh6SmptV081RzVGWmFIdnFmZXdYeXhKbmhWYmFLU3BRbGpUUFp1SXZQMERLX3FvV1h4MFNYUk4tbmJuUkxtaG5QNUQwM0lZenR1R1J4RVM3djdPdG5kY2JSOUNLaWNaRjNJdUdoOS0zdTJRdHY5UlNRIiwiZSI6IkFRQUIifQ",
  "jti": "c79e8272c8694db4af36dfa1430e2640",
  "sub": "did:jwk:eyJrdHkiOiJSU0EiLCJuIjoicHVYb3VRS1Vha2t2X2JUZWQ4dkNYLU9FTG1jUzhqQ21DWE9WZFp2b3l5c0wxTWMyMWZGSzBxMXBIN1dMRU1hOUFhd1hQSk1sckdEdmcxT0FiS1h0TkMwZ2hHMTR2dzVqQXpieldsb3F3c25jaGlQRk5ENWt6aTNfUmNpYzlxZlpGUnN3aUdjUkNtRHNKUnlqX244MDhVZkNGdkRnYVZzVjlNNVJhMmNZMHlYQkJDM29tRkpJNXBkTEEySTFFRFZuMWJkTzFaRXQtUFY3Z3c0MWFQZHdhNzd2cTBNRkFDaTNyS0wtTEdzWkNxYlo1Q0ZsNjJFMWNYMU5KZmd1d3BoMDJHMEdRSjZIMnhBSFdnU3BkVUtXcTNQdXJrWVl3VGkwTFJXR015Mk5sSzdwVUxPMlFwem1GN2tWRmdhbW5fb0VOMFlhVkoxbVgzVE02UEVHVzZFdDFRIiwiZSI6IkFRQUIifQ"
}
```

The payload will contain the data for the credential following the specified data model described previously.

### JWT Signature

The JWT signature is shown below:

```bash
2NT-u81MN5nmIeMNohnJnL7pVkLm2rB2YpV3njJFCTNBP0_PQNls8S6l4QJElfBMCZZ1cJUx11OaOQenHeNVAD5EGTQ9VRCv3b5WahdQYZRiQj-E6z4C2azz0OGn_xVL6Zz_-yTvElUszYnySgUwcVDjCmLvQAvm52c5mEtbQN_-toL4FbLTVaSzGcWHHUXMj7L1WdhUcJH-NSQU0leOpkwGJ5WttiXH7dh1wc3RJoLLpSqmrD1yWOsSlLGdv7bvDcHxOyyPXozB9AoWSkTPNTX1z055HTCEgDVR8Xa_0Prp-rRivDW4r7L5ytIShYrOQLdg7Zn-nB_bh8pGvv4F_w
```

# Storing a Digital Credential

A holder will download his/her digital credential from the credential issuance platform as a ``.jwt`` file. The holder will then upload and store the credential in the wallet applications.

Where available, a holder may automatically send the credential to a wallet using the credentials ``API``. The hoster of the issuer application must configure the application to use the API.

A user must upload their DID in the wallet application's DID store before they can upload a credential. The holder's DID included in the credential must match their DID in the wallet store for it to be accepted by the wallet.

# Sharing a Digital Credential

In the wallet applications, a holder can share their credentials with verifiers such as employers, trainers


