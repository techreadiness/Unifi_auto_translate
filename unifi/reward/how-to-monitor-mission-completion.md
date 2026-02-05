---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/unifi/reward/how-to-monitor-mission-completion
---

# How to monitor mission completion

Apps can list the mission-reward(KAIA/USDt, NFT, point) implemented within their Apps on the Unifi Apps. Each reward is listed and tracked on the Unfi Apps in the following ways.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The Unifi Apps tracks the transactions of the EOA Wallet (for rewards) submitted by the Apps. When a transaction of a specific amount occurs from that wallet to a specific user's wallet, the Unifi Apps recognizes that the mission has been completed and the reward has been distributed. Due to this characteristic, a separate wallet must be prepared for each mission if you are running multiple missions. If the same wallet is used for rewards for multiple missions, the Unifi Apps will not be able to recognize which mission was completed.

\*Reward distribution for mission completion must be implemented by the Apps. For information on sending KAIA or USDt, please refer to [https://docs.kaia.io/references/json-rpc/references/](https://docs.kaia.io/references/json-rpc/references/)



### NFT Reward

The tracking structure for the NFT mission is similar to that of the KAIA/USDt mission. The Unifi Apps tracks the transactions of the EOA Wallet from which the NFT submitted by the Apps is distributed and references the contract address. The EOA Wallet must be submitted to the Unifi Apps team when minting the NFT, and the Unifi Apps team will airdrop the NFT to that wallet.

\*Due to the functionality of the Unifi Apps, tracking is only possible when a single NFT is distributed in a single event.
