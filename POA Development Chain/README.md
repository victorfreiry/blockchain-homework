The Proof of Authority (PoA) algorithm is typically used for private blockchain networks as it requires pre-approval of, or voting in of, the account addresses that can approve transactions (seal blocks).

Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as our pre-approved sealer addresses.

Create accounts for two nodes for the network with a separate datadir for each using geth.
./geth --datadir node1 account new
./geth --datadir node2 account new
Next, generate your genesis block.

Now use puppeth to create a new network, and navagate the options to configure a new genesis block.

1- Choose the Clique (Proof of Authority) consensus algorithm.
2- Paste both account addresses from the first step one at a time into the list of accounts to seal.
3- Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.
4- You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.
5- Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.
6- Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.
7- initialize the nodes with the genesis' json file.

Using geth, initialize each node with the new networkname.json.
./geth --datadir node1 init networkname.json
./geth --datadir node2 init networkname.json
Now the nodes can be used to begin mining blocks.

NOTE: Make sure to get your enode address in the lines after running Node 1.

Run the nodes in separate terminal windows with the commands:
./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

NOTE: Type your password and hit enter - even if you can't see it visually!
Your private PoA blockchain should now be running!

NOTE: Nodes are now up and running, the blockchain can be added to MyCrypto wallet for trial.

*Open the MyCrypto wallet, then click Change Network at the bottom left:*
change network
![alt text](https://github.com/victorlfreire/blockchain-homework/blob/main/POA%20Development%20Chain/images/change%20netwrok.PNG)

*Click "Add Custom Node", then add the custom network information that you set in the genesis.*

![alt text](https://github.com/victorlfreire/blockchain-homework/blob/main/POA%20Development%20Chain/images/Add%20custom%20node.PNG)

Make sure that you scroll down to choose Custom in the "Network" column to reveal more options like Chain ID:

1- Custom network
2- Type ETH in the Currency box.
3- In the Chain ID box, type the chain id you generated during genesis creation.
4- In the URL box type: http://127.0.0.1:8545. This points to the default RPC port on your local machine.

Finally, click Save & Use Custom Node.

After connecting to the custom network in MyCrypto, it can be tested by sending money between accounts.

Select the View & Send option from the left menu pane, then click Keystore file.
select_keystore_file

On the next screen, click Select Wallet File, then navigate to the keystore directory inside your Node 1 directory, select the file located there, provide your password when prompted and then click Unlock.

This will open your account wallet inside MyCrypto.

NOTE: Testnets usually fund a lot of ETH into accounts, you will most likely never need to use a faucet to fund more test ETH to your acount.

keystore_unlock

In the To Address box, type the account address from Node2, then fill in an arbitrary amount of ETH:
transaction send

Confirm the transaction by clicking "Send Transaction", and the "Send" button in the pop-up window.
Send transaction
![alt text](https://github.com/victorlfreire/blockchain-homework/blob/main/POA%20Development%20Chain/images/confirmation.PNG)


Click the Check TX Status when the green message pops up, confirm the logout:
check tx

You should see the transaction go from Pending to Successful in around the same blocktime you set in the genesis.

You can click the Check TX Status button to update the status.
![alt text](https://github.com/victorlfreire/blockchain-homework/blob/main/POA%20Development%20Chain/images/check%20tx.PNG)

successful transaction
