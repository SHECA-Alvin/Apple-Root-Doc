# Linting

## Q: Do you perform pre-issuance linting?

Yes. Prior to the official issuance of certificates, SHECA issues pre-certificates and performs pre-issuance linting on them. SHECA mandates that no linter should return any errors or warnings before the official issuance.

## Q: If a pre-issuance linter detects an issue, what steps are performed?

First, SHECA will immediately stop issuing certificates and check relevant regulations (BR or RFC protocols, etc.) for confirmation. If it is confirmed that there is a problem, SHECA will run a script to scan all valid certificates and revoke all problematic certificates. At the same time, a new case will be opened in BugZilla and reported to Apple Root Program (certificate-authority-program@apple.com).

## Q: Do you regularly run linters post-issuance?

Yes. SHECA will perform a lint on all valid certificates once a week through a scheduled task.

## Q: What linters do you run? 

SHECA mainly uses **[pkimetal](https://github.com/pkimetal/pkimetal)**, which contains the following linters:

- General-purpose linters:

  - [certlint](https://github.com/certlint/certlint): Certificate linter (CABForum TLS; RFC5280).
  - [pkilint](https://github.com/digicert/pkilint): Certificate, CRL, and OCSP response linter (CABForum TLS and S/MIME; ETSI EN 319 412 and TS 119 495; RFC5280).
  - [x509lint](https://github.com/kroeckx/x509lint): Certificate linter (CABForum TLS; RFC5280).
  - [zlint](https://github.com/zmap/zlint): Certificate and CRL linter (CABForum TLS, S/MIME, and Code Signing; ETSI EN 319 412 and TS 119 495; RFC5280).

  Special-purpose linters:

  - [badkeys](https://github.com/badkeys/badkeys): Detects various public key vulnerabilities.
  - [dwklint](https://github.com/CVE-2008-0166/dwklint): Detects Debian weak keys (CVE-2008-0166), as required by CABForum Ballot [SC-73](https://github.com/cabforum/servercert/pull/500/files#diff-e0ac1bd190515a4f2ec09139d395ef6a8c7e9e5b612957c1f5a2dea80c6a6cfeR1705).
  - [ftfy](https://github.com/rspeer/python-ftfy): Detects mojibake (character encoding mix-ups).
  - [pwnedkeys](https://https//pwnedkeys.com): Detects compromised keys, where the private key was found "in the wild" and reported to the Pwnedkeys service. (NOTE: Since this linter currently involve calling an external API over the internet, it is **disabled by default**; to enable it via an environment variable, set `PKIMETAL_LINTER_PWNEDKEYS_NUMGOROUTINES=<n>` where `<n>` is an integer greater than zero).
  - [rocacheck](https://github.com/titanous/rocacheck): Detects ROCA weak keys (CVE-2017-15361), as required by CABForum Ballot [SC-73](https://github.com/cabforum/servercert/pull/500/files#diff-e0ac1bd190515a4f2ec09139d395ef6a8c7e9e5b612957c1f5a2dea80c6a6cfeR1706).

## Q:How often do you update linters and/or linter configurations?

SHECA will deploy the latest version of pkimetal to the test environment every half month, and migrate the version of the test environment to the production environment after the test environment has been running stably for two weeks.

## Q: Do you disable any lints from any linters? If so, what lints? How do you decide what lints to disable?

All items in the lints’ checklist will be checked. To ensure the compliance of certificates, SHECA hasn’t disable any lints so far. 

## Q: What is your process for reviewing or contributing new lints?

- When a new lint is determined to have broad industry applicability and aligns with the charter of the public lint library, it will be contributed. 

- When a new lint is imported, SHECA runs all lint updates through a set of previously issued certificates to confirm compatibility with existing processes. 
- When a lint is updated, SHECA reviews the code and do positive/negative test cases.

## Q: What is your process for executing lints on all of your valid certificates?

SHECA will perform a lint on all valid certificates once a week through a scheduled task.

