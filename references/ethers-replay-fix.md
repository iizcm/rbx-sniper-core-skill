# ethers v6.17 CALDATA REPLAY FIX (RBH)

## Symptom
`sub.sendTransaction({to, data, gasPrice, gasLimit})` fails:
```
invalid BytesLike value (argument="value", value="0x161ac21f0000...")
```
ethers v6.17 on RBH RPC misreads `data` as `value` during populate/sign.
Happens even when `data` is valid hex (271 chars incl 0x). NOT a data error.

## Root cause
ethers populateTransaction / signTransaction path on this RPC mishandles the
field order when `data` is a long hex string. Confirmed: `ethers.isHexString(cd)`
returns true, but sendTransaction still throws on `value`.

## PROVEN FIX (raw-sign path)
Bypass sendTransaction entirely. Build explicit tx, sign raw, broadcast:

```js
const { ethers } = require("ethers");
const sub = new ethers.Wallet(w.pk, prov);
const nonce = await prov.getTransactionCount(sub.address);
const rawTx = {
  type: 0,                              // legacy tx
  to: "0x00005EA00Ac477B1030CE78506496e8C2dE24bf5", // SeaDrop
  value: 0,                            // MUST be number 0, not 0n
  gasPrice: 94384000,                  // from captured tx
  gasLimit: 163001,                    // from captured tx
  data: ethers.getBytes(cd),          // hex string -> Uint8Array
  nonce: nonce,
  chainId: 4663,
};
const signed = await sub.signTransaction(rawTx);
const tx = await prov.sendTransaction(signed);
console.log("OK", tx.hash);
```

## Critical details
- `value: 0` (number), NOT `0n`. Mixing types triggers the BytesLike error.
- `data` as `ethers.getBytes(cd)` (Uint8Array) is safer than raw string.
- Always `getTransactionCount` fresh per sub (concurrent runs need nonce mgmt).
- gasPrice/gasLimit: copy from the user's successful manual mint tx.

## Capture calldata
```js
const tx = await prov.getTransaction("0xUSER_MINT_TX");
// tx.data = 0x161ac21f + args; arg3 (offset 24 hex after 0x) = minter addr
// replace minter substring with sub.address.toLowerCase()
```
Template minter pos: `ea29bd21dd507bba7b83c7c2b2df64030c92a361` (sub0).
Replace with each sub's address (no 0x prefix, lowercase).

## Gas math
need = gasPrice * gasLimit = 94384000 * 163001 ≈ 0.00001539 ETH/sub.
100 subs ≈ 0.00154 ETH. Check primary balance BEFORE run.
