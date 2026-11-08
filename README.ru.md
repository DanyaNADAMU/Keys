# Keys — Канонический источник открытых криптографических ключей

Этот репозиторий является **единым источником истины (Single Source of Truth, SSoT)** для всех персональных открытых криптографических ключей, сертификатов, деклараций безопасности и метаданных верификации **Danya** (`nada.mu`).

## Границы и инварианты
* **Исключительно открытые данные**: здесь хранятся только публичные ключи, сертификаты и манифесты.
* **Никаких серверных ключей**: ключи администрирования хостов и серверов сюда строго не допускаются.
* **Математическая неизменяемость**: каждый коммит подписан SSH-ключом `danya-git` (Ed25519) и зафиксирован в блокчейне Bitcoin через OpenTimestamps.

## Структура репозитория
* [`ssh/`](file:///Projects/Keys/ssh) — открытые SSH-ключи для верификации коммитов и релизов Git.
  * [`danya-git.pub`](file:///Projects/Keys/ssh/danya-git.pub) — открытый ключ OpenSSH Ed25519 в текстовом формате.
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
