# ledger-solana-sdk

NodeJS SDK for signing Solana txs with Ledger.

## Installation

```sh
npm i '@tensor-oss/ledger-solana-sdk'
yarn add '@tensor-oss/ledger-solana-sdk'
```

## Usage

```ts
import { PublicKey, Transaction } from "@solana/web3.js";
import {
    solanaDerivationPath,
    solanaLedgerSignTx,
    Transport,
} from "@tensor-oss/ledger-solana-sdk";

// Lookup addresses corresponding to account + change index
const change = undefined; // most wallets leave this as undefined.
const transport = await Transport.default.open(undefined);
for (let account = 0; account < 10; account++) {
  const deriv = solanaDerivationPath(account, change);
  const pubkey = new PublicKey(solanaLedgerGetPubkey(transport, deriv));
  console.log(`pubkey for account ${account}: ${pubkey.toBase58()}`);
}

// Sign tx
const tx = new Transaction().add(...);
const ledgerAddr = new PublicKey("...");
const ledgerAcc = ...; // From above
const ledgerChange = ...; // From above
await solanaLedgerSignTx({
    tx,
    signer: ledgerAddr,
    account: ledgerAcc,
    change: ledgerChange
});
```
