# Python SDK

# Table of Contents
1. [Overview](#overview)
2. [Before you begin](#before-you-begin)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Examples](#examples)



## Overview

This document describes the installation and usage of the Python SDK.
[This repo](https://github.com/aeternity/aepp-sdk-python) is for developing apps for the æternity blockchain in Python. Apps built for the æternity blockchain are called æpps. Visit <https://www.aepps.com/> to get more information about æpps.



## Before you begin

You should be connected to one of our test chains. Please see the [main dev site](https://dev.aepps.com/) for instructions on accessing the testnet, and for running a local æternity node.
Also this SDK requires [Python 3](https://www.python.org/download/releases/3.0/).


## Installation

Below you can find commands, which should be run for SDK installation. For out of the box use, it is recommended to use
`venv` and install dependencies into it.

```
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

**Note**: whenever you come back, don't forget to run `source venv/bin/activate`, again.

## Usage

You can launch the command line tool using:

```
./aecli
```
```
Available Commands:
  chain       Query the state of the chain
  config      Print the configuration of the client
  help        Help concerning any command
  inspect     Inspect an object of the blockchain
  name        A brief description of your command
  account     Handle wallet operations
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
You can find more information about CLI [here](https://github.com/snizhanalviv/aepp-sdk-js/blob/develop/new%20docs/CLI.md).

## Examples

As most examples are common, you can view examples from [JS SDK](https://github.com/snizhanalviv/aepp-sdk-js/blob/develop/new%20docs/JavaScript%20SDK.md).