---
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/juuhQ1BuKwYKE7NR6geM/dapp-portal/collection-and-drops/how-to-mint-nft
---

# How to mint NFT

## Drops Flow

<figure><img src="../../.gitbook/assets/스크린샷 2025-01-14 오전 9.21.45.png" alt=""><figcaption></figcaption></figure>

### Airdrop Stage

<mark style="color:red;">**Airdrop which is a one of the stage from Drops should be deployed from Dapp Portal side with signer address.**</mark> Mini Dapps who want to airdrop NFT must request to register Drops via Ops Support channel.

**Please NOTE** that the <mark style="color:red;">**execution times of the airdrop stage and other stages within Drops MUST NOT overlap**</mark> because the airdrop execution is implemented as one of the stages within Drops. **Please ensure the minting process is completed as below guied before Drops begins.**

#### Minting Process

<figure><img src="../../.gitbook/assets/스크린샷 2025-01-10 오전 12.47.44.png" alt=""><figcaption></figcaption></figure>

#### How to mint

* Signer of airdrop stage can transfer transction with directly hosting 'mintSigned' for the contract.
* You can mint NFT if the transaction is confirmed.

**function mintSigned()**

You can create signature following below function.

```
mintSigned(address,address,uint32,((address,uint96,(address,uint96)[]),uint48,uint40,uint40,uint16,uint32),bytes32,bytes)
#method sig : 'c45f2655'
```

```
function mintSigned(
  address nftContract,
  address minterIfNotPayer,
  uint32 quantity,
  MintParams calldata mintParams,
  bytes32 salt,
  bytes calldata signature
)
```

#### Parameter for function mintSigned

* nftContract - contract adress for NFT collection
* minterIfNotPyer - wallet address to be received NFT for mint. It can be same with signer address or another address
* quantity - NFT amount to mint
* MintParams - It is related in information of airdrop stage, refer to below. - - This parameter can be delivered from Ops team after setting airdrop stage.&#x20;

```
struct MintParams {
    Price mintPrice;
    uint48 maxTotalMintableByWallet;
    uint40 startTime;
    uint40 endTime;
    uint16 dropStageIndex;
    uint32 maxTokenSupplyForStage;
}
  
struct Price {
    address token;
    uint96 amount;
    Fee[] fees;
}
  
struct Fee {
    address recipient;
    uint96 amount;
}
```

* Details (**It will be delivered from Ops support channel if you submit information for Airdrop stage**)
  * maxTotalMintableByWallet
  * startTime
  * endTime
  * dropStageIndex
  * maxTokenSuppyForStage
  * Price
    * token
    * amount
    * fees
* salt - You need to it create signature for next step. It must be recreated with each function call because it's a value for just one-time.
* signature - EIP signature with the parameters above.

#### How to create signature

```
EIP712Domain(
  string name,
  string version,
  uint256 chainId,
  address verifyingContract
)
SignedMint(
  address nftContract,
  address minter,
  MintParams mintParams,
 bytes32 salt
)
Fee(
  address recipient,
  uint96 amount
)
MintParams(
  Price mintPrice,
  uint48 maxTotalMintableByWallet,
  uint40 startTime,
  uint40 endTime,
  uint16 dropStageIndex,
  uint32 maxTokenSupplyForStage
)
Price(
  address token,
  uint96 amount,
  Fee[] fees
)
```

* primaryType - 'SignedMint'.
* minter - wallet address to be received NFT for mint. It can be same with signer address or another address
* Set parameter for EIP712Domain
  * name- "Next Drop"
  * version - "1"
  * chainId - Production : 8217 | Testnet : 1001
  * verifyingContract - contract address deployed as 'drop router' already

#### contract

* 'mintSigned' function is for 'drop router's contract.

#### Value

* Set quantity \* price(in kei) for value when you create transaction

#### Sample Transactions

* [Transaction (on Kairos) >](https://kairos.kaiascan.io/tx/0xd8a6073e9a672420d738e3e2403bc7bc9b587bb896ac9cfd2eb56659ea1282af)
  * collection - 0xf8f22bb6a6dbb2219f762162c1dbd4e917816ef1
  * drop router contract - 0x7a766037653d055821fecd501c5c40a02cfffe57
  * signer - 0xc92aca8530b5e3c9d1819ebe94367b7444026fc1
  * minter - 0x340a32ef7263836adf87dc8941621a78443973f5

#### Appendix

**How to host Meta/ImageUri?**

You can choose one of the ways below.

* Submit 'csv' flie for airdrop information with Meta data if you have imageURI server to upload NFT images.

```
tokenID,name,description,file_name,attributes|Color,attributes|Level,attributes|Birthday
1,title1,description1,https://{imageUrl_path}/{sub_path}/1.png,Green,5 level,2024.12.5
2,title2,description2,https://{imageUrl_path}/{sub_path}/2.png,Red,3 level,2024.12.6
3,title3,description3,https://{imageUrl_path}/{sub_path}/4.png,Brown,5 level,2024.12.7
4,title4,description4,https://{imageUrl_path}/{sub_path}/3.png,Red,4 level,2024.12.8
5,title5,description5,https://{imageUrl_path}/{sub_path}/5.png,Red,5 level,2024.12.9
6,title6,description6,https://{imageUrl_path}/{sub_path}/6.png,Green,5 level,2024.12.10
7,title7,description7,https://{imageUrl_path}/{sub_path}/7.png,Blue,1 level,2024.12.11
8,title8,description8,https://{imageUrl_path}/{sub_path}/8.png,Brown,5 level,2024.12.12
9,title9,description9,https://{imageUrl_path}/{sub_path}/9.png,Green,5 level,2024.12.13
10,title10,description10,https://{imageUrl_path}/{sub_path}/10.png,Green,5 level,2024.12.14
```

* Submit image files with Meta data without **file\_name** column to Ops Support channel. Dapp Partal can upload the images you've submitted to internal server and host them when mint NFT.

### Non-Airdrop Stage

Please follow Collection & Drios guide >

## NFT Specification





