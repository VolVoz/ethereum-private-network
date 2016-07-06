# Building Ethereum

## Installation Instructions for Mac

By far the easiest way to install go-ethereum is to use our Homebrew tap. If you don't have Homebrew, install it first.

Then run the following commands to add the tap and install geth:

```
brew tap ethereum/ethereum
brew install ethereum
```
After installing, run ```geth account new``` to create an account on your node.

## Installation Instructions for Linux/Unix
### Installation Instructions for Ubuntu
For the latest development snapshot, both ppa:ethereum/ethereum.

```
sudo apt-get install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```
After installing, run ```geth account new``` to create an account on your node.

You should now be able to run ```geth``` and connect to the network.

Make sure to check the different options and commands with ```geth --help```

You can alternatively install only the geth CLI with ```sudo apt-get install geth``` if you don't want to install the other utilities (bootnode, evm, disasm, rlpdump, ethtest).


### Installation Instructions for  Fedora 22

1. sudo dnf install golang
2. dnf install automake make gcc gcc-c++ git gmp-devel kernel-devel
Run the following commands as a normal (non-root) user following instructions here https://github.com/ethereum/go-ethereum/wiki/Installation-Instructions-for-Ubuntu:

3. git clone https://github.com/ethereum/go-ethereum
4. cd go-ethereum
5. make geth

To run geth, enter this command in a command line terminal from your normal user account:

```
build/bin/geth
```

# Connecting to our "Quinta" private ethereum network

Clone repo with our custom genesis block
```
git clone https://github.com/VolVoz/ethereum-private-network.git

cd ethereum-private-network
```

There are some command line options (also called "flags") that are necessary in order to make sure that your network is private.

```
--nodiscover
```
Use this to make sure that your node is not discoverable by people who do not manually add you. Otherwise, there is a chance that your node may be inadvertently added to a stranger's node if they have the same genesis file and network id.
```
--maxpeers 0
```
Use maxpeers 0 if you do not want anyone else connecting to your test chain. Alternatively, you can adjust this number if you know exactly how many peers you want connecting to your private chain.
```
geth init genesis.json

geth --datadir ethereum-private/ --networkid 9876 --nodiscover --maxpeers 0 console
```

Create a new account on the console:
```
> personal.newAccount("very hard password") ,for example: "mYlittlEethereuMunicorN"

```

Start miner for generating DAG and mine some blocks:
```
> miner.start(10)
> miner.stop()
```
Check your ether balance
```
> primary = eth.accounts[0];
> balance = web3.fromWei(eth.getBalance(primary), "ether");

to disconnect
Ctrl+D
```

For connecting to "Quinta" private testnet you must run your geth with following flags:
```
--port "10001"
```
This is the "network listening port", which you will use to connect with other peers manually.
```
--rpc
```
This will enable RPC interface on your node. This is generally enabled by default in Geth.
```
--rpccorsdomain "http://23.94.171.200:3030"
```
This dictates what URLs can connect to your node in order to perform RPC client tasks.
```
--networkid 9876
```
Network identifier

Run geth:
```
 geth --datadir ethereum-private/ --networkid 9876 --rpc --rpccorsdomain "http://23.94.171.200:3030" --unlock=0 --port "10001" console
```
Note: Genesis block must be:
```
Successfully wrote custom genesis block: dd8a406402626663a5a1a319408ab278c995d037f313fe20e8c670c6c093c3b4
```
Go to http://23.94.171.200:3030 in you browser.


To add you to our private network, send your static node. in console run:
```
> admin.nodeInfo.enode
"enode://4100e89e8b11762d690df6de19da38613638e5c39dd52646c2ae5a3dcd4ef5cae71b46e20c3ea4edb3e2e5d6e902598fadc64f2232da56fa7183f893d9976489@[::]:10001"
```

In pull request into "static-nodes.json" add your enode like:
```
[
"enode://pubkey@ip:10001",
]
```

#Introduction to writing smart contracts

To write a smart contracts I use solidity browser.
You can use solidity browser on web:

https://ethereum.github.io/browser-solidity/
```
... --rpccorsdomain "http://23.94.171.200:3030, https://ethereum.github.io" ...
```

or run him on you localhost:

```
git clone -b gh-pages https://github.com/ethereum/browser-solidity.git
cd browser-solidity
python -m SimpleHTTPServer
```
Run geth with parameters:
```
... --rpccorsdomain "http://23.94.171.200:3030, http://localhost:8000"
```
