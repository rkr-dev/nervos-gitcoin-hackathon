## Gitcoin: 6)  Use Force Bridge to Deposit Tokens From Ethereum to Polyjuice


1) A screenshot of the console output immediately after you have successfully generated your Deposit Receiver Address.
![](./deposit-reciever-address.png)

2) Your Deposit Receiver Address (in text format).
ckt1q3dz2p4mdrvp5ywu4kk5edl2uc4p03puvx07g7kgqdau3n3dmypkqnxzuefxyp9wdghglncj77k5wt6p59sx6kukyjlwh5s467qgp8m25yqqqqqsqqqqqvqqqqqfjqqqqryga3jchp7jdy5t8zc7em6pjf3dkhwjyjxptdffwnl9ayrgxkp9s6gqqqqpqqqqqqcqqqqqxyqqqqx7asf60w8pqpte2sfcfn90fdfzxue7ff2g8sawe9wacnqat6jmygqngqqqqpxv9ejjvgz2u63w3l839aadguh5rgtqd4devf97a0fpt4uqsz0k5uehneqlmtc9wqe9mvrj03q4phntqwzd2q9rqgqqqqqqcqupsgr8

3) The Ethereum address used to generate the Deposit Receiver Address (in text format).
0x73379E41FDaf0570325db0727c4150dE6b0384D5

4) A link to the Etherscan explorer for the successful Force Bridge transaction. This can be found on Force Bridge under History→Succeed.\
https://rinkeby.etherscan.io/tx/0x85c6c8c8fae0af3917fff273eb516529b728e23f0b66e77b99ff44a4ca1a1c1f

5) A link to the Nervos explorer for the successful Force bridge transaction. This can be found on Force Bridge under History→Succeed.
https://explorer.nervos.org/aggron/transaction/0xdcc12c12b56f6aa98e0c34ddac31afb64219b7a826e9a7673518584bbf8ce72c



### Use Force Bridge to Deposit Tokens From Ethereum to Polyjuice

Moving assets between blockchains is an extremely important part of building the cross-chain dApps of the future. Not only do developers need secure infrastructure to build on, but the experience for the end user must be simple and straightforward.

Nervos' solutions to cross-chain interoperability are major steps towards these goals. At the base of this is Force Bridge, the decentralized cross-chain bridge which enables the transfer of assets between Nervos and other blockchains. You can learn more about the way a user from another blockchain will interact with Nervos in this document about the Common User Action Flow.

Force Bridge is currently in the late testing phase, and supports moving tokens to and from the Ethereum Rinkeby testnet. The Cardano bridge has also been announced and is in the late stages of development. More networks will continue to be added, continuously growing the available audience for any developers building on Nervos today.
Task Instructions

    Note: Before starting the tasks, it is recommended that you review the Task Submission section so you know what materials you will need to provide to judges to review your task submission.

In this task you will use Force Bridge to transfer ETH from the Ethereum Rinkeby testnet to ckETH on Nervos Layer 2. ETH is a native asset on Ethereum, and it is represented as a wrapped token on Nervos using ckETH SUDT tokens. The ckETH SUDT token is a native asset on Nervos, and it can be used both on Layer 1 and Layer 2, and is widely supported by all tooling within the Nervos ecosystem.

To do this, you will use MetaMask and Force Bridge to transfer ETH from the Rinkeby testnet directly to Nervos' Layer 2. Under the hood, the assets will flow from Ethereum to Force Bridge to Nervos Layer 1 to Nervos Layer 2, but from the end-user perspective this will all be done in a single step.
Prerequisites

This task requires the Gitcoin Task Instruction Examples repo (gw-gitcoin-instruction) which was setup in task 2. If you do not have this repo available for any reason, please set it up now.
1. Configure MetaMask to Use the Rinkeby Testnet

Open MetaMask and select the Ethereum account you want to use for the Force Bridge transfer. This should be the same Ethereum account you are using for Layer 2 on Nervos. Then select the "Rinkeby Test Network" from the Network dropdown.

You will need to get some Testnet ETH from one of the Rinkeby faucets. You can use either the Rinkeby Authenticated Faucet or the Rinkeby Ether Faucet to get a small amount of testnet funds.
2. Calculate Your Layer 2 Deposit Receiver Address

Nervos' unique architecture allows a single account to have multiple addresses to be created for different purposes. We will be using one of these addresses to streamline the process of moving tokens to Layer 2.

The process flow we mentioned earlier of Ethereum to Force Bridge to Nervos Layer 1 to Nervos Layer 2 is still going on, but the steps can be consolidated to a single action by the end user. We will walk through the steps of the developer process, which starts with calculating the Layer 2 deposit receiver address for the user.

Open the example code from gw-gitcoin-instruction/src/examples/6-bridge/index.js in an editor of your choosing.

Replace <YOUR_ETHEREUM_ADDRESS> with the Ethereum address that you wish to receive your Layer 2 ckETH tokens.

After all values have been replaced, use the following commands in a console to execute the script.

cd ~/projects/gw-gitcoin-instruction/src/examples/6-bridge
node index.js

You should see console output similar to this:

➜ node index.js 
Using Ethereum address: 0xD173313A51f8fc37BcF67569b463abd89d81844f
Corresponding Polyjuice address: 0xa3cd0b1d997e5281dd574dd34155945febcf73a4

Deposit to Layer 2 address on Layer 1: 
ckt1qs4vva27537dzxxpgle3vq5jjgfd8x2ye3dynmqj7c78z3vmuzve4xexq9s7qquh9s9knxfehstyelw0eelagr4ezdvr2qyd6lsf60dw5yqqqqqsqqqqqvqqqqqfjqqqqp303zade957p346euv9lgwy2zhpj6d0tkdhsgchl8kdnvhantykq6gqqqqpqqqqqqcqqqqqxyqqqq8u7zf6tuwlgqmuagje6jwlqp0quujcknmrueer8md9kdmt0lfzjqqngqqqqzdjvqtpuqpewtqtdxvnn0qkfn7ulnnl6s8tjy6cx5qgm4lqn576a5tnxya9r78ux770vatfk336hkyasxzy7q9rqgqqqqqqcq7pq9ye

The long address at the bottom of the output is your deposit receiver address. This is a Layer 1 address that is used to automatically transfer funds to Layer 2. We will use this with Force Bridge in the next step.
3. Initiate a Force Bridge Transfer

Open the Force Bridge Testnet in a web browser. Make sure you have Rinkeby network selected in MetaMask, and that your selected account has Rinkeby ETH.

You will be transferring from Ethereum to Nervos, and you will be transferring ETH to ckETH. Make sure these values are selected as seen in the screenshots below, if they are not already selected.
 

After you have selected the assets to transfer across the bridge, you can specify the amount in the top box. There will be a small fee for the transfer, and this will be calculated automatically.

In the box marked "Recipient", you will specify the Nervos destination address for the funds. Input the deposit receiver address that was generated in the previous step.

When you have finished inputting and reviewing your selections, click the Bridge button. You will be asked to sign the transaction using MetaMask as seen below.

When you confirm the signing of the transaction in the MetaMask you will get a modal with a link to the Etherscan explorer, where you can optionally view the progress of mining your transaction on the Ethereum chain.

You will also see the transaction at the bottom of the page in the History section of the UI under the Pending tab. It will first be in a "lock asset on Ethereum (x/15)" state, where X is the number of block confirmations on the Ethereum chain.

When there is at least 15 block confirmations your pending transaction will transition to "lock asset on Ethereum (confirmed)" state.

After all the required confirmations are received, the first part of the transfer is complete. The funds have now been received by Force Bridge, and the second part of the transfer is to send the SUDT tokens on Nervos' Layer 1. Once this transaction has been submitted, the History status will move from the "Pending" to the "Succeed" tab.

At this point the SUDT tokens reside on Layer 1, and are awaiting collection by a Layer 2 validator node. Once they are picked up by a validator node, the SUDT tokens will released on Layer 2 to the user's Ethereum account. This process is automatic, but it can take up to 10 minutes under normal conditions.


