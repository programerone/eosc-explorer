# EOS Classic Blockchain Explorer

[![Build Status](https://travis-ci.org/eosclassic/eosc-explorer.svg?branch=master)](https://travis-ci.org/eosclassic/eosc-explorer)

<b>Live Version: [explorer.eos-classic.io](https://explorer.eos-classic.io)</b>

## Local installation

### Requirement

+ [Parity-eosclassic](https://github.com/eosclassic/parity-eosclassic) 

+ [Nodejs](https://docs.npmjs.com/getting-started/installing-node "Nodejs install")

### Install

Clone the repo

`git clone https://github.com/eosclassic/eosc-explorer`

Install dependencies:

`npm install`

Install mongodb:

MacOS: `brew install mongodb`

Ubuntu: `sudo apt-get install -y mongodb-org`

## Populate the DB

This will fetch and parse the entire blockchain.

Setup your configuration file: `cp config.example.json config.json`

Edit `config.json` as you wish

Basic settings:
```json
{
    "nodeAddr":     "localhost",
    "gethPort":     8545,
    "startBlock":   0,
    "quiet":        true,
    "syncAll":      true,
    "patch":        true,
    "patchBlocks":  100,
    "settings": {
        "symbol": "EOSC",
        "name": "EOS Classic",
        "title": "EOS Classic Blockchain Explorer",
        "author": "EOSC"
    }
}

```

```nodeAddr```    Your node API RPC address.

```gethPort```    Your node API RPC port.

```startBlock```  This is the start block of the blockchain, should always be 0 if you want to sync the whole EOSC blockchain.

```endBlock```    This is usually the 'latest'/'newest' block in the blockchain, this value gets updated automatically, and will be used to patch missing blocks if the whole app goes down.

```quiet```       Suppress some messages. (admittedly still not quiet)

```syncAll```     If this is set to true at the start of the app, the sync will start syncing all blocks from lastSync, and if lastSync is 0 it will start from whatever the endBlock or latest block in the blockchain is.

```patch```       If set to true and below value is set, sync will iterated through the # of blocks specified.

```patchBlocks``` If `patch` is set to true, the amount of block specified will be check from the latest one.


### Run:
The below will start sync.js (which populates MongoDB with blocks/transactions).
`npm start`

The below will start web-gui on http://localhost:3000 by default.
`npm start`

You can leave sync.js running without app.js and it will sync and grab blocks based on config.json parameters
`node ./tools/sync.js`

Enabling stats requires running a separate process:
`node ./tools/stats.js`

Enabling rich list requires running a separate process one time:
`node ./tools/richlist.js`

You can configure intervals (how often a new data point is pulled) and range (how many blocks to go back) with the following:
`RESCAN=1000:100000 node tools/stats.js` (New data point every 1,000 blocks. Go back 100,000 blocks).

### Credits

Originally made by [ethereumproject - explorer](https://github.com/ethereumproject/explorer)

Modified by eosclassicteam for EOS Classic usage.
