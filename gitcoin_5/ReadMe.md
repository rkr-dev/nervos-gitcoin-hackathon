## Gitcoin: 5)  Deploy the ERC20 Proxy Contract for the Deposited SUDT

1) A screenshot of the console output immediately after deploying smart contract.
![](./deploy-sudt-erc20-proxy-contract.png)


2) The address of the ERC20 Proxy Contract you deployed (in text format).
   Deployed SUDT-ERC20 Proxy contract address: 0x6AAd4A42B72C43ECC4dA180a1e6eD8B43b0a9171

3) A screenshot of the console output immediately after checking your SUDT balance.
![](./check-sudt-balance.png)

4) The Ethereum address that was checked (in text format).
Using Ethereum address: 0x73379E41FDaf0570325db0727c4150dE6b0384D5



Deploy the ERC20 Proxy Contract for the Deposited SUDT

In order to use SUDT tokens that have been moved between Layer 1 and Layer 2, you will need to deploy the ERC20 Proxy Contract to interact with them. This special Solidity smart contract has been prepared by the Nervos team to allow EVM to interact with SUDT tokens on Nervos.

The ERC20 Proxy Contract is a modified ERC20 Solidity contract where the token balance and transfer functions have been modified to interact directly with the Polyjuice EVM compatibility layer. This allows Ethereum smart contracts to use an ERC20 interface to work with SUDT tokens on Layer 2.
Task Instructions

    Note: Before starting the tasks, it is recommended that you review the Task Submission section so you know what materials you will need to provide to judges to review your task submission.

We will use some example code that you will need to populate with values such as your private key and Ethereum address. After updating the values, we will execute the script to deploy the ERC20 Proxy Contract, and we'll then use it to check your SUDT balance on Nervos' Layer 2!

    Note: Your private keys are used to secure your accounts and all the funds and assets contained within. It is important to keep your private keys safe, and to only use them with tools you can trust. However, on these tasks we will only be working with Testnet funds and assets that have no value. You can operate without concern knowing that there is nothing at risk.

Prerequisites

To deploy the ERC20 Proxy Contract, also known as the SUDT-ERC20 Proxy Contract, you need to first have a Layer 2 SUDT ID. This can be found by depositing an SUDT to Layer 2 using the account-cli tool, which was done in the previous task. If you have not completed this task, please do so before proceeding.

This task requires the Gitcoin Task Instruction Examples repo (gw-gitcoin-instruction) which was setup in task 2. If you do not have this repo available for any reason, please set it up now.
1. Compile the Smart Contract and Copy the Artifact

Before you deploy a smart contract you need to compile it. Our instructions will show you how to quickly compile a smart contract using the Truffle compiler.

The SUDT-ERC20 Proxy Solidity smart contract below is SudtERC20Proxy.sol, and it is located in the `gw-gitcoin-instruction/src/examples/5-erc20-proxy/contracts/SudtERC20Proxy.sol file.

The command below can be used to compile the Solidity into EVM bytecode using the Truffle compiler. This process will use Docker. If you do not have Docker installed, please revisit the task setup and requirements page.

cd ~/projects/gw-gitcoin-instruction/src/examples/5-erc20-proxy
yarn compile

After the command is complete you will find the compiled file in the build/contracts directory. ie: src/examples/5-erc20-proxy/build/contracts/ERC20.json
2. Deploy the SUDT-ERC20 Proxy Contract Using Web3.js

Next we will use the example code to deploy the smart contract. Open the file src/examples/5-erc20-proxy/index.js in an editor of your choosing. You will need to update the values in index.js to match your Ethereum private key and SUDT ID.
Ethereum Private Key

This private key will be used to deploy the smart contract, and it should be the same Ethereum private key that funds were added to in the previous tasks. Make sure you use your Ethereum private key for Layer 2, not your Nervos CKB Layer 1 private key. Replace <YOUR_ETHEREUM_PRIVATE_KEY> with this value.

const ACCOUNT_PRIVATE_KEY = '<YOUR_ETHEREUM_PRIVATE_KEY>';

SUDT ID

The SUDT ID is needed by the deployed contract in order to associate it with a specific SUDT token. This creates a 1:1 binding between the Ethereum smart contract and the Layer 2 SUDT token that cannot be changed once deployed. Replace <YOUR_SUDT_ID> with the SUDT ID from the token you created earlier.

const SUDT_ID = '<YOUR_SUDT_ID>';

Run the Script

After all values have been replaced, use the following commands in a console to execute the script.

cd ~/projects/gw-gitcoin-instruction/src/examples/5-erc20-proxy
node index.js

After running the command, the contract should deploy without any errors. You will be presented with a transaction hash, and an Ethereum contract address. The transaction hash is provided by Godwoken, and Ethereum contract address is provided by Polyjuice. Keep track of these values as they will be needed in the future tasks and for task submission.

Example Output:

➜ node index.js
Using Ethereum address: 0xD173313A51f8fc37BcF67569b463abd89d81844f
Deploying contract...
Transaction hash: 0xcfa9a2e6d691fd095b4cb2edbea3437bd6de7fedd210e8a55c2ccc5c24b32ad5
Deployed SUDT-ERC20 Proxy contract address: 0xc013772cAAaBf6ca3F584B6D7b98e73a701233b5

3. Check your Layer 2 SUDT balance

Once the SUDT-ERC20 proxy smart contract has been deployed for your SUDT, you can check the token balance for any account. This can be done by calling the ERC20ProxyContract.balanceOf method. It accepts the account or smart contract address as first and the only argument. One important thing to remember though is that this is a Polyjuice address, not your Ethereum address. When dealing with addresses on-chain in smart contract calls, you will almost always want to use Polyjuice address.

What is a Polyjuice address, you ask? A Polyjuice address is the address that Nervos' Layer 2 uses internally to track the Ethereum address behind it. The concept of Polyjuice address exists because of the cross-chain Layer 2 architecture used by Nervos. It is not possible to use the Ethereum address on Nervos Layer 2 because Nervos Layer 2 is designed to also support many other type of blockchain accounts. The addresses from all these different blockchains must be standardized to a single format that Nervos can utilize internally.

Don't worry though, it's extremely easy to go from the Ethereum to Polyjuice address and vice-versa. The example code to demonstrate this is included in examples/5-erc20-proxy/check-sudt-balance.js. You can also use account-cli tool to do a one time conversion using command-line. The instructions for account-cli can be found here.

Next we will check an SUDT balance using the provided example code. Open the file src/examples/5-erc20-proxy/check-sudt-balance.js in an editor of your choosing. You will need to update the values in index.js to match your Ethereum address and the ERC20 Proxy Contract address.
Ethereum Address

The script will need to know which Ethereum address we will check the balance of. Replace <YOUR_ETHEREUM_ADDRESS> with the Ethereum address that you previously deposited your SUDT to.

const ETHEREUM_ADDRESS = '<YOUR_ETHEREUM_ADDRESS>';

ERC20 Proxy Contract Address

You should have received SUDT-ERC20 proxy contract address as a result of previous step of this tutorial. Replace <YOUR_SUDT_PROXY_CONTRACT_ADDRESS> with the address of the deployed ERC20 Proxy Cntract.

const SUDT_PROXY_CONTRACT_ADDRESS = '<YOUR_SUDT_PROXY_CONTRACT_ADDRESS>';

Run the Script

After all values have been replaced, use the following commands in a console to execute the script.

cd ~/projects/gw-gitcoin-instruction/src/examples/5-erc20-proxy
node check-sudt-balance.js

Example Output (click to expand)

Congratulations, the number you see at the end of the console output is the balance of SUDT tokens on Layer 2 for your Ethereum account!

You should see a value that is greater than zero since the instructions indicated that you should use the Ethereum account which already had tokens. If you see 0 then recheck the steps above starting with the Ethereum address.
Task Submission

To complete the tasks, add the following materials to a document on your Github and submit for review by the judges (include the link in your Gitcoin submission):

    A screenshot of the console output immediately after deploying smart contract.
    The address of the ERC20 Proxy Contract you deployed (in text format).
    A screenshot of the console output immediately after checking your SUDT balance.
    The Ethereum address that was checked (in text format).

Bonus: Get Layer 2 SUDT ID from Layer 1 SUDT Issuer Lock Hash (AKA SUDT Type Args)

If you have already deposited a SUDT and you don't know its Layer 2 SUDT ID there is a JavaScript code that you can use to retrieve it.

You need to prepare Layer 1 SUDT Issuer Lock Hash (AKA SUDT Type Args) and use src/examples/5-erc20-proxy/get-sudt-id.js.

    Note: Remember to replace <YOUR_SUDT_TYPE_ARGS> inside the script before using it.
