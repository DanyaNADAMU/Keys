# Keys Documentation (English)

This directory contains guides and reference materials for verifying cryptographic identities published in this repository.

## Verification Guides

- **Git Commit Signatures**: Verify commits and tags using OpenSSH `allowed_signers` (`.allowed_signers` or `ssh/allowed_signers`).
- **OpenPGP**: Import and verify ASCII-armored PGP keys from `pgp/danya.asc`.
- **S/MIME**: Validate X.509 certificates and trust chains for email encryption and signatures from `smime/danya.crt`.
- **OpenTimestamps**: Verify Bitcoin blockchain proof timestamps for commits and tags using `git ots verify`.
- **Security Policy**: Vulnerability disclosure contacts and RFC 9116 policies in `security/security.txt`.
