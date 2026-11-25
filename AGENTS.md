# Keys — Project Agent Rules

This file documents Keys-specific architecture, domain boundaries, and repository rules. Global standards live in `~/Projects/Agent/AGENTS.md` and apply unconditionally on top of this file.

## What This Project Is

Keys is the Single Source of Truth (SSoT) for all personal public cryptographic keys, public certificates, trust declarations, and verification metadata for Danya (`nada.mu`). It distributes authentic OpenSSH commit signing keys, OpenPGP keys, S/MIME certificates, and RFC 9116 security contact policies to enable mathematical verification of software releases, git commits, and secure communications.

## Non-Negotiables

- **Global rules win**: Global directives from `~/Projects/Agent/AGENTS.md` apply across all environments.
- **Strictly public identity**: This repository is public and open source by default. Only public identity declarations (public keys, public certificates, security declarations) belong here.
- **Zero infrastructure or private secrets**: Private keys, server credentials, API tokens, and infrastructure host keys must never be committed. Private automation secrets reside exclusively in Ansible Vault (synchronized to VaultWarden). Infrastructure discovery records are published via `{*,@}.nada.mu/.well-known/`.
- **Single commit signing key**: Only the primary OpenSSH key (`danya-git`, fingerprint `SHA256:zUV6/z1GQKLalAt6WIBOIwgS5TdaQovUVkR+7ItwbZc`) is authorized for Git commit and release signature verification in `.allowed_signers`.
- **Mathematically anchored**: All commits and tags must be cryptographically signed with `danya-git` (Ed25519) and anchored into the Bitcoin blockchain via OpenTimestamps (`scripts/release-check.sh`).

## Repository Layout & Asset Invariants

- **`ssh/` (`.allowed_signers`)**: Contains exclusively `danya-git.pub` and canonical `.allowed_signers` (with symlink at `ssh/allowed_signers`).
- **`pgp/`**: OpenPGP ASCII-armored public key files (`danya.asc`, `public.asc`).
- **`smime/`**: X.509 S/MIME public client certificates and issuer CA chain (`danya.crt`, `fullchain.crt`).
- **`security/`**: Vulnerability disclosure policy conforming to RFC 9116 (`security.txt`).
- **`web/`**: Rendered payload of `https://nada.mu/.well-known/` (`index.html`, `privacy.html`, `terms.html`). Plain static HTML, never templated: the `Infra` role `well_known` copies these files verbatim, so a Jinja placeholder would reach production as literal text. Domain and contact details are intentionally baked in — this repository *is* the `nada.mu` identity.
- **`fingerprints.txt`**: Plaintext cryptographic attestation of SHA-256 and MD5 fingerprints for all identity assets.

## Conventions

- **Commits**: Conventional Commits (`feat`, `fix`, `docs`, `chore`, `refactor`), written in English in imperative mood, signed with SSH key `danya-git`.
- **Documentation**: All user-facing documentation must be bilingual (English in `README.md` and `docs/en/`; Russian in `README.ru.md` and `docs/ru/`).
- **Releases**: Milestone releases are tagged with annotated SemVer tags (`vMAJOR.MINOR.PATCH`) via `scripts/release.sh` with corresponding sections in `CHANGELOG.md`.
