# Linting

## Q: Do you perform pre-issuance linting?

Yes. Prior to the official issuance of certificates, SHECA issues pre-certificates and performs pre-issuance linting on them. SHECA mandates that no linter should return any errors or warnings before the official issuance.

## Q: If a pre-issuance linter detects an issue, what steps are performed?

- First, SHECA will cease certificate issuance immediately and verify the encountered issue. 

- Then, SHECA will run scripts to scan all valid certificates issued to ascertain if there are any certificates with compliance concerns, which will then be reported to BugZilla.

## Q: Do you regularly run linters post-issuance?

Yes. SHECA will promptly initiate linters to assess the compliance of newly issued certificates immediately following the certificate issuance. Additionally, SHECA will periodically employ linters to scan all valid certificates for ongoing compliance. 

## Q: What linters do you run? 

SHECA primarily uses Zlint, but also uses Cablint and X509lint.

## Q:How often do you update linters and/or linter configurations?

SHECA will check all updates of Zlint、Cablint、X509lint once a month, and deploy the new version after testing. It will also check for updates to the linter when there are significant rule adjustments from the CA/B Forum.

## Q: Do you disable any lints from any linters? If so, what lints? How do you decide what lints to disable?

SHECA uses Zlint, which is currently sourced from: 

- ·[Apple's Certificate Transparency policy - Apple Support](https://support.apple.com/en-us/HT205280)

- [EV Guidelines for TLS Server Certificates – CAB Forum](https://cabforum.org/extended-validation/)

- [ETSI - Digital Signature | Buy Electronic & Digital Signature](https://www.etsi.org/technologies/digital-signature)
- [GitHub - mozilla/pkipolicy: Documents for Mozilla's PKI policies - certificate root program, etc.](https://github.com/mozilla/pkipolicy)
- Various RFCs (e.g. [RFC 6818](https://www.ietf.org/rfc/rfc6818.txt), [RFC 4055](https://www.ietf.org/rfc/rfc4055.txt), [RFC 8399](https://www.ietf.org/rfc/rfc8399.txt))

All items in the lints’ checklist will be checked. To ensure the compliance of certificates, SHECA hasn’t disable any lints so far. 

## Q: What is your process for reviewing or contributing new lints?

- When a new lint is determined to have broad industry applicability and aligns with the charter of the public lint library, it will be contributed. 

- When a new lint is imported, SHECA runs all lint updates through a set of previously issued certificates to confirm compatibility with existing processes. 
- When a lint is updated, SHECA reviews the code and do positive/negative test cases.

## Q: What is your process for executing lints on all of your valid certificates?

- SHECA executes lints immediately after the issuance of the certificates. 
- SHECA surpervises the update of linters, lints are executed during the regular batch inspection of valid certificates or when the linter is updated. 
- If any issues are discovered, SHECA will investigate the causes, report the issues, and take remediations.

