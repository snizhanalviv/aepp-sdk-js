The æternity command line interface

## Summary
Each æternity's SDKs feature a command-line interface which you can use to invoke the blockchain's features. All CLIs  have the same name and syntax, which are described here. However, not all of them have a full feature set. An entry in [square brackets] indicates which SDKs support a feature, using the following codes:
- G go
- J javascript
- P python

So [GP] indicates that a feature is only available in Go and Python.


## Overview 

The command-line interface is invoked using the command `aecli`. Depending on where it's installed on your system, you may have to give a path when you invoke it. 

## General usage
If you invoke `aecli` with no arguments, it shows basic usage:
```
$ ./aecli 
The command line client for the Aeternity blockchain

Usage:
  aecli [command]

Available Commands:
  chain       Query the state of the chain
  config      Print the configuration of the client
  help        Help about any command
  inspect     Inspect an object of the blockchain
  name        A brief description of your command
  wallet      Handle wallet operations
  contract    Compile contracts
  crypto      Crypto helpers


Flags:
  -c, --config string   config file to load (defaults to $HOME/.aeternity/config.yaml
      --debug           enable debug
  -h, --help            help for aecli
      --json            print output in json format
      --version         version for aecli
  -u, --epoch-url,      show URL of epoch   

Use "aecli [command] --help" for more information about a command.
```

The general groupings of commands are:
- `chain`  commands do not require a public or private key and give information about the state of the chain. None of the chain commands change the state of the chain at all.
- `config` displays the client's configuration file and can write the configuration to disk.
- `help` does what one would expect and is described here no further.
- `inspect` allows you to look at the objects on the blockchain.
- `name` allows interaction with the naming system.
- `wallet` commands cover a set of functions which operate with a keypair, from transferring tokens to registering names to invoking smart contracts.
- `oracle` allows you to interact with the oracles.
- `contract` allows to compile the smart contracts.


## The chain group

```
$ ./aecli chain
Query the state of the chain

Usage:
  aecli chain [command]

Available Commands:
  play        Query the blocks of the chain one after the other
  top         Query the top block of the chain
  version     Get the status and version of the node running the chain
```
These commands display basic information about the blockchain and require little explanation. Play moves backwards through the blockchain displaying blocks and transactions.

## The inspect group
The inspect command allows you to see inside various æternity types. Because each æternity type starts with two letters identifying what sort of thing it is, you can throw anything you like at inspect, and it will bravely try to do the right thing.

#### inspect public key
```
$ ./aecli inspect ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
Balance___________________________________________ 9999497
ID________________________________________________ ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
Nonce_____________________________________________ 3
```
#### inspect transaction
```
$ ./aecli inspect th_2kgDHbvFjZn4nRLrxrimzyjdJzdEnMtFnD56r5K5UXHMaMbPkd
BlockHash_________________________________________ mh_2MTsaWUdadr1YRKC5FE7qMHXvtzCZixQyHFV8zsPUCQvwJr2fP
BlockHeight_______________________________________ 151
Hash______________________________________________ th_2kgDHbvFjZn4nRLrxrimzyjdJzdEnMtFnD56r5K5UXHMaMbPkd
 versionField_____________________________________ 1
  Amount__________________________________________ 20000
  Fee_____________________________________________ 1
  Nonce___________________________________________ 1
  Payload_________________________________________ test tranasaction
  RecipientID_____________________________________ ak_2uLM25PWdhrTQfuxgJiM8E5sZREzUoB5iFnukHCz1uAZYBMqwo
  SenderID________________________________________ ak_2a1j2Mk9YSmC1gioUq4PWRm3bsv887MbuRVwyv4KaUGoR1eiKi
```
#### inspect block
```
$ ./aecli inspect mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
Hash______________________________________________ mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
Height____________________________________________ 682
PrevHash__________________________________________ kh_Uo54QZNbXAP52BftwHoLVjrfEPmYVn8186D6CfqicXz25gtbE
PrevKeyHash_______________________________________ kh_Uo54QZNbXAP52BftwHoLVjrfEPmYVn8186D6CfqicXz25gtbE
Signature_________________________________________ sg_FctQnGxxCzNUf5vkAfhVVeVAQ8DbBiknQW5Wh6DpSz77ku9tgL23GpaDk6V5yij4Fw1jozNwzJJPYbzMroLkaHJU2rYE3
StateHash_________________________________________ bs_phbFtw7EhFKEP63mtMYd9wSR818VQJqyTqsbLefWJT68ecbR1
Time______________________________________________ 2018-09-20T13:34:51+02:00
TxsHash___________________________________________ bx_GnJ5zjiwAatgQjmQF9gPkFjxKiX7uwvc6z1YGrECSv6QmazeH
Version___________________________________________ 23
  BlockHash_______________________________________ mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
  BlockHeight_____________________________________ 682
  Hash____________________________________________ th_UvCG8Xo7EvsdA1D21ngLmxnJ1oDYv5qEKKNAg2pDXdYs5mJvW
   versionField___________________________________ 1
    Amount________________________________________ 10000000
    Fee___________________________________________ 1
    Nonce_________________________________________ 61
    Payload_______________________________________ hello Naz! 
    RecipientID___________________________________ ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
    SenderID______________________________________ ak_2a1j2Mk9YSmC1gioUq4PWRm3bsv887MbuRVwyv4KaUGoR1eiKi
    TTL___________________________________________ 1182
```
## Wallet commands
The wallet commands are those which create and report on key pairs, and all of the operations which payments require. To perform transactions within aeternity, you need to have at least two wallets with some coins on their accounts. Using the WALLET commands, you can create a wallet (with a password or without it), add some coins to it, send coins, and view the wallet’s address (public key).

#### create

Use this command to create a new wallet.
``` 
$ aecli wallet mywallet create
 ```
Specify a password for accessing your wallet or just press Enter if you do not want to set a password.
The wallet is created in the specified directory.
```
Wallet created
Wallet address________________ ak$8w6SZmeFBXC4wJ6CR6jBB36bTz1FWSR1qKCaHo4yueWdjKr1j
Wallet path___________________ C:\aeternity\aepp-sdk-python-develop\mywallet 
```

Wallet address is your public key.
Wallet path is the directory where the wallet is created.
Both public and private keys are located in the _mywallet_ file.

#### save

Using this command, you can pass the private key to generate a wallet with a key pair.


``` 
$ aecli wallet mywallet save
 ```

#### balance
 
This command is used to check the balance of your wallet.
``` 
$ aecli wallet mywallet balance
```  
 
#### spend

Using this command, you can send coins to another wallet.
```  
$ aecli wallet 1wallet spend ak$94TQqDjzwKQYPcCdEAfxcGb3mHq2s9Rm4dybMbDWwiVRwg8RK 10
```  
As an option, you can set _--ttl_ parameter, which limits lifespan of this transaction.

#### address

View the address (public key) of your wallet using the following command:
```  
$ aecli wallet 1wallet address
``` 
## The name group 

With the aeternity naming system (AENS), you can assign and register a name to your account or oracle. This way, instead of a complex hash, you can use a name you choose.
These names have an expiration period, after which they can be transferred to another account.
For more information, see [The Æternity Naming System (AENS)](https://dev.aepps.com/aepp-sdk-docs/AENS-Python.html) and [Aeternity Naming System](https://github.com/aeternity/protocol/blob/master/AENS.md) docs.  

#### claim

Create and register a name for your account (public key).
``` 
$ aecli wallet mywallet name 'testname.aet' claim
``` 

#### revoke
TBD

#### transfer

Transfer a name to another account or contract.
TBD

#### update

Update a name
TBD

## The contracts group 

#### deploy
TBD

#### call

TBD

