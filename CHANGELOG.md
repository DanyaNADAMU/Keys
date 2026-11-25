# Changelog

All notable changes to the `Keys` project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- **`.well-known` Web Payload (`web/`)**: The canonical trust dashboard, privacy policy, and terms of service previously rendered from Jinja templates inside the `Infra` role `well_known` now live here as plain static HTML. Keys becomes the single source of truth for the whole `https://nada.mu/.well-known/` surface, so the served page is versioned, signed, and OpenTimestamps-anchored like every other trust artifact.
- **Release Attestation (`release.yml`)**: Signed semver tags now attest a source archive — `git archive` → `SHA256SUMS` → OpenTimestamps → GitHub Release with checksums and proofs attached. The pipeline carries no deploy job: delivery to the host stays with Ansible.
- **Protection Audit (`protection-audit.yml`, `.github/protection-expected.json`)**: Weekly drift check of `main` branch protection and the release-tag ruleset against the committed contract; the trust anchor must not be silently rewritten.

### Fixed
- **Signing Key Drift**: The dashboard advertised the secondary signing key (`danya-git-2`) that was removed from the repository in v1.1.0; the card is gone and only the primary `danya-git` key is presented.

### Changed
- **README links**: Repository layout links are now relative, so they resolve on GitHub instead of pointing at a local `file:///Projects/Keys` checkout.

## [v1.1.0] - 2026-11-15

### Changed
- **Commit Signing Keys**: Retained strictly the primary OpenSSH signing key (`danya-git`, `SHA256:zUV6/z1GQKLalAt6WIBOIwgS5TdaQovUVkR+7ItwbZc`) in `.allowed_signers` and `fingerprints.txt`. Removed secondary key `danya-git-2` and infrastructure entry `glacier-git`.

### Added
- **Project Rules (`AGENTS.md`)**: Added canonical repository agent rules and identity invariant boundary specifications.
- **MIT License (`LICENSE`)**: Added standard permissive open-source license.

## [v1.0.0] - 2026-11-09

### Added
- **Public Identity Root**: Canonical repository tracking public identity declarations, OpenPGP, S/MIME, and SSH commit signing keys for `git@nada.mu`.
- **SSH Keys**: Primary (`danya-git`), secondary (`danya-git-2`), and server identity (`glacier-git`) public keys.
- **OpenPGP & S/MIME**: Cryptographic public certificates and validation chains.
- **Fingerprint Attestation**: `fingerprints.txt` with SHA-256 hashes of all identity assets.
- **Release Automation**: Release gate verification (`scripts/release-check.sh`) and milestone release tagging tool (`scripts/release.sh`).
