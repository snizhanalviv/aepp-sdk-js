This document describes the installation and usage of the JavaScript SDK.


# Table of Contents
1. [Overview](#overview)
2. [Before you begin](#before_you_begin)
3. [Installation](#installation)
4. [Usage](#usage)



## Overview

**Important:** This SDK is at an alpha stage where things easily can break. We aim to make our alpha releases as stable as possible. Nevertheless it should not be taken as production-ready. 
 
With this SDK, you can develop apps for the æternity blockchain in JavaScript.
In particular, you can implement the following:
 
1. Communication with Chain
2. Crypto methods for working with transactions
3. Contracts
4. Naming system
5. Accounts
6. Oracles
 
For detailed information on these components, see **Major components** at <https://dev.aepps.com/>.



## Before you begin


* If you are new to the æternity ecosystem, please review the [Getting Started](https://dev.aepps.com/) section at <https://dev.aepps.com/>.
* Make sure to get access to a node before installing an SDK.
 
**Requirements:**
 
aepp-sdk is compiled to EcmaScript 5 through WebPack and Babel and is expected to work in any sufficiently new version of Node.js or modern web browser.
 
The minimum version Node.js is expected to work at is 8.11. For better performance, we recommend using node v.9 or later.



## Installation

To install JavaScript SDK, complete the following steps:
 
1. Add the latest **@aæternity/aepp-sdk** release from npmjs.com to your project:
```
pnpm i @aæternity/aepp-sdk
npm i @aæternity/aepp-sdk
yarn add @aæternity/aepp-sdk
 ```
**Note:**  You can also add a development version from the GitHub. To do this, drop the @ and add # and a branch name at the end, for example pnpm i aæternity/aepp-sdk#develop.

2. Set environment variables **WALLET_PRIV** and **WALLET_PUB**.
If you do not yet have the public and private keys, you need to generate them. See
the **Creating an Account** section for details.
 
**Creating an Account**
 
To work with æternity, you need to have an account. You can create it by installing its public and private key.
**Public key** is an ID of your account. You will provide it to other people so that they can send you money.
**Private key** must be kept secret and secure. It is used for signing your transactions.
You wallet can include several accounts.
 
You can create an account in one of two ways:
 
1. Using CLI:
 
   * **ae sdk genkey mykeys**
   * Add keys to your environment. Create two variables: **WALLET_PUB** and **WALLET_PRIV** and take the values from the **myKey_Pub** and **myKey** files correspondingly.
   * Reload the **Command Promt** to activate variables.
 
2. Using SDK:
 
   * import Crypto from '@aæternity/aepp-sdk/es/utils/crypto'
Crypto.genareteKeyPair(name)  // create priv and public key with 'name' current directory
   * Add keys to your environment. Create two variables: **WALLET_PUB** and **WALLET_PRIV** and take the values from the **myKey_Pub** and **myKey** files correspondingly.
   * Reload the **Command Promt** to activate variables.
 
After you create an account, add some tokens to your balance. This way you will be able to perform transactions with your wallet.
1. Go to <https://faucet.aepps.com/>.
2. Insert you public key, and then click **Top Up**.
3. Wait several minutes for tokens to come to your balance.
 
Now you can try sending and receiving money, and checking your balance. For details on these methods, see the following section.



## Usage

Depending on your needs, you can choose to work with one of the following AE parts called AE Factories (Flavors):
 
* Web Aepp development  <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/aepp.html>
* Wallet development <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/wallet.html>
* Command line tool development <https://dev.aepps.com/aepp-sdk-js/docs/api/ae/cli.md>
 
An example below illustrates connecting to a system and running a specific method:
 
Get the height (sequence number) of the last block in chain:
```
Ae({url: 'https://sdk-testnet.aepps.com'}).then(ae => {
  ae.height().then(height => {
	console.log('Current Block', height)
  })
``` 



