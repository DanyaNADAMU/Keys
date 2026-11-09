# Changelog

All notable changes to the `Keys` project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [v1.0.0] - 2026-11-09

### Added
- **Public Identity Root**: Canonical repository tracking public identity declarations, OpenPGP, S/MIME, and SSH commit signing keys for `git@nada.mu`.
- **SSH Keys**: Primary (`danya-git`), secondary (`danya-git-2`), and server identity (`glacier-git`) public keys.
- **OpenPGP & S/MIME**: Cryptographic public certificates and validation chains.
- **Fingerprint Attestation**: `fingerprints.txt` with SHA-256 hashes of all identity assets.
- **Release Automation**: Release gate verification (`scripts/release-check.sh`) and milestone release tagging tool (`scripts/release.sh`).
