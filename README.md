[![codecov](https://codecov.io/gh/cryptococks-xyz/cryptococks-contract/branch/main/graph/badge.svg?token=RRX86L2MKF)](https://codecov.io/gh/cryptococks-xyz/cryptococks-contract)

<a href="https://cryptococks.xyz/">
 <p align="center">
   <img src="https://github.com/cocodigrande2021/cc-contract/raw/main/logo.png" width="320" alt="CryptoCocks" />
 </p>
</a>

# CryptoCocks

[CryptoCocks (cryptococks.xyz)](https://cryptococks.xyz/) is a decentralized generative art project where the rarity of the unique digital collectibles ([ERC721 NFTs](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/#top)) not only is determined by pseudo-randomly assigned
traits of varying frequency but also how someone's wallet balance at the time of minting compares
with the wallet balance of previous minters at the time they minted their token. CryptoCocks tokens are fair-priced meaning that the cost for minting will always be 1% of that minter's wallet balance and is primarily decisive for the rarity of the minted NFT.
The total supply of CryptoCocks is limited to 10000 unique tokens and each image is stored decentralized on [IPFS](https://ipfs.io) and [Filecoin](https://filecoin.io) forever.

When minting a CryptoCocks token, we store on-chain your balance
(or more specifically, the fee of 1% of your wallet balance) in an
[Order Statistics Tree](https://en.wikipedia.org/wiki/Order_statistic_tree) in order to be able to efficiently find the rank of this balance, i.e. its index in a sorted list of balances of all minters.
We calculate the [Percentile Rank (PR)](https://en.wikipedia.org/wiki/Percentile_rank), i.e., the percentage of
balances in its frequency distribution that are less than the minter's current wallet balance.
We bin the continuous PRs (e.g. 33% or 99%) uniformly into 10 intervals such that
all bins have nearly identical widths. We map these 10 intervals (decentiles) to the 10 cock lengths, so that PRs in [0,10) are mapped to cock length 1, PRs in [20,30) are mapped to cock length 2, ..., PRs in [90,100) are mapped to cock length 10. Only the largest balance at the point in time of the mint will receive a special length, namely 11, which persists this information on the blockchain (i.e., see token URI and linked metadata fields).

In other words, this means that someone's cock will be as short as possible (length 1 of 10) if that minter's balance at the time of minting is no greater or equal to 10% of all the balances of the previous minters. 90% of previous minters have made a larger investment to obtain a CryptoCock.

This repository contains the solidity contracts powering CryptoCocks.

# Gallery
<p float="left">
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/1/11/cock.svg" width="200" alt="CryptoCock 11" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/2/12/cock.svg" width="200" alt="CryptoCock 12" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/3/13/cock.svg" width="200" alt="CryptoCock 13" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/4/14/cock.svg" width="200" alt="CryptoCock 14" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/5/15/cock.svg" width="200" alt="CryptoCock 15" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/6/16/cock.svg" width="200" alt="CryptoCock 16" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/7/17/cock.svg" width="200" alt="CryptoCock 17" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/8/18/cock.svg" width="200" alt="CryptoCock 18" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/9/19/cock.svg" width="200" alt="CryptoCock 19" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/10/20/cock.svg" width="200" alt="CryptoCock 20" />
  <img src="https://storage.googleapis.com/crypto-cocks/svgs/11/1/cock.svg" width="200" alt="CryptoCock 1" />
    <img src="https://storage.googleapis.com/crypto-cocks/svgs/11/5/cock.svg" width="200" alt="CryptoCock 5" />
</p>

# IPFS
Since the allocation of the length of the cocks when minting is completely dynamic we have to provide 10000 unique images for each of the 10 (+1 for `All Time High` cocks) available lengths.
To facilitate the IPFS upload of the total `10000 * 11 * 2 = 220000` files we have decided to upload the metadata and images in batches.

## Metadata
| Min Token ID   | Max Token ID  | IPFS CID | Gateway  |
|---|---|---|---|
| 1  | 2000  | bafybeiesbbihtfdj3kqbah5642p7drsb6hrzwzksezbgb2t2ojjwgh2k5m  | [link](https://bafybeiesbbihtfdj3kqbah5642p7drsb6hrzwzksezbgb2t2ojjwgh2k5m.ipfs.dweb.link)  |
| 2001  | 4000  | bafybeifclnruolpdcsouhmzhnardvpzroxk6qouc53drw4vh2f3zdoouya  | [link](https://bafybeifclnruolpdcsouhmzhnardvpzroxk6qouc53drw4vh2f3zdoouya.ipfs.dweb.link)   |
| 4001  | 6000  | bafybeihbeszvaoc3exx6ji77g74nyuqmoz2scdykudna3qd6xzgygn36ra  | [link](https://bafybeihbeszvaoc3exx6ji77g74nyuqmoz2scdykudna3qd6xzgygn36ra.ipfs.dweb.link)  |
| 6001  | 8000  | bafybeidl3uswhq65hnfvgj6bfahbvdb57y7cxiaelgct6q7raweubcms6u   | [link](https://bafybeidl3uswhq65hnfvgj6bfahbvdb57y7cxiaelgct6q7raweubcms6u.ipfs.dweb.link)  |
| 8001  | 10000  | bafybeifx2hrh6mhbpcivo4z53l76uqwc6fth4nf4qah6aow7e62lcka3d4   | [link](https://bafybeifx2hrh6mhbpcivo4z53l76uqwc6fth4nf4qah6aow7e62lcka3d4.ipfs.dweb.link)  |

## Images
| Length | IPFS CID | Gateway |
|---|---|---|
|1|bafybeidgznl4kxsrvcnob2mjxaugxsewvomt2ugumuek6jkmwg2qnplbhy|[link](https://bafybeidgznl4kxsrvcnob2mjxaugxsewvomt2ugumuek6jkmwg2qnplbhy.ipfs.dweb.link)|
|2|bafybeiddwhda4ucs3oqlvrqabc2oiluumv7zrsyuq3er3zzlcgcuwltod4|[link](https://bafybeiddwhda4ucs3oqlvrqabc2oiluumv7zrsyuq3er3zzlcgcuwltod4.ipfs.dweb.link)|
|3|bafybeiazprkpomsikvdxyrur75freaqopon4pxhzq2bvt6w6hzx7yga6qa|[link](https://bafybeiazprkpomsikvdxyrur75freaqopon4pxhzq2bvt6w6hzx7yga6qa.ipfs.dweb.link)|
|4|bafybeicymvym3nlkmepptxznn6mlc5pjt6xn4gzxzukja5wyri3t4zawwi|[link](https://bafybeicymvym3nlkmepptxznn6mlc5pjt6xn4gzxzukja5wyri3t4zawwi.ipfs.dweb.link)|
|5|bafybeifb3upudkwuw7gq5yqnbtss2r22hjnz5ngwybsxywg6w64fnzkphm|[link](https://bafybeifb3upudkwuw7gq5yqnbtss2r22hjnz5ngwybsxywg6w64fnzkphm.ipfs.dweb.link)|
|6|bafybeiarocxbhl2vx52thdhebsjdn7dbmaxjk6e2e6ivw5opsi4ihsmtma|[link](https://bafybeiarocxbhl2vx52thdhebsjdn7dbmaxjk6e2e6ivw5opsi4ihsmtma.ipfs.dweb.link)|
|7|bafybeidj7eio5gspvapwux2oxupju35aprrvcrudsvscsnmbshrtzhrose|[link](https://bafybeidj7eio5gspvapwux2oxupju35aprrvcrudsvscsnmbshrtzhrose.ipfs.dweb.link)|
|8|bafybeigli4kkcnts7q3kcgegdf6lvnboml5g4eepwpwcozkzgq2ihfj4mm|[link](https://bafybeigli4kkcnts7q3kcgegdf6lvnboml5g4eepwpwcozkzgq2ihfj4mm.ipfs.dweb.link)|
|9|bafybeifiyx2etlte2ebhj2glgixtwu5d4xjqt3qrbmmdfjqqxd6zgliglm|[link](https://bafybeifiyx2etlte2ebhj2glgixtwu5d4xjqt3qrbmmdfjqqxd6zgliglm.ipfs.dweb.link)|
|10|bafybeidodcrxbwdzpopchv5xdn7nj5adrus6xgelusd6r6cfc2spb6t3g4|[link](https://bafybeidodcrxbwdzpopchv5xdn7nj5adrus6xgelusd6r6cfc2spb6t3g4.ipfs.dweb.link)|
|10<sup>*</sup>|bafybeidzb6zbvffokobhko4rstlau4x6jwi6r42ifu2stuhogfr74kecnu|[link](https://bafybeidzb6zbvffokobhko4rstlau4x6jwi6r42ifu2stuhogfr74kecnu.ipfs.dweb.link)|

<sup>*</sup>Length 10 with `All Time High` characteristic.

# Commands
## Deploy
```shell
npx hardhat run scripts/deploy.ts
TS_NODE_FILES=true npx ts-node scripts/deploy.ts
```

## Tests
```shell
npm run test # run unit tests
npm run test:no-logs # run unit tests and hide contract console.log messages
npm run coverage # run unit tests with coverage report
npm run test:gas # run unit tests with gas usage report
```

## Static Analysis
> "Slither is a Solidity static analysis framework written in Python 3. It runs a suite of vulnerability detectors, prints visual information about contract details, and provides an API to easily write custom analyses. Slither enables developers to find vulnerabilities, enhance their code comprehension, and quickly prototype custom analyses." – [crytic/lither](https://github.com/crytic/slither)
```shell
pip3 install slither-analyzer # requires python 3.6+
slither . --filter-paths "hardhat|openzeppelin" # static contract analysis
```

## Linting
```shell
npm run check # contract checking (includes linting)
npm run lint # linting of typescript files
```

## Other
```shell
npx hardhat compile # compile contracts
npx hardhat clean
npx hardhat node
npx hardhat help
npx solhint 'contracts/**/*.sol'
npx solhint 'contracts/**/*.sol' --fix
```

# Etherscan verification

To try out Etherscan verification, you first need to deploy a contract to an Ethereum network that's supported by Etherscan, such as Ropsten.

In this project, copy the `.env.example` file to a file named `.env`, and then edit it to fill in the details. Enter your Etherscan API key, your Rinkeby node URL, e.g., from Alchemy, and the private key of the account which will send the deployment transaction. With a valid `.env` file in place, first deploy your contract:

```shell
npm run deploy:rinkeby
```

Then, copy the deployment address(es) and paste it in to replace `DEPLOYED_CONTRACT_ADDRESS` in this command:

```shell
npx hardhat verify --network ropsten DEPLOYED_CONTRACT_ADDRESS
```

# Performance optimizations

For faster runs of your tests and scripts, consider skipping ts-node's type checking by setting the environment variable `TS_NODE_TRANSPILE_ONLY` to `1` in hardhat's environment. For more details see [the documentation](https://hardhat.org/guides/typescript.html#performance-optimizations).
