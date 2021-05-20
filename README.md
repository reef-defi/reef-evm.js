# @reef-defi/evm-provider.js

`evm-provider.js` implements a web3 provider which can interact with the [Reef chain EVM](https://github.com/reef-defi/reef-chain).

## Getting Started

Install dependencies

```
yarn
```

## Documentation

Most of the api of `evm-provider.js` is compatible with `ethers.js`. If you are not familiar with ethers.js, you can start by looking at its [documentation](https://docs.ethers.io/v5/single-page/).

### Provider

The Provider provides some api for interacting with nodes and is an instance of `ethers.js` [AbstractProvider](https://docs.ethers.io/v5/single-page/#/v5/api/providers/-%23-providers).

#### Creating Instances

**new Provider( apiOptions )**

apiOptions has the same parameters as when creating an instance of apiPromise for polkadot.js 

```javascript
import { options } from "@reef-defi/api";
import { Provider } from "@reef-defi/evm-provider";
import { WsProvider } from "@polkadot/api";

const provider = new Provider(
  options({
    provider: new WsProvider("ws://localhost:9944")
  })
);
```

### Wallet

The Wallet class inherits Signer and can sign transactions and messages using a private key. When using the wallet for the first time, make sure to always claim the EVM account for the wallet you are using:

```javascript
wallet.claimDefaultAccount()
```

before performing any EVM calls otherwise it may lead to `InsufficientBalance` errors.


#### Creating Instances

**new Wallet( privateKey , provider? , keyringPair? )**

`privateKey` is the private key of evm's account.`provider` is an instance of [Provider](#Provider). `keyringPair` is a [key pair for polkadot](https://polkadot.js.org/docs/api/start/keyring). If the `keyringPair` is empty, a key pair will be generated from the 
`privateKey`.

```javascript
import { Wallet } from "@reef-defi/evm-provider";
const wallet = new Wallet("0xaa397267eaee48b2262a973fdcab384a758f39a3ad8708025cfb675bb9effc20", provider)
```


# Examples

For examples see scripts in [hardhat-reef-examples repo](https://github.com/reef-defi/hardhat-reef-examples/blob/master/scripts/flipper/deploy.js).

