# xbacked-sdk
Official SDK for the xBacked Protocol
This allows third party software & bots to communicate seamlessly with the xBacked protocol.

# Installation
```
yarn install @xbacked-dao/xbacked-sdk
```
# Usage
```js
import { Account, Vault, convertFromMicroUnits } from '@xbacked-dao/xbacked-sdk';

const acc = new Account({
  network: 'LocalHost | TestNet | MainNet',
  mnemonic: process.env.SEED_PHRASE
});

const vault = new Vault({ id: 123456 });

await acc.createVault({
  collateral: convertFromMicroUnits(100),
  mintAmount: convertFromMicroUnits(50),
  vault,
});

// global vault state
const vaultState = await acc.getVaultState({ vault });
// data for a specific vault
const myVault = await vault.getUserInfo({ account, address: acc.getAddress() });
const friendsVault = await vault.getUserInfo({ account, address: friendsAddress });

if (
  // might want to calculate this off chain for latest CR
  (friendsVault.collateralRatio < vaultData.liquidationCollateralRatio) ||
  // partial liquidations are available
  friendsVault.liquidating
) {
  await account.liquidateVault({
    address: friendsAddress,
    debtAmount: convertFromMicroUnits(500),
    vault
  }
}

```
