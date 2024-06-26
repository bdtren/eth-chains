[![Publish](https://github.com/bdtren/eth-chains/actions/workflows/publish-release.yml/badge.svg)](https://github.com/bdtren/eth-chains/actions/workflows/publish-release.yml/badge.svg) ![npm](https://img.shields.io/npm/v/eth-chains?logoColor=blue)

# Eth Chains

Helper module for getting Ethereum chains info from [chainid.network](https://chainid.network/).

## Install

```
yarn add @bdtren/eth-chains
```

```
npm install @bdtren/eth-chains
```

### Note on versioning

`@bdtren/eth-chains` uses a weekly automated release script that updates its chain data. This release script takes breaking changes into account, so breaking changes (e.g. renamed chains) are released as a new major version, while non-breaking changes (e.g. new chains) are released as a new minor version.

## Usage

Import `chains` methods and enums:

```ts
import chains, { ChainId, ChainName } from '@bdtren/eth-chains'
```

### Easily get most popular chains:

```ts
import { chain } from '@bdtren/eth-chains'

console.log(chain.ethereum.rinkeby)

console.log(chain.polygon.mumbai)
```

### Chain names and ids via Enums:

```ts
console.log(ChainId.EthereumMainnet) // 1
console.log(ChainId.BinanceSmartChainMainnet) // 56
console.log(ChainName.EthereumMainnet) // "Ethereum Mainnet"
console.log(ChainName.Rinkeby) // "Rinkeby"
```

### Chain by ID:

```ts
chains.getById(ChainId.EthereumMainnet) // { name: "Ethereum Mainnet", ..., "infoURL": "https://ethereum.org" }
// Equivalent
chains.getById(1)
```

### Chain by Name:

```ts
chains.getByName(ChainName.EthereumMainnet) // { name: "Ethereum Mainnet", ..., "infoURL": "https://ethereum.org" }
// Equivalent
chains.getByName('Ethereum Mainnet')
```

### Get all Chains:

```ts
const allChains = chains.all()
// { 1: { name: "Ethereum Mainnet", ..., "infoURL": "https://ethereum.org" }, 2: {...}}
```

### Get all Icons:

```ts
const allChains = chains.allIcons()
// { "5ireChain": { data: [...], imgUrls: ["https://ipfs.io/ipfs/QmaZDNDFLWESH4i3XqwEWfWBb1HPnQSNbDAr74nr2x8QAk"] }, "ETND": {...}}
```

### Chain Icon by Name:

```ts
chains.getIconByName("ethereum") // { data: [...], imgUrls: ["https://ipfs.io/ipfs/QmdwQDr6vmBtXmK2TmknkEuZNoaDqTasFdZdu3DRw8b2wt"] }
```

### Typescript Types:

```ts
import { Chain, NativeCurrency, Explorer } from '@bdtren/eth-chains'
const ethereum: Chain = chains.getById(ChainId.EthereumMainnet)
ethereum.chain // 'ETH'
```

---

TODO:

- [ ] Add webhook that watches the chains repo and triggers an update to this package whenever that repo gets updated
  - [ ] Add check in the deploy script to make sure that the types are correct before publishing
- [ ] Add Tests
  - [ ] Once quicktype is added, test with different chains.json objects to make sure it can handle new types
- [ ] Use [quicktype](https://github.com/quicktype/quicktype) to autogen types from json
- [x] Autogen Chain Id enum
- [x] Autogen Chain Name enum
