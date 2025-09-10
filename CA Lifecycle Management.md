# CA Lifecycle Management

## Q: How many Roots are in active operation?

**Active Root Certificates**

| Common Name                  | Expiration Date | Signature Algorithm | Key Length |
| ---------------------------- | --------------- | ------------------- | ---------- |
| UCA Extended Validation Root | 2038-12-31      | RSA                 | 4096       |
| UCA Global G2 Root           | 2040-12-31      | RSA                 | 4096       |

**Timeline for Converting Legacy Roots to Single-Purpose Roots**

After December 15, 2025, SHECA will fully transition the above two root certificates into single-purpose roots. By December 1, 2025, all non-TLS subordinate CAs under these roots will be revoked according to the following schedule:

| Subordinate CA                                             | Revoked Date |
| ---------------------------------------------------------- | ------------ |
| UCA Extended Validation Root → SHECA EV Code Signing CA G3 | 2025-12-01   |
| UCA Global G2 Root → SHECA Code Signing CA G4              | 2025-12-01   |
| UCA Global G2 Root → SHECA MV SMIME RSA CA G1              | 2025-12-01   |
| UCA Global G2 Root → SHECA IV SMIME RSA CA G1              | 2025-12-01   |
| UCA Global G2 Root → SHECA OV SMIME RSA CA G1              | 2025-12-01   |

**Timeline for Decommissioning Legacy Roots**

Currently, SHECA only uses UCA Extended Validation Root and UCA Global G2 Root. Since the timeline for new roots being integrated into browsers is unpredictable, the cessation of certificate issuance will align with the removal schedules of major browsers.

| CN                           | Hash                                                         | Stop Issuing Certificates |
| ---------------------------- | ------------------------------------------------------------ | ------------------------- |
| UCA Extended Validation Root | D43AF9B35473755C9684FC06D7D8CB70EE5C28E773FB294EB41EE71722924D24 | 2030-12-31                |
| UCA Global G2 Root           | 9BEA11C976FE014764C1BE56A6F914B5A560317ABD9988393382E5161AA0493C | 2030-12-31                |

------

## Q: How many Roots are planned for?

To meet Apple’s requirement for single-purpose root certificates and to accommodate the demand for ECC certificates, SHECA plans to gradually introduce the following root certificates:

- **Two TLS root certificates (RSA, ECDSA)**

| Common Name                        | Expiration Date     | Signature Algorithm | Key Length |
| ---------------------------------- | ------------------- | ------------------- | ---------- |
| UniTrust Global TLS RSA Root CA R1 | 2039-03-27 23:59:59 | RSA                 | 4096       |
| UniTrust Global TLS ECC Root CA R2 | 2039-03-27 23:59:59 | ECDSA               | secp384r1  |

- **Two S/MIME root certificates (RSA, ECDSA)**

| Common Name                          | Expiration Date     | Signature Algorithm | Key Length |
| ------------------------------------ | ------------------- | ------------------- | ---------- |
| UniTrust Global SMIME RSA Root CA R1 | 2039-03-27 23:59:59 | RSA                 | 4096       |
| UniTrust Global SMIME ECC Root CA R2 | 2039-03-27 23:59:59 | ECDSA               | secp384r1  |

- **One Time Stamping root certificate (RSA)**

| Common Name                                  | Expiration Date     | Signature Algorithm | Key Length |
| -------------------------------------------- | ------------------- | ------------------- | ---------- |
| UniTrust Global Time Stamping RSA Root CA R1 | 2049-03-27 23:59:59 | RSA                 | 4096       |


## Q: How far in advance of a Root expiring is its replacement signed?

According to CAB Forum recommendations, CAs should update root certificates every five years. SHECA will sign replacement root certificates **10 years** before the expiration of existing roots to ensure a smooth transition.

## Q: How are cross-signatures handled between generations?

Due to compatibility challenges, SHECA considers it necessary to cross-sign certain certificates using legacy roots. SHECA commits to fully complying with community best practices for cross-signatures. Once new certificates meet compatibility requirements, cross-signing will cease. As a general principle, cross-certificates will be limited to a maximum validity period of five years.

## Q: What trust purposes is each Root created to server?

**Legacy Root Certificates**

| Common Name                        | Expiration Date     | Root Purpose (Before 2025-12-01)             | Root Purpose (After 2025-12-01) |
| ---------------------------------- | ------------------- | -------------------------------------------- | ------------------------------- |
| UniTrust Global TLS RSA Root CA R1 | 2039-03-27 23:59:59 | Server Authentication, S/MIME, Time Stamping | Server Authentication           |
| UniTrust Global TLS ECC Root CA R2 | 2039-03-27 23:59:59 | Server Authentication, S/MIME, Time Stamping | Server Authentication           |

**New Root Certificates**

| Common Name                                  | Expiration Date     | Root Purpose          |
| -------------------------------------------- | ------------------- | --------------------- |
| UniTrust Global TLS RSA Root CA R1           | 2039-03-27 23:59:59 | Server Authentication |
| UniTrust Global TLS ECC Root CA R2           | 2039-03-27 23:59:59 | Server Authentication |
| UniTrust Global SMIME RSA Root CA R1         | 2039-03-27 23:59:59 | S/MIME                |
| UniTrust Global SMIME ECC Root CA R2         | 2039-03-27 23:59:59 | S/MIME                |
| UniTrust Global Time Stamping RSA Root CA R1 | 2049-03-27 23:59:59 | Time Stamping         |

------


## Q: How comprehensive is the PKI with regards to algorithmic and key size usage?

For RSA key pairs, SHECA shall ensure that the modulus size, when encoded, is at least 2048 bits, and ensure that the modulus size, in bits, is evenly divisible by 8.

For ECDSA key pairs, SHECA shall ensure that the key represents a valid point on the NIST P‐256, NIST P‐384 or NIST P‐521elliptic curve. 

The size of SM2 key is 256 bits. 

Since June 1,2021, the size of RSA key of codesigning certificate or timestamp certificate should be 3072 bits or more.

The SHECA key pair length is RSA 2048 bits, RSA 4096 bits, ECDSA NIST P‐256, ECDSA NIST P‐384 and SM2 256bits.

## Q: How quickly are customers transitioned from one Root to another?

SHECA presently possesses two root certificates for certificate issuance. In the event that a customer necessitates a transition to an alternative root certificate, SHECA offers an efficient and comprehensive issuance system. Within this system, SHECA can reissue certificates to another root within a period of 3 days subsequent to the revalidation of the customer. However, for those customers who have not yet embraced automated deployment, manual deployment post-certificate reissuance is imperative, consuming an estimated duration of 1-10 days. It is noteworthy that SHECA is equipped with automated certificate management capabilities (ACME) and actively advocates for certificate automation. In the future, SHECA's clientele will experience accelerated root certificate switching.

 

Upon the generation of a new root certificate, an official root inclusion request is initiated with browser vendors. This procedural step generally spans a duration of 1-3 years before the new root attains effective inclusion in mainstream browsers and operating systems. Subsequently, SHECA systematically transitions all subscriber certificates to the new root, ensuring compatibility with earlier versions of systems and browsers through cross-certification. Following the fulfillment of compatibility requirements by the new root and the absence of valid subscriber certificates under the old root, the gradual removal of the old root is undertaken. This phased process is anticipated to encompass a span of approximately 3-5 years. In summation, SHECA's comprehensive migration of all subscriber certificates from an old root to a new one necessitates a time frame of 5-8 years.

## Q: When are new Roots submitted to the Apple Root Program for inclusion?

SHECA has submitted a single-purpose root certificate to the Apple Root Certificate Program via CCADB on September 12, 2025, and will continue to submit new root certificates every five years thereafter.

SHECA will closely monitor baseline requirements and root store policies to ensure that the new root certificate enters the inclusion application process immediately after issuance.

## Q: When can deprecated Roots be removed from the Apple Root Program?

Once new roots meet compatibility requirements and all end-entity certificates under deprecated roots have expired, SHECA will initiate the removal process to ensure legacy roots are completely withdrawn from the Apple Root Program.
