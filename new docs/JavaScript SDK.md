This document describes the installation and usage of the JavaScript SDK.


# Table of Contents
1. [Overview](#overview)
2. [Before you begin](#before_you_begin)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Examples](#examples)



## Overview

**Important:** This SDK is at an alpha stage where things easily can break. We aim to make our alpha releases as stable as possible. Nevertheless, it should not be taken as production-ready. 
 
With this SDK, you can develop apps for the æternity blockchain in JavaScript.
In particular, you can implement the following:
 
1. Communication with Chain
2. Crypto methods for working with transactions
3. Contracts
4. Naming system
5. Accounts
6. Oracles (in the nearest future)
 
For detailed information on these components, see **Major components** at <https://dev.aepps.com/>.



## Before you begin


* If you are new to the æternity ecosystem, please review the [Getting Started](https://dev.aepps.com/) section at <https://dev.aepps.com/>.
* Make sure to get access to a node before installing an SDK.
 
**Requirements:**
 
aepp-sdk is compiled to EcmaScript 5 through WebPack and Babel and is expected to work in any sufficiently new version of Node.js or modern web browser.
 
The minimum version Node.js is expected to work at is 8.11. For better performance, we recommend using node v.9.12 or later.

For advanced use, development versions and to get a deeper understanding of the SDK, it is advised to read the Hacking [Hacking](https://github.com/aeternity/aepp-sdk-js/blob/develop/docs/hacking.md) documentation.

## Installation

To install JavaScript SDK, add the latest **@aæternity/aepp-sdk** release from npmjs.com to your project:
```
pnpm i @aæternity/aepp-sdk
npm i @aæternity/aepp-sdk
yarn add @aæternity/aepp-sdk
 ```
**Note:**  You can also add a development version from the GitHub. To do this, drop the @ and add # and a branch name at the end, for example pnpm i aæternity/aepp-sdk#develop.


## Usage

Depending on your needs, you can choose to work with one of the following AE parts called AE Factories (Flavors):
 
* Web Aepp development  <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/aepp.html>
* Wallet development <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/wallet.html>
* Command line tool development <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/cli.md>
 
An example below illustrates connecting to a system and running a specific method.
Import { Wallet: Ae} from ”@aeternity/aepp-sdk/es/ae/wallet” using following ways:

1. Set environment variables WALLET_PRIV and WALLET_PUB.
If you do not yet have the public and private keys, you need to generate them. See
**Creating an Account** section below for details.
2. You can pass “keypair” as parameter to Ae init function
Ae({url: 'https://sdk-testnet.aepps.com', keypair: { priv: ‘Your priv key’, pub: ‘Your public key’ } })       
3. In case you do not set keypair or you do not have WALLET_PRIV and WALLET_PUB in your environment, you can still can interact with the Chain but you cannot sign any transaction.


**Creating an Account**
 
To work with æternity, you need to have an account. You can create it by installing its public and private key.
**Public key** is an ID of your account. You will provide it to other people so that they can send you money.
**Private key** must be kept secret and secure. It is used for signing your transactions.
Your wallet can include several accounts.
 
You can create an account in one of two ways:
 
* Using CLI- run the command  **ae sdk genkey mykeys**
  
* Using SDK - run the following:
 
   import Crypto from '@aæternity/aepp-sdk/es/utils/crypto'
Crypto.genareteKeyPair(name)  // this function generate keyPair and return Object like “{ priv: ‘Your private key’, pub: ‘You public key’ }”
 
After you create an account, add some tokens to your balance. This way you will be able to perform transactions with your wallet.
1. Go to <https://faucet.aepps.com/>.
2. Insert your public key, and then click **Top Up**.
3. Wait several minutes for tokens to come to your balance.
 
Now you can try sending and receiving money, and checking your balance. 


## Examples

AEPP with Wallet example can be found [here](https://github.com/aeternity/aepp-sdk-js/tree/feature/wallet-aepp-rpc/examples/connect-two-ae).

Transactions methods can be found [here](https://github.com/aeternity/aepp-sdk-js/tree/feature/wallet-aepp-rpc/docs/api).

Below you can find other examples:

### ES Modules

In is generally advised to use ESM (EcmaScript Modules), whenever possible. At
this point however, this requires a modern _bundler_ which understands ES2015
`import/export` syntax, such as [webpack] 4 (or newer). In addition, a compiler
which translates the subset of ES used by aepp-sdk will have to be used, such as
[Babel] - `.babelrc` in the project's root directory shows which plugins are
required, at least.  
Using this method also enables the use of [Tree shaking] (dead code
elimination).  
aepp-sdk's `package.json` specifies a separate entry point for any such tool
that understands ESM. In order to make sure the modules are loaded directly, use
the following syntax to load parts of aepp-sdk:

```js
import Aepp from '@aeternity/aepp-sdk/es/ae/aepp'

Aepp({url: 'https://sdk-testnet.aepps.com'}).then(client => {
  client.height().then(height => {
    console.log('Current Block', height)
  })
})
```

[webpack]: https://webpack.js.org/
[Babel]: https://babeljs.io/
[Tree shaking]: https://webpack.js.org/guides/tree-shaking/

### Browser bundle

The browser bundle is relevant in two separate cases: Either the SDK is to be
loaded traditionally through a `<script>` tag, or the bundler / compilation is
not sufficient to use and compile the SDK's ES Modules.

#### Browser `<script>` tag

The bundle will assign the SDK to a global `var` called `Ae`.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
  <script src="aepp-sdk.browser.js"></script>
  <script type="text/javascript">
    Ae.Aepp.default({url: 'https://sdk-testnet.aepps.com'}).then(ae => {
      ae.height().then(height => {
        console.log('Current Block', height)
      })
    })
  </script>
</body>
</html>
```

#### Bundler

The bundle is wrapped in UMD format, which is understood by webpack and
automatically used if no `/src` suffix is given.

```js
import Aepp from '@aeternity/aepp-sdk/es/ae/aepp'

Aepp({url: 'https://sdk-testnet.aepps.com'}).then(ae => {
  ae.height().then(height => {
    console.log('Current Block', height)
  })
})
```

### Node.js bundle

The Node.js bundle is primarily interesting for scripts which use non-transpiled
code, such as the ones provided in the `bin/` directory of the project.

```js
const {Cli: Ae} = require('@aeternity/aepp-sdk')

Ae({url: 'https://sdk-testnet.aepps.com'}).then(ae => {
  ae.height().then(height => {
    console.log('Current Block', height)
  })
})

// same with async
const main = async () => {
  const client = await Ae({url: 'https://sdk-testnet.aepps.com'})
  const height = await client.height()
  console.log('Current Block', height)
}

main()
```

### [Vue.js]

Adding aepp-sdk to a Vue.js project requires nothing special, but it should be
noted that `Ae.create` is asynchronous which needs to be taken into account.

```
vue init webpack my-project
cd my-project
yarn add @aeternity/aepp-sdk
```

```js
# src/components/HelloWorld.vue

<script>
import Aepp from '@aeternity/aepp-sdk/es/ae/aepp'
const ae = Aepp({url: 'https://sdk-testnet.aepps.com'})

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  async mounted () {
    const client = await ae
    const height = await client.height()
    this.msg = 'Current Block: ' + height
  }
}
</script>
```

[Vue.js]: https://vuejs.org/

### Basic structure of an æpp

**Interactions**

> "There are two approaches, purist and high-level."
*Alexander Kahl.*

The purist uses the functions generated out of the Swagger
file. After `create`ing the client and `await`ing it (or use `.then`),
it exposes a mapping of all `operationId`s as functions, converted to
camelCase (from PascalCase). So e.g. in order to get a transaction
based on its hash, you would invoke `client.api.getTx(query)`.

In this way the SDK is simply a mapping of the raw API calls into
JavaScript. It's excellent for low-level control, and as a teaching tool to
understand the node's operations. Most real-world requirements involve a series
of chain operations, so the SDK provides abstractions for these. The JavaScript
Promises framework makes this somewhat easy:

Example spend function, using the SDK, talking directly to the API (**purist**):
```js
  // Import necessary Modules
  import Tx from '@aeternity/aepp-sdk/es/tx/epoch.js'
  import Chain from '@aeternity/aepp-sdk/es/chain/epoch.js'
  import Account from '@aeternity/aepp-sdk/es/account/memory.js'

  async function spend (amount, receiver_pub_key) {

    const tx = await Tx({url: 'HOST_URL_HERE'})
    const chain = await Chain({url: 'HOST_URL_HERE'})
    const account = Account({keypair: {priv: 'PRIV_KEY_HERE', pub: 'PUB_KEY_HERE'}})
    const spendTx = await tx.spendTx({sender: 'PUB_KEY_HERE', receiver_pub_key, amount}))

    const signed = await account.signTransaction(spendTx, 'PUB_KEY_HERE')
    return chain.sendTransaction(signed, opt)

  }
```

The same code, using the SDK abstraction (**high-level**):
```js
  // Import necessary Modules by simply importing the Wallet module
  import Wallet from '@aeternity/aepp-sdk/es/ae/wallet' // import from SDK es-modules

  Wallet({
    url: 'HOST_URL_HERE',
    accounts: [MemoryAccount({keypair: {priv: 'PRIV_KEY_HERE', pub: 'PUB_KEY_HERE'}})],
    address: 'PUB_KEY_HERE',
    onTx: confirm, // guard returning boolean
    onChain: confirm, // guard returning boolean
    onAccount: confirm // guard returning boolean
  }).then(ae => ae.spend(parseInt(amount), receiver_pub_key))
```

### AENS usage examples

### Contracts usage examples