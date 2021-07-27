# Blockchain_POA_homework18

-----------------------------------------------------
Submitted by: Rina Niles

-----------------------------------------------------


## Summary
The purpose of this code is to become familiar with a Proof of Authority Blockchain. We will create an ethereum test network (name: test4) and send ETH from Node 1 to Node 2. 


### Prerequisities
You will need to install Go Etherum (https://geth.ethereum.org/) and MyCrpyto (https://download.mycrypto.com/)

### Step 1. Initialize 2 nodes, create gensis network
The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks).  

1a. Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

    * Create accounts for two nodes for the network with a separate `datadir` for each using `geth`.
        * ./geth --datadir node1 account new
        * ./geth --datadir node2 account new
        
![Initialize Nodes](Images/Create_Nodes.png)


1b. Next, generate your genesis block.

    * Run `puppeth`, name your network test4, and select the option to configure a new genesis block.

    * Choose the `Clique (Proof of Authority)` consensus algorithm.

    * Paste both account addresses from the first step one at a time into the list of accounts to seal.

    * Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.

    * You can choose `no` for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.

    * Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.

    * Export genesis configurations. This will fail to create two of the files, but you only need `test4.json`.
    
![Create Gensis Block](Images/Config_Gensis.png)    

1c. With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.

    * Using `geth`, initialize each node with the new `networkname.json`.
        * ./geth --datadir node1 init test4.json
        * ./geth --datadir node2 init test4.json
        

![Start Nodes](Images/Init_Nodes.png)    



Your private PoA blockchain should now be running!



### Step 2. Activate mining  
Now the nodes can be used to begin mining blocks.

    * Run the nodes in separate terminal windows with the commands:
        *  ./geth --datadir node1 --unlock "0x202eC8083255304d5272f1E7C21cB0ECB03c88B2" --mine --rpc --allow-insecure-unlock
        *  ./geth --datadir node2 --unlock "0x3F5BdC0dc6Bbd38757CE71995CAE957A55f398Cb" --mine --port 30304 --bootnodes "enode://03f3967727bf1c2e8e8282c93b95cb1c21913f95d3961230dd821f550e70026261da4528275198bfad813641d2265340a3cb4bff8220fd048f59f37032c0ddfc@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
        
    * **NOTE:** Type your password (test1) and hit enter - even if you can't see it visually!

![Start Mining](Images/Mining.png)
  

### Step 3. Add test blockchain (test4) to MyCryto
 
With both nodes up and running, the blockchain can be added to MyCrypto for testing.

3a. Open the MyCrypto app, then click `Change Network` at the bottom left:

  ![change network](Images/change-network-Copy1.png)

    * Click "Add Custom Node", then add the custom network information that you set in the genesis.

    * Make sure that you scroll down to choose `Custom` in the "Network" column to reveal more options like `Chain ID`:

   ![custom network](Images/custom-node.png)

    * Type `ETH` in the Currency box.
    
    * In the Chain ID box, type the chain id you generated during genesis creation.

    * In the URL box type: `http://127.0.0.1:8545`.  This points to the default RPC port on your local machine.

    * Finally, click `Save & Use Custom Node`. 

3b. After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

    * Select the `View & Send` option from the left menu pane, then click `Keystore file`.

   ![select_keystore_file](Images/select_keystore_file.png)

    * On the next screen, click `Select Wallet File`, then navigate to the keystore directory inside your Node1 directory, select the file located there, provide your password when prompted and then click `Unlock`.

    * This will open your account wallet inside MyCrypto. 
    
    * Looks like we're filthy rich! This is the balance that was pre-funded for this account in the genesis configuration; however, these millions of ETH tokens are just for testing purposes.   

   ![keystore_unlock](Images/keystore_unlock.gif)

    * In the `To Address` box, type the account address from Node2, then fill in an arbitrary amount of ETH:

   ![transaction send](Images/transaction-send.png)

    * Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.  

   ![Send transaction](Images/send-transaction.gif)

    * Click the `Check TX Status` when the green message pops up, confirm the logout:

   ![check tx](Images/check-tx-status.png)

    * You should see the transaction go from `Pending` to `Successful` in around the same blocktime you set in the genesis.

    * You can click the `Check TX Status` button to update the status.

   ![successful transaction](Images/txn-pending.png)
   
***NOTE: I have not been able to achieve a SUCCESS status on my txn yet...

Congratulations, you successfully created your own private blockchain!

## Conclusions and Next steps

