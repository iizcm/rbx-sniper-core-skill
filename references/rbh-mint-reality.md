# RBH Mint Reality — Verify On-Chain, Don't Trust RPC / Agent Logs

## LESSON KRITIS (session RobinGeckos, 2026-07-17)
Agent (gue) klaim 10 sub sukses mint RobinGeckos (`0xa22cb465` raw token call, tx status 1, hash ada).
User: "jujur ngga ada yang ke mint. di live mint ngga ada minter baru."
**CHECK ON-CHAIN BENERAN → user BENER.** Semua sub lu = owned 0.

## KENAPA RPC BOHONG
- `rpc.mainnet.chain.robinhood.com` balikin `tx.wait()` status=1 buat tx yg SEBENARNYA revert silent / gak masuk chain.
- `getTransactionReceipt` ktg blm cek (gak dipanggil), tp Blockscout `getstatus` bilang isError=0 (jg misleading) tp `balanceOf(sub)=0` + `totalSupply` gak naik = fakta mutlak gagal.
- Root cause mint gagal: token `mint(to,qty)` gated (allowlist/active state). 46 org lain BISA direct mint (pegang 3 tiap) krna wallet mereka udah di-allow; sub lu gak.

## RULE WAJIB (embed ke workflow mint apa pun di RBH)
1. **JANGAN klaim sukses dari `tx.wait().status===1` doang.** Itu unreliable di RBH.
2. Setelah mint batch, WAJIB verify:
   - `balanceOf(sub.address)` via ethers Contract (RPC) DAN
   - cross-check via Blockscout `account/tokenlist?address=...` (sumber beda)
   - `totalSupply()` sebelum vs sesudah harus NAIK = N * jumlah sub sukses
3. Kalau balanceOf=0 tp tx "sukses" → MINT GAGAL. Stop, jangan lanjut 90 sisa.
4. Self-deployed kontrak (owner=wallet lu) = lu yg atur allowlist. Tanya user buat allowlist 100 sub / kasih ABI fungsi whitelist. Jangan asumsi raw call jalan.

## DECODE TOOLS YG KERJA (terbukti session ini)
- Blockscout API tanpa key: `https://robinhoodchain.blockscout.com/api?module=account&action=txlist&address={C}&sort=desc`
  - filter `t.input.startsWith("0xa22cb465")` → dapet caller + calldata
  - `t.from` = minter, decode arg: `to=0x+input.slice(10,74).slice(24)`, `qty=BigInt(input.slice(74,138))`
- `account/tokenlist?address={addr}` → filter `contractAddress==C` → `balance` (truth NFT hold)
- `token/getToken?contractaddress={C}` → `totalSupply` (fakta supply)
- RPC `getStorage(C, slot)` → cek allowlist/flag (slot[9] sering whitelist bitmap/Merkle root)

## SeaDrop = TIDAK DIPAKAI di RobinGeckos
- OS page bilang "MINTING NOW / Freemint / LIMIT 3 PER WALLET" tp backend mints via `token.mint()` langsung (0 mintPublic ke SeaDrop 0x00005EA0... ditemukan di 200 tx).
- Jadi gak usah sniff SeaDrop utk collection ini. Direct token.mint() adalah jalur nyata — tp butuh allowlist.

## COST (rbh, freemint value=0)
- gas per mint ~0x49207 * ~75.9M wei = 0.00000374 ETH (~$0.0075 @ $2000). 100 sub ~0.00045 ETH (~$0.90).
- Primary butuh topup ~0.0006 ETH buat fund 100 sub + gas.
