# CA Lifecycle Management

## Q: How many Roots are in active operation?

| Common Name                  | Expiration Date | Signature algorithm | Key length |
| :--------------------------- | :-------------- | :------------------ | ---------- |
| UCA Extended Validation Root | 2038-12-31      | RSA                 | 4096       |
| UCA Global G2 Root           | 2040-12-31      | RSA                 | 4096       |

## Q: How many Roots are planned for?

Current Root Inclusion Plan

| Common Name                  | Expiration Date | Signature algorithm | Key length |
| :--------------------------- | :-------------- | :------------------ | ---------- |
| UCA Extended Validation Root | 2038-12-31      | RSA                 | 4096       |
| UCA Global G2 Root           | 2040-12-31      | RSA                 | 4096       |

 

To align with Apple's root inclusion requirements, which mandate that Certification Authorities (CAs) only apply for single-purpose root certificates, and in response to subscriber demand for Elliptic Curve Cryptography (ECC) algorithm certificates, SHECA outlines its plans to introduce the following single-purpose roots in the future:

- Two root for EV TLS (ECC & RSA);
- Two root for TLS (ECC & RSA);
- Three roots for S/MIME (RSA & ECC & EdDSA);
- Two roots for Client Authentication (ECC & RSA);
- Two roots for Time Stamping (ECC & RSA);

## Q: How far in advance of a Root expiring is its replacement signed?

8 years before expiration.

## Q: How are cross-signatures handled between generations?

In light of certain compatibility challenges, SHECA deems it necessary to utilize earlier root certificates for the purpose of cross-signing SHECA certificates. SHECA hereby undertakes full compliance with the regulations established by the relevant community governing cross-signing practices. Upon the satisfaction of basic compatibility prerequisites by the new certificates, SHECA solemnly commits to the cessation of cross-signing activities. It is hereby acknowledged that, as a general practice, the utilization of cross-certificates shall be subject to a constraint, limited to a maximum duration of five years.

## Q: What trust purposes is each Root created to server?

UCA Global G2 Root

A multi-purpose RSA certificate, currently serving TLS Server Authentication, Client Authentication, Code Signing, Document Signing and Email Protection.



UCA Extended Validation Root

A multi-purpose RSA certificate, currently serving TLS Server Authentication, Client Authentication, Code Signing, Document Signing and Email Protection.

 

Our future plan is to generate dedicated Roots for TLS , Code Signing, Document Signing, Time Stamping Certificates, and S/MIME.

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

In adherence to Apple's root inclusion requirements stipulating that Certification Authorities (CAs) should exclusively apply for single-purpose root certificates, SHECA outlines its plan to submit single-purpose root certificates to the Apple Root Program by the year 2024. Subsequently, SHECA commits to conducting new root submissions at five-year intervals moving forward.

 

SHECA will maintain vigilant oversight of the Baseline Requirements and the root store policy. This proactive monitoring aims to comprehend the lifecycle expectations and facilitate preparations for new root inclusions during the transition period of the root's lifecycle. Upon the issuance of a new root, SHECA will promptly initiate the root inclusion application process with the Root Store operators.

## Q: When can deprecated Roots be removed from the Apple Root Program?

Deprecated Roots will be removed from the Apple Root Program when SHECA's new root satisfies the basic compatibility requirements, and when all end-entity certificates under that root hierarchy are no longer valid.