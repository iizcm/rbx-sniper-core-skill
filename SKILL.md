---
name: rbx-sniper-cored
description: "CORE Web3 mint skill utk Robinhood Chain (RBH, chainId 4663). Sniper Calldata: user cuma kasih alamat NFT contract -> bot Listening mode (RPC getBlock latest) -> tangkap calldata mintSigned orang lain yg sukses detik itu -> swapMinter (ganti alamat minter org -> sub1..99) -> replay concurrency 40 dgn gasPrice 0.067 gwei SEBELUM signature expired. 100% otomatis, gak butuh manual mint."
version: 1.0.0
author: Community
license: MIT
platforms: [linux, macos, windows]
tags: [general]
---

# Rbx Sniper Core — Skill

CORE Web3 mint skill utk Robinhood Chain (RBH, chainId 4663). Sniper Calldata: user cuma kasih alamat NFT contract -> bot Listening mode (RPC getBlock latest) -> tangkap calldata mintSigned orang lain yg sukses detik itu -> swapMinter (ganti alamat minter org -> sub1..99) -> replay concurrency 40 dgn gasPrice 0.067 gwei SEBELUM signature expired. 100% otomatis, gak butuh manual mint.

## Install

```bash
cp -r <skill-name> ~/.hermes/skills/<skill-path>/
```

Or clone this repository:

```bash
git clone https://github.com/iizcm/rbx-sniper-core-skill.git ~/.hermes/skills/<skill-path>/
```

## Usage

Invoke your AI agent with a clear instruction matching this skill's purpose. The agent will route tasks to this skill when the instruction matches its description or trigger keywords.

Refer to `README.md` in this repository for:
- Detailed step-by-step installation guide
- Bilingual documentation (English + Indonesian)
- Troubleshooting table
- Security best practices
- Customization tips

## Safety rules

- Never commit private keys, seed phrases, API tokens, or personal data to version control
- Use placeholders (`<YOUR_...>`) in all examples and code snippets
- Validate all outputs before acting on them
- Keep real credentials in your runtime's secure credential store only
