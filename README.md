# Keys — Canonical Cryptographic Identity & Public Trust Anchors

This repository serves as the **Single Source of Truth (SSoT)** for all personal public cryptographic keys, trust declarations, and verification metadata for **Danya** (`nada.mu`).

## Invariant Boundaries
* **Strictly Public Identity**: Tracks exclusively public keys, public certificates, and declarations that constitute personal identity (e.g. `danya-git`, PGP, S/MIME).
* **Zero Infrastructure / Server Keys**: Server administration keys, host credentials, and agent signing keys are strictly excluded. Public infrastructure keys and discovery records are published via `{*,@}.nada.mu/.well-known/`.
* **Private Secrets SSoT**: All private credentials required for Ansible automation reside in Ansible Vault as the single source of truth (synchronized to VaultWarden).
* **Mathematically Anchored**: All commits and tags are signed with `danya-git` (Ed25519) and anchored into the Bitcoin blockchain via OpenTimestamps.

## Repository Layout
* [`ssh/`](file:///Projects/Keys/ssh) — OpenSSH public keys used for Git commit and release verification.
  * [`danya-git.pub`](file:///Projects/Keys/ssh/danya-git.pub) — Raw OpenSSH Ed25519 public key.
  * [`allowed_signers`](file:///Projects/Keys/ssh/allowed_signers) — Canonical OpenSSH `allowed_signers` file for Git.
* [`pgp/`](file:///Projects/Keys/pgp) — OpenPGP / GPG public keys (ASCII-armored).
* [`smime/`](file:///Projects/Keys/smime) — S/MIME public certificates (X.509 PEM / DER) for email encryption and signatures.
* [`security/`](file:///Projects/Keys/security) — Vulnerability reporting policy and declarations ([RFC 9116 `security.txt`](file:///Projects/Keys/security/security.txt)).
* [`docs/`](file:///Projects/Keys/docs) — Living documentation and verification guides in English and Russian.

## How to Verify Git Commits Locally

Configure Git to use this repository's `.allowed_signers`:
```bash
git config gpg.ssh.allowedSignersFile .allowed_signers
git log --show-signature
```

## How to Verify Bitcoin Blockchain Timestamps

Verify timestamp proofs via OpenTimestamps:
```bash
git ots verify
```
