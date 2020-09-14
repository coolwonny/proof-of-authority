# Proof of Authority: Building a testnet blockchain

In this assignment, we will be setting up a new private testnet blockchain that enables developers to explore potentials for blockchain environment.
As this will be a testnet, we're going to use the Proof of Authority, or POA, for our consensus algorithm. 

For doing that, we need to create two node accounts, initializing them to run mining with the **RPC** flag which will communicate with the Mycrypto application. Once the two nodes start mining, then we need to set up a custom network at Mycrypto for the test.    

## Instruction: Running the POA Blockchain
* Create a new folder (we named it `poa`) and download `geth` configuration. 

* Create accounts for two nodes for the network with a separate `datadir` for each using `geth`.
    * ./geth account new --datadir node1
    * ./geth account new --datadir node2 
​
* Run `puppeth`, name the network (we named it `marcus`), and select the option to configure a new genesis block.
​
* Choose the `Clique (Proof of Authority)` consensus algorithm.
​
* Paste both account addresses from the first step one at a time into the list of accounts to seal.
​
* Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.
​
* You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.    
​
![puppeth_1](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_puppeth1.png)

* Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.
​
* Export genesis configurations. This will fail to create two of the files, but you only need `networkname.json` (here is `marcus.json`).
​
* Initialize each node with the new `networkname.json` with `geth`.
    * ./geth init networkname.json --datadir node1
    * ./geth init networkname.json --datadir node2      

​![puppeth_2](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_puppeth2.png)


* Runs the nodes in separate terminal windows with the commands:
    *  ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock  

![node1](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_node1.png)    

    *  ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock    

![node2](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_node2.png)    

Note that the `--mine` flag is for mining and `--rpc` is for communication with the other network. Also, we used `--port 30304` because the node1 already occupied port 30303. `--bootnodes` enalbes node2 to connect with node1.   

When all nodes are producing new blocks, it's time for moving on to the next process.   

## Instruction: Testing transactions
   
* Go to the Mycrypto app. You may see `Change Network` and the current status of network on the left panel.   
![1](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_1.png)   

* Click the `Change Network`, then click the `Add Custom Node`.    
![2](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_2.png)    

* A new screen will pop up. Here you need to put your Node and Network name, Chain ID and URL as shown in the figure below.    
(note: the orange signs are shown up because we have already created our custom network)    
![3](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_3.png)    

* Now you can see your new custom network created on the left panel. Click on it to change it to your network.   
![4](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_4.png)   

* Congratulations! You now are connected to your own network. To get access to your account, click the `Keystore File` in the bottom.    
![5](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_5.png)    

* Click `Select Wallet File`. Import the keystore file from the node1/keystore directory into MyCrypto. This will import the private key. It will take a few seconds loading it.    
![6](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_6.png)    

* Now you can see your keystore file shown under the button. Input the password (the one you used in the process of `puppeth`) and unlock it.    
![7](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_7.png)    

* You may find the node1 address on the right side with its current balance below. For testing a transaction, input the node2 address at `To Address` with an amount you'd like to send at `Amount`. Then click the `Send Transaction`.    
![8](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_8.png)    

* A new window will pop up for your confirmation.
![9](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_9.png)    

* At the bottom, you may see a green box indicating the TX Hash. Click the `Check TX Status`.    
![10](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_10.png)    

* The result of transaction will be displayed. 
![11](https://github.com/coolwonny/proof-of-authority/blob/master/images/screenshot_connect_11.png)      

## Conclusion
     
We have demonstrated how to create a new testnet blockchain from scratch using the POA algorithm. You may find it stressful if you experience errors and enless `Looking for Peers` messages while mining blocks. We went through the same and got the successful result after several trials so don't get stressed out.   

In this way, the developers may be able to explore and test the blockchain by applying many scenarios. We hope this was helpful!












