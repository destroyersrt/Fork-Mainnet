# Fork-Mainnet
Interact with InstaDApp DSA using Forked Mainnet from your local network


**Step 1:** Forking the Ethereum Mainnet

Open terminal and run

```javascript
ganache-cli --fork https://mainnet.infura.io/v3/{Project_Id} --unlock {Ethereum_Address} -p {Port_Number} --networkId 1
```
<table class="table">
  <tr>
    <th>Parameters</th>
    <th>  </th> 
  </tr>
  <tr>
    <tr>
    <td>{Project_Id}</td>
    <td>This Id comes from infura. If you don’t know about how to get this, just open infura and create a free account. After creating account add a new project and you will get the Project_Id that you need. Sample Project_Id has been shown below.
</td>
  <tr>
  <tr>
    <td>{Ethereum_Address}</td>
    <td>On forked mainnet you can unlock any account of your choice without knowing their private key. So, let’s say you want to test  something which requires transaction of DAI or other coin. So, you can choose an account which has lots of DAI. This way you can unlock any account of your choice.
</td>
  </tr>
  <tr>
    <td>{Port_Number}</td>
    <td>It is the port number on which you want to run the ganache-cli. The default port number for ganache-cli is 8545</td>
  </tr>
</table>

If you want to fork mainnet at a particular block number you can do that by providing value of Block_Number after infura Project_ID

```javascript
ganache-cli --fork https://mainnet.infura.io/v3/{Project_Id}@{Block_Number} --unlock {Ethereum_Address} -p {Port_Number} --networkId 1
```

After running the command, it will fork the mainnet for you and run ganache

**Note:** If Block’s value in the Forked Chain characteristics is ‘0’ then it means that you have not been able to fork the chain properly.

**Step 2:** Interacting with DSA

Clone the repo on your machine and run 

```javascript
npm install
```
Before interacting with DSA make sure you have configured .env file which contains the private key, Ethereum address and Infura project Id.

`dsa.js` is the file which whill help you interact with DSA.
check if the port number of your ganache-cli matches with the web3 provider's host.

The file contains different sections containing spells, create wallet, setup account and transfer which you can edit as per your needs

After making the required edits in `dsa.js` file. You can run the file by opening another tab in terminal and run 
```javascript
node dsa.js
```
This may take few minutes as ganache has to fetch contracts from mainnet and then work on them so be patient, if you want to know if it has stuck or not then head to the tab on console where the ganache-cli is working and check if it is making some calls.
If you are using the default `dsa.js` file then output will contain `dsa  accounts linked to your ethereum address` and `transaction hash`

To check the transaction receipt you can follow these steps: 


Step 1: Open another terminal tab

Step 2: run 
```javascript
truffle console
``` 
(make sure you have truffle installed on your machine)

Step 3: In the truffle console, run 

```javascript
receipt = await web3.eth.getTransactionReceipt({txHash})
```

# Additional advice
If you want to use any particular token then you can unlock address which holds that token and you can get list of all token holders on 
ethplorer.

If you encounter error saying : “Error: Returned error: Returned error: project ID does not have access to archive state”. Trying reloading the ganache-cli as this will most probably fix this.
 
**Note:** This is not the best way to interact with DSA as you might face a lot of errors in the process of interacting on forked mainnet. The best way is still the Ethereum Mainnet.
