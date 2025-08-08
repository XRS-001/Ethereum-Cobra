# Ethereum-Cobra

Ethereum-Cobra 

## Installation

All dependencies are provided in the Ethereum file so there is no need to install anything except Python itself if you do not already have it as it is needed to run the code from source. Helios itself is also precompiled into the Ethereum folder.

```bash
https://www.python.org/downloads/
```

## Usage
Remember that this is an experimental project and although there are security measures in place to prevent human error there's always the possiblity that you'll encounter bugs that could potentially risk funds. Use the interface with caution.

To run the interface itself from the source code you'll need to open a command line tool and change directory into the Ethereum-Cobra directory, you can then run the interface code to get started with python3 interface.py.
```bash
C:\Users\user_name>cd desktop/ethereum-cobra

C:\Users\user_name\Desktop\Ethereum-Cobra>python3 interface.py
Ethereum Interface
------------------
Enter an Ethereum RPC URL (Helios will use it to trustlessly bootstrap a light client):
```
You'll be asked to provide an RPC URL on the first startup. Helios will use this URL to bootstrap a light client connection to the Ethereum network trustlessly, I recommend getting an Alchemy or Infura RPC URL to use with Helios. 

Once you've setup Helios you'll be presented with the main interface.
```bash
1: My Accounts
2: Add Account
3: Sign Transaction
4: Check Address Balance
5: Token Interface
6: Ethereum Name Service
7: Blockchain Explorer
8: Check Transaction Status
9: Deploy Contract
```
**My Accounts** uses Helios to check the Ether and ERC-20 token balances of the accounts saved in the accounts.json file in the Ethereum folder.

**Add Account** adds a new account to the accounts.json file using secrets to generate a random private key. There's no account importing so if you have existing Ethereum accounts I'd reccomend creating a new one with this function and sending a small amount of Ether to test some of the interface's functions.

**Sign Transaction** is a simple function for sending Ether from one address to another, gas prices are generated automatically and a confirmation appears with an estimated fee denominated in Ether before signing and broadcast. This confirmation with estimated fee functionality is implemented across the entire interface for every value transfer. Every value transfer also has checks to make sure the recipient is a valid checksummed address.

**Check Address Balance** is pretty simple, it just checks the Ether balance of a checksummed address.

**Token Interface** loads up the tokeninterface.py menu, which I'll get into later.

**Ethereum Name Service** loads up the nameservice.py menu, which I'll get into later.

**Block Explorer** provides you with an updating stream of the latest block and some data about it, you can use it to look at some metrics like gas prices. You need to press CTRL-C to exit from the explorer.

**Check Transaction Status** checks whether a transation is included in the mempool or included in a block, or neither.

**Deploy Contract** is a function for deploying bytecode to the network and returning the contract address after deployment. Estimated deployment fees are also displayed before deployment.

If you were to have selected 5 here you would be brought to the token interface menu which has functions for interacting with ERC-20 tokens and Uniswap.
``` bash
1: Check Address Balance
2: Transfer Token
3: Place Token Order
4: Withdraw Wrapped Ether
5: Add Token Account
```

**Check Address Balance** is similiar to the Ether version except you first provide the ERC-20 token's contract address.

**Transfer Token** is a function for transferring ERC-20 tokens from one address to another.

**Place Token Order** lets you place an order for an ERC-20 token on Uniswap either with Ether or another ERC-20 token, there's different functionality for both scenarios as swaps that are paid for in ERC-20 need approval transaction to be broadcast first. You also need to select some different parameters like maximum slips and fee pools. I recommend checking swap data on the Uniswap website before attempting a swap. Also make sure that you're checking the Uniswap V3 router as I've hard coded support for only the V3 router currently.

**Withdraw Wrapped Ether** is for when you've executed an ERC-20 to Ether swap and you need to unwrap the received Ether as Uniswap uses Wrapped Ether rather than native Ether for swaps where you've receiving Ether.

**Add Token Account** is for manually linking one of your Ethereum accounts to an ERC-20 token contract to check for balances in the token that are listed when you select **My Accounts** in the main interface.

If you were to have selected 6 in the main interface you would be brought to the Ethereum Name Service menu for resolving/purchasing/renewing ENS names.
``` bash
1: Resolve Name
2: Resolve Address
3: Purchase Name
4: Renew Name
```
**Resolve Name** takes an ENS name and returns the resolved address.

**Resolve Address** this takes an address and reverse resolves it into an ENS name, note that reverse resolving does not guarentee that the ENS name resolves to the address as it doesn't guarentee the address is the owner.

**Purchase Name** lets you purchase an ENS name with one of the accounts that you own, by default I've hardcoded it so that the address you purchase with is what the ENS name resolves too. Purchasing a name involves a two transaction process for commiting to the purchase and purchasing two minutes after the commit is included in a block.

**Renew Name** Renews the purchase of an ENS name you own for an amount of days.

That's all of the functionality I've implemented currently, in the future I may add HD wallet support and some other features, perhaps even a GUI one day. Thanks for reading the documentation and I hope you find some use for the source code, there is no license so do whatever you'd like with it. Just be careful and watch out for some bugs, I've tested every feature but there may be bugs I haven't found yet.
