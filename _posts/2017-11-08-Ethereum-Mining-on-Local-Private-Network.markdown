---
layout: post
title: Ethereum Mining on Local Private Network
date: 2017-11-08 04:59:00-0400
description: A guide to setup an Ethereum private network.
comments: true
---

Ethereum Mining on Local Private Network
===

Ethereum Introduction
---

Ethereum is currently the second largest public Blockchain network (only after BitCoin). Mining on the public Ethereum network is a complex task as it's only feasible using GPUs, requiring an OpenCL or CUDA enabled ethminer instance. In a private network setting however, a single CPU miner instance is more than enough for practical purposes as it can produce a stable stream of blocks at the correct intervals without needing heavy resources (consider running on a single thread, no need for multiple ones either). 

In this lab, you will be asked to setup an Ethereum local cluster of nodes on private network and do some mining on it.


Setup Ethereum
---

### 1. **Envrionment Setup**
- `VirtualBox`
- `Ubuntu 14.04.3 LTS`

### 2. **Ethereum setup**

We are gonna build Ethereum from source on the Ubuntu machine.

```
$ git clone https://github.com/ethereum/go-ethereum
```

Building the ```geth``` program using the following command.

```
$ cd go-ethereum
$ make geth
```

Following the prompts to run  geth. If you are trying to build ```geth  ``` on your own host, you will need Go(v1.7).

Setup a Local Network
---

Since connections between nodes are valid only if peers have identical protocol version and network ID, you can effectively isolate your network by setting either of these to a non default value. We recommend using the --networkid command line option for this. Its argument is an integer, the main network has id 1 (the default). So if you supply your own custom network ID which is different than the main network your nodes will not connect to other nodes and form a private network.

### 1. **Setup first node and start mining** 
    
**Step 1**: Every blockchain starts with the genesis block. For a private network, we have to define our own genesis block.

Here is a simple example for how to write a custom ```genesis.json``` file. For this lab you can simply use the ```genesis.json``` file I created.

```
{
    "config": {
        "chainId": 1907,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "difficulty": "4000",
    "gasLimit": "2100000",
    "alloc": {}
}
```

**Step 2: Make a data directory and set up an account to be used by this node.**

```
$ mkdir <datadir>
$ go-ethereum/build/bin/geth --datadir <datadir> account new
```
    
you will be required for a passphrase for the account you just created. You can also create a new account through the Geth Javascript console.
    
**Step 3: Choose a networkid and launch a geth console.**

To create a database that uses this genesis block, run the following command. This will import and set the canonical genesis block for your chain. Future runs of geth on this data directory will use the genesis block you've defined.
    
```
geth --datadir <data-node> init genesis.json
```
    
Now, run the following command to launch the geth console. 
    
```
go-ethereum/build/bin/geth --rpc --rpcaddr "128.230.208.73" --rpcport "8101" --rpccorsdomain "*" --datadir "<datadir>" --port "30303" --networkid 7000 --unlock "0" console init genesis.json
```
    
[This page](https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options) describes the options for ```geth``` command, it can help you understand the command above.
    
**Step 4: Interact with Geth console and do some mining on this node.**
    
[This page](https://github.com/ethereum/go-ethereum/wiki/Management-APIs) describes the Ethereum management APIs, check it for more information. Here is an example.
    
```
> personal.listAccounts     # you should be able to see your accounts information
> personal.newAccount       # create a new account
> eth.coinbase              # check your coinbase, should be same as the first account by default.
> miner.start(1)                # start the miner
> eth.blockNumber           # check the toppest block number on this block chain
> eth.getBlock('latest', true) # get lastest block
> eth.getBlock('pending', true) # get pending block
> miner.getHashRate         # get current hashrate
> eth.getBalance(eth.coinbase) # check balance
> eth.getBalance(web3.eth.accounts[0]) # should be same as eth.coinbase by default
> admin.nodeInfo                    # check the current node information
> miner.stop()              # stop the miner
```
    

### 2. **Setup a Local Cluster**  

In this section, we will run a second miner node.

**Step 1**: You need to follow the **Step 2** and **Step 3** in the last section to setup a data directory and initialise the genesis block for this node. Notice that the genesis block must to be the same, so you don't need to create a new ```genesis.json``` file this time.

**Step 2**: Launch the ```Geth``` console by running the following command
    
```
go-ethereum/build/bin/geth --rpc --rpcaddr "128.230.208.73" --rpcport "<another-rpc-port>" --rpccorsdomain "*" --datadir <new-data-dir> --port <another-port> --networkid 7000 --nat "any" console init genesis.json
```

**Step 3**: Add the previous peer node defined from the last section.

```
> admin.peers                   # check peers, '0' by default
> admin.addPeer(<enode-url>)        # you can check the peer's enode url by running 'admin.nodeInfo' in the previous console, it is defined by the 'enode' field
```
If you successfully add the peer node, you will see the peer node information by running ```admin.peers``` again.

Now, you can simultaneously run the miner on each of the node and observe the result.

Reference
---

[Setting-up-private-network-or-local-cluster](https://github.com/ethereum/go-ethereum/wiki/Setting-up-private-network-or-local-cluster)

[Private-network](https://github.com/ethereum/go-ethereum/wiki/Private-network)

[Establishing a connection](https://github.com/ethereum/go-ethereum/wiki/RLPx-Encryption)

[Ethereum Wire Protocol](https://github.com/ethereum/wiki/wiki/Ethereum-Wire-Protocol)

**Notes: For more information, you can check [my github repository](https://github.com/SamuelXing/EthereumMining)**
