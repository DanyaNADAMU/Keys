# Keys — Канонический источник открытых криптографических ключей

Этот репозиторий является **единым источником истины (Single Source of Truth, SSoT)** для всех персональных открытых криптографических ключей, сертификатов, деклараций безопасности и метаданных верификации **Danya** (`nada.mu`).

## Границы и инварианты
* **Исключительно открытая цифровая личность (Identity)**: здесь хранятся только публичные ключи, сертификаты и манифесты, образующие персональную идентичность (`danya-git`, PGP, S/MIME).
* **Никаких инфраструктурных секретов**: ключи серверов, хостов и серверных агентов сюда строго не допускаются. Открытые инфраструктурные ключи и протоколы автообнаружения публикуются на `{*,@}.nada.mu/.well-known/`.
* **Первоисточник приватных секретов (SSoT)**: все приватные секреты для автоматизации Ansible хранятся в Ansible Vault и синхронизируются в VaultWarden.
* **Математическая неизменяемость**: каждый коммит подписан SSH-ключом `danya-git` (Ed25519) и зафиксирован в блокчейне Bitcoin через OpenTimestamps.

## Структура репозитория
* [`ssh/`](file:///Projects/Keys/ssh) — открытые SSH-ключи для верификации коммитов и релизов Git.
  * [`danya-git.pub`](file:///Projects/Keys/ssh/danya-git.pub) — открытый ключ OpenSSH Ed25519.
  * [`allowed_signers`](file:///Projects/Keys/ssh/allowed_signers) — канонический файл OpenSSH `allowed_signers` для Git.
* [`pgp/`](file:///Projects/Keys/pgp) — открытые ключи OpenPGP / GPG (ASCII-armored).
* [`smime/`](file:///Projects/Keys/smime) — открытые сертификаты S/MIME (X.509 PEM / DER) для подписи и шифрования почты.
* [`security/`](file:///Projects/Keys/security) — политика сообщений об уязвимостях ([RFC 9116 `security.txt`](file:///Projects/Keys/security/security.txt)).
* [`docs/`](file:///Projects/Keys/docs) — документация и руководства по проверке на русском и английском языках.

## Локальная проверка подписей Git

Настройка локального репозитория Git для использования `.allowed_signers`:
```bash
git config gpg.ssh.allowedSignersFile .allowed_signers
git log --show-signature
```

## Проверка временных меток в блокчейне Bitcoin

Проверка криптографических доказательств OpenTimestamps:
```bash
git ots verify
```
