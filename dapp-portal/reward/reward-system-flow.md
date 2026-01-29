---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/dapp-portal/reward/reward-system-flow
---

# Reward System Flow

## Reward system flow

Mini Dapp can list the mission-reward(KAIA/USDt, NFT, point) implemented within their Dapp on the Dapp Portal. Each reward is listed and tracked on the Dapp Portal in the following ways.

### **KAIA/USDt Reward** <a href="#kaia-usdt-reward" id="kaia-usdt-reward"></a>

<figure><img src="../../.gitbook/assets/image1.avif" alt=""><figcaption></figcaption></figure>

The Dapp Portal tracks the transactions of the EOA Wallet (for rewards) submitted by the Dapp. When a transaction of a specific amount occurs from that wallet to a specific user's wallet, the portal recognizes that the mission has been completed and the reward has been distributed. Due to this characteristic, a separate wallet must be prepared for each mission if you are running multiple missions. If the same wallet is used for rewards for multiple missions, the Dapp Portal will not be able to recognize which mission was completed.

\*Reward distribution for mission completion must be implemented by the Dapp. For information on sending KAIA or USDt, please refer to [https://docs.kaia.io/](https://docs.kaia.io/).

### **NFT Reward** <a href="#nft-reward" id="nft-reward"></a>

<figure><img src="../../.gitbook/assets/image2.avif" alt=""><figcaption></figcaption></figure>

The Dapp Portal tracks the transactions of the EOA Wallet from which the NFT submitted by the Dapp is distributed and references the contract address. The EOA Wallet must be submitted to the Dapp Portal team when minting the NFT, and the Dapp Portal team will airdrop the NFT to that wallet.

\*Due to the functionality of the Dapp Portal, tracking is only possible when a single NFT is distributed in a single event.

### **Point Reward** <a href="#point-reward" id="point-reward"></a>

The Dapp Portal does not currently track the flow of point rewards. It simply lists a URL to the page where points can be acquired. The policy and features regarding point movement and balance tracking may change in the future.
