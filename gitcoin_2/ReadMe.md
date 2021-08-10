## Gitcoin: 2) Deploy a Simple Ethereum Smart Contract on Polyjuice

1) A screenshot of the console output immediately after you have successfully deployed a smart contract.

![](./deployed-contract.png)
    
2) The transaction hash from the contract deployment (in text format).

   Transaction hash: 0x001ef0c89783dcf94614450382ddab5e62cbf5cbf43e360518897fe3e27a5a81

3) The deployed contract address from the contract deployment (in text format).

   Deployed contract address: 0x2238066dF2525a431C9170Fd99Efe4243BD52Aa6







Deploy a Simple Ethereum Smart Contract on Polyjuice

Compiling and deploying a smart contract on Nervos' EVM compatible Layer 2 is a process that has a lot of similarity to the process on Ethereum. There are only a few small changes that need to be made.

The end goal of Polyjuice is to provide 100% compatibility with all EVM based dApps and EVM tooling. However, development is still in progress. This goal has not been fully realized yet, but it is getting closer by the day.
Task Instructions

    Note: Before starting the tasks, it is recommended that you review the Task Submission section so you know what materials you will need to provide to judges to review your task submission.

In this task you will take a very basic smart contract written in Ethereum's Solidity, compile it to EVM bytecode, and deploy it to Polyjuice on Layer 2.

The code we will be working with in this step will compile your smart contract and deploy it. This uses the original versions of Web3.js and Truffle for Ethereum, with the only difference being that they use a custom Web3.js provider.

The instructions will provide a basic smart contract you can work with, but you should feel free to use any smart contract of your choosing. However, we recommend only using basic smart contracts that have a functions to read and write basic values to ensure you can complete this task and future tasks.
Prerequisites

Before you begin on this task you must complete the previous task to create a Godwoken account on the EVM Layer 2 Testnet. You will also need the private key and Testnet address from the previous task in order to proceed. If you have not completed it, please do so now.
1. Prepare Your Ethereum Private Key

In the previous task, you extracted the private key for your Nervos CKB Layer 1 account. Next we need to extract the private key for your Ethereum account. This private key will be used by the tooling to deploy your smart contract on Layer 2. Attempting to recycle your Layer 1 private key as a Layer 2 private key is not recommended and may cause the process to fail.

    Note: Never use a private key that is associated with a real account for any of these tasks. The following steps will show you how to extract your private key from MetaMask, but you should never do this using a MetaMask installation that you use for real funds since this could potentially leak infomation that could compromise your account.

If you need instructions on how to extract your private key from MetaMask, follow the steps in this tutorial.
2. Clone and Setup the Gitcoin Task Instruction Examples

In this step you will clone the Gitcoin Task Instructions examples repository. This which contains the example code required by this task, and future tasks.

First, we need to clone the Gitcoin Task Instructions examples repository:

mkdir -p ~/projects
cd ~/projects
git clone https://github.com/kuzirashi/gw-gitcoin-instruction
cd ~/projects/gw-gitcoin-instruction

Then we install all dependencies:

yarn install-all

3. Compile the Smart Contract and Copy the Artifact

Before you deploy a smart contract you need to compile it. This can be done in several ways, but our instructions will compile it using the Truffle compiler. If you have an alternate method you prefer, feel free to use it.
Using the Truffle Compiler

Provided below is a simple smart contract example that you can use, however you can use any smart contract you wish for this task.

The example Solidity smart contract below is SimpleStorage.sol, and it is located in the src/examples/2-deploy-contract/contracts directory.

pragma solidity >=0.8.0;

contract SimpleStorage {
  uint storedData;

  constructor() payable {
    storedData = 123;
  }

  function set(uint x) public payable {
    storedData = x;
  }

  function get() public view returns (uint) {
    return storedData;
  }
}

The command below can be used to compile the Solidity into EVM bytecode using the Truffle compiler. This process will use Docker. If you do not have Docker installed, please revisit the task setup and requirements page.

cd ~/projects/gw-gitcoin-instruction/src/examples/2-deploy-contract/
yarn compile

After the command is complete you will find the compiled file in the build/contracts directory. ie: src/examples/2-deploy-contract/build/contracts/SimpleStorage.json
Alternative: Using the Remix Compiler

If for some reason the Truffle compiler isn't working, you can use the Remix web-based compiler as an alternative, but we will not be providing detailed instructions on using Remix. This is only recommended if you are already familiar with this tool, or you are having trouble with the Truffle compiler.

After uploading and compiling your Solidity code, you will receive a JSON file that can be found in Remix's "artifacts" directory. Place the contents of this file in src/examples/2-deploy-contract/build/contracts directory.
4. Deploy a Smart Contract Using Web3.js

In the `gw-gitcoin-instruction/src/examples/2-deploy-contract/ directory you will find the script needed to deploy a smart contract to Nervos Layer 2.

First, update the Ethereum private key in the file gw-gitcoin-instruction/src/examples/2-deploy-contract/index.js. Replace <YOUR_ETHEREUM_PRIVATE_KEY> with your Ethereum private key. This should be the private key that corresponds with the Ethereum account that was funded previously. This will be used to deploy the smart contract on Layer 2.

Run the `gw-gitcoin-instruction/src/examples/2-deploy-contract/index.js script via console using the following commands:

cd ~/projects/gw-gitcoin-instruction/src/examples/2-deploy-contract/
node index.js SimpleStorage.json

After running the command, the contract should deploy without any errors. You will be presented with a transaction hash, and an Ethereum contract address. The transaction hash is provided by Godwoken, and Ethereum contract address is provided by Polyjuice. Keep track of these values as they will be needed in the future tasks and for task submission.