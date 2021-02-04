# Proof of Authority Development Chain

The Proof of Authority Development Chain was setup to send a test transaction.

## Installing Dependencies

* Anaconda (including terminal window) (https://docs.anaconda.com/anaconda/install/)

* Geth & Tools (https://geth.ethereum.org/downloads/)

* MyCrypto (https://download.mycrypto.com/)

<br>

## Instructions and Environment Configurations

* Unzip `Geth` including `puppeth` to a designated folder directory 
    * Geth is a command-line tool used to create keys, initialize nodes, and connect the nodes together

    * Puppeth installed with Geth is used to generate the genesis block

* Open a Terminal window and navigate to the designated folder directory 

* Create accounts for two nodes ( ./geth --datadir znode1 account new) and (./geth --datadir znode2 account new )

* Run `puppeth` ( ./puppeth ) to configure a new genesis using Clique (Proof of Authority) algorithm and the following settings:
    * **Network Name: `"zbank"`** 
    * **Blocktime default: `15 seconds`**
    * **Chain ID: `333`**

* Seal the public key addresses for both nodes into the list of accounts to pre-fund the accounts
    * **First node:**  znode1 key created with password geth1<br>
    Public address of the key:   0x62d69A1E3115D6b441A5C834E41A0F4449C9Cc3A

    * **Second node:**  znode2 key created with password geth2<br>
Public address of the key:  0x1742c3F5b955239E995BC73E0c3979f13e98c464

* Export the successful genesis configuration ( `zbank.json` )

* Initialize the first node using the genesis .json file by running the command: `./geth --datadir znode1 init zbank.json`
<br>
Unlock the account and enable mining using the RPC flag by running the command: `./geth --datadir znode1 --unlock "0x62d69A1E3115D6b441A5C834E41A0F4449C9Cc3A" --mine --rpc --allow-insecure-unlock`

* Initialize the second node using the genesis .json file by running the command: `./geth --datadir znode2 init zbank.json`, unlock the account and enable mining using the first node's **enode** address as the bootnode flag by running the command: 

    `./geth --datadir znode2 --unlock "0x1742c3F5b955239E995BC73E0c3979f13e98c464" --mine --port 30304 --bootnodes "enode://a60ff13f7c183617391916801744f4add12b83cfcaeadc23fecb846f2b7b7a20b21e6a7093cec2d71548f41261176af38f4961ad7206ef77ba3a46fa4b08bc36@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`

### *Description of `geth` flags:* 
* The --mine flag tells the node to mine new blocks

* The --rpc flag enables you to talk to the second node and allows for transacting with the chain (used MyCrypto)

* The first node's sync port used 30303 (referenced in the enode) the second node's port is changed using --port

* The --bootnodes flag allows the required network information to pass to other nodes in the blockchain and will keep both of the nodes connected

* The --ipcdisable is used for Microsoft Windows to safely disable the multiple IPC/Unix sockets running


### Sending Test Transaction using MyCrypto

* Use MyCrypto GUI wallet to connect to the first node (znode1) that includes the RPC port

* Custom node `zbank` created to send the transaction in currency **ETH** by connecting to the network **Puppernet** and Chain ID **333** 
    * *Note: a new custom node using the `zbank` network/chain ID **333** could not be  generated because the network/chain ID **333** already existed for the network **"Puppernet"***
    <br>

    **Custom_Node (zbank) using Puppernet Network**
    ![](/Screenshots/custom_node_rev.png)

<br>
* Using the Keystore file in MyCrypto, the private key is imported from the `znode1/keystore` directory into MyCrypto

* Blockchain successfully created and transaction was sent from the `znode1` account to the `znode2` account

    **Transaction Sent** <br>
    TX Hash: 0xedcc4cf9f984a576ffc70bc97f59b6a774c67efa23876eaa1238fe26332ccf46
    ![TX_metadata](/Screenshots/TX_metadata.png)

