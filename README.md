# Project ZBlock

Project ZBlock is the project name for the development of ZBank's private blockchain.  We'll use this blockchain for testing and development to explore how we can use blockchain here at ZBank.  Our blockchain network has two nodes, each with its own address (public key).  The addresses are stored in the text file called [Node_Keys](/Node_Keys.txt).  The nodes are essentially servers in the blockchain network that verify (mine) the transactions that occur on the blockchain.  If a transaction is deemed valid, it is accepted as a new block in the chain.

Transactions on the ZBank blockchain will be verified by a proof of authority consensus algorithm called Clique.  As a proof of authority type of consensus, Clique relies on trusted nodes (our blockchain nodes) to validate each block on the blockchain.  Each block will take approximately 15 seconds to complete once initiated.  The blockchain network ID is 333.  We'll need this ID to send transactions on the chain.  

As a develeper for Project ZBlock, you will need to be able to start the blockchain network and send transactions.  

### Installations

The first thing you will need to do is install Go Ethereum (Geth) Tools.  On the [Download Geth web page](https://geth.ethereum.org/downloads/), download "Geth & Tools 1.9.7."  Decompress the downloaded ZIP file onto your hard drive into a folder called ZBank-Blockchain.

Next, install the MyCrypto application.  Go to the [MyCrypto downloads page](https://download.mycrypto.com/) and install the latest version of the software.

### Initialize the Blockchain Network

The data for the nodes in the Zbank blockcahrin are in the files in this repository called node1 and node2. Download both of these files and the file called zbank.json to the ZBank-Blockchain folder.  The JSON file contains the ZBank blockchain network configuration data.

To initialize the nodes, open up a Git Bash terminal and change directory to ZBank-Blockchain.  Run the following commands (these are also found in the text file called [Initialize_Nodes](/Initialize_Nodes.txt)).  When prompted for a password, enter zbankgenesis.

- ./geth --datadir node1 --unlock "0dCAF04C1128F0b6519B6DE5ef14AFe39a01E612" --mine --rpc --allow-insecure-unlock

- ./geth --datadir node2 --unlock "14a15DB65A2B50b34861e71e0eB8CA3fffC05d7f" --mine --port 30304 --bootnodes "enode://dbf453e4b109ac76d3ae2ff637db078aa0d2dc38a3a4e9c7d609623b253fedd386e5d905571ff67c8cdb2da39be107bbb37d5d4048ee278b8119cc384fd0c731@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

These commands unlock each node using the node address for each node.  The mine flag instruct the nodes to being the mining process.  After the mine flag, the code varies slightly for each node.  

The rpc flag in the code for Node 1 enables communication between Node 1 and Node 2 so that we can perform transactions on the blockchain.  

The code for initializing Node 2 uses the enode address from the initialization of Node 1.  The enode (Ethereum node) address contains the encoded node ID followed by @ and the host address and port number for Node 1. We need to specify port 30304 for Node 2 because Node 1 is running on port 30303, as indicated in the enode address.  The bootnodes flag enables discovery of other nodes in the network.  The ipcdisable flag in the code for Node 2 disables IPC sockets in Windows.  

Finally, in the code for both nodes, the last flag, allow-insecure-unlock, unlocks the accounts.

### Sending Transactions

In MyCrypto, click on Change Network in the menu on the left side of the screen.  Select Custom.  Enter the following information:

- Node Name: Puppernet
- Network: Custom
- Network Name: Puppernet
- Currency: ETH
- Chain ID: 333
- URL: http://127.0.0.1.8545

![My Crypto Custom Network Information](/Screenshots/MyCryptoCustomNode.png)

Select Save & Use Custom Node.  

To open up the account wallet, select View & Send from the left menu.  Click on KeystoreFile at the bottom of the main screen.  Click on Select Wallet File and navigate to node1 > keystore and select the file in that folder (the file name begins with UTC).  Enter the password zbankgenesis.  

Now you can send transactions on the blockchain.  Copy and paste the following account address from node2 (this is found in the file called [Node_Keys](/Node_Keys.txt)):

0x14a15DB65A2B50b34861e71e0eB8CA3fffC05d7f

Enter any amount of ETH and click Send Transaction.  Click Send in the confirmation window.  Click on Check TX Status in the green box that pops up to view the transaction status.  It will change from Pending to Successful.

![My Crypto Transaction Successful](/Screenshots/04MyCrypto_Transaction_Successful.PNG)

