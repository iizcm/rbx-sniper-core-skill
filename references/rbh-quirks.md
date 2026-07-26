# RBH Chain Quirks & Proven Findings

## On-chain marketplace: NONE
- Seaport v1.1 `0x00000000006c3852cbe3e08e8df289169ede581` -> empty
- Seaport v1.4 `0x00000000000000adc04c56bf30ac9d3c0aaf14dc` -> empty
- Seaport v1.5 `0x00000000000001ad428e4906ae43c5507fac6d9` -> RPC error / no code
- Implication: NO on-chain NFT listing possible via script. `volume_booster.js`
  can only (1) track sub balances, (2) auto-send-back to primary. Listing must
  be done manually in OpenSea web UI. Do NOT promise on-chain listing on RBH.

## RPC quirks (chainId 4663)
- `provider.getCode(addr)` and `getBalance` sometimes throw
  `could not coalesce error` or `network does not support ENS`.
- WORKAROUND: use raw `provider.send("eth_getCode", [addr.toLowerCase(), "latest"])`.
  Valid contract => code !== "0x". Empty => "0x".
- `isApprovedForAll` on NFT contract also fragile via ethers helper; prefer raw send.

## OpenSea API (RBH)
- Key `OPENSEA_API_KEY` is read-only. Collection read works sometimes, but
  listing/mint endpoints return 401 on RBH (not supported). Use only for
  reading collection / NFT / events metadata.

## Wallet backup (proven working)
- Private GitHub repo: `iizcm/hermes-tasks` (NOT public `robin-jellyfish`).
- `wallet_backup/sybil_wallets.json` = primary + 100 subs + PKs (pushed OK).
- `bot/*.js` + `*.json` = ai-mint-bot scripts (pushed OK).
- Restore: clone repo -> copy wallet_backup/ to /root/wallet/, bot/ to
  /root/ai-mint-bot/, `npm i` in bot/.

## IAMHC vs hcnsec (chat)
- IAMHC (`api.iamhc.cn`) = image gen keys (9 valid). Saldo gambar TIDAK
  mempengaruhi chat.
- hcnsec (`api.hcnsec.cn`) = chat endpoint (OpenAI-compatible, DeepSeek-V4-Flash).
  Key `sk-Hg32...` valid tapi kuota bulanan HABIS ("每月token额度已不足").
  Gak bisa jadi provider utama chat saat ini. Default tetap OpenRouter
  (tencent/hy3:free = gratis).
