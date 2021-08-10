## Gitcoin: 0) Setup a Local CKB Node and CKB Indexer for the Testnet

#### Screen Node of the Local ckb Node and ckb indexer

![setup-node-ckb](./local-ckb-node-and-ckb-indexer.png)



Description

0. Setup a Local CKB Node and CKB Indexer for the Testnet

Before diving into the more complicated tasks, you need to setup a CKB Node and a CKB Indexer. These two pieces of node software work together to support the needs of dApps. The scripts we will use later on will interact with the Nervos Testnet and rely on these nodes for information about the state of the network.

You can run nodes locally, or you can use public nodes. The Nervos Foundation hosts public Testnet nodes for use with the Gitcoin tasks, and you will find their URLs at the bottom of this page. However, running a local node is recommended since synchronization with the public nodes is a much slower process that using one locally.

When setting up a node, you are given the option of using the Mainnet, the Testnet, or a Devnet. We will be using the Testnet since this is the test environment that will require the least amount of setup.

The Nervos Testnet, also known as "Aggron", is the public facing test environment for Nervos Network. This is a shared test environment which contains the new infrastructure that is not yet available on the Mainnet. The tokens and assets on the Testnet have no value, so you can safely test here without worrying about any lost funds.
Setup and Requirements

Before starting, you will need to setup your development environment. If you have not completed the instructions on the Task Setup and Requirements page, please do so now.
Task Instructions

    Note: Before starting the tasks, it is recommended that you review the Task Submission section so you know what materials you will need to provide to judges to review your task submission.

In this task you will setup a local CKB Node and a local CKB Indexer for use with the Aggron Testnet. The general process is as follows:

    Setup a local CKB Node, configure it for the Testnet, and allow it to fully synchronize with the network.
    Setup a local CKB Indexer, and allow it to fully synchronize with the local CKB Node.

    Note: You will need approximately 20GB of disk space and a minimum of 2 CPU cores in order to setup the nodes. If you are unable to meet these requirements, you can still participate on other tasks using public nodes, but you will not receive credit for completing this task.

Project Folder

Some of our later instructions will install files into the projects directory within the user's home folder. Creating the projects directory is optional, but it may be helpful for organization since we will be installing more tools later.

mkdir -p ~/projects
cd ~/projects

1. Setup a CKB Node

To setup a Testnet CKB Node, follow the steps below. Once the node has started, it will take 5+ hours to fully synchronize with the network, but you can speed up the process by using a Bootstrap for a CKB Node from CKB.tools.

First, download the version 0.43.1 binary from the CKB Node Releases page, or use the commands below to install.

Commands for Linux:

cd ~/projects
curl -LO https://github.com/nervosnetwork/ckb/releases/download/v0.43.1/ckb_v0.43.1_x86_64-unknown-linux-gnu.tar.gz
tar xzf ckb_v0.43.1_x86_64-unknown-linux-gnu.tar.gz
mv ckb_v0.43.1_x86_64-unknown-linux-gnu ckb_v0.43.1

Commands for MacOS:

cd ~/projects
curl -LO https://github.com/nervosnetwork/ckb/releases/download/v0.43.1/ckb_v0.43.1_x86_64-apple-darwin.zip
unzip ckb_v0.43.1_x86_64-apple-darwin.zip
mv ckb_v0.43.1_x86_64-apple-darwin ckb_v0.43.1

Then initialize the blockchain to the Aggron Testnet:

cd ~/projects/ckb_v0.43.1
./ckb init --chain testnet

If you want to start the node and download the blockchain starting from the genesis block, use the command below to start the node. If you want to use the bootstrap to speed things up, you can skip starting it now and continue going through the bootstrap instructions.

cd ~/projects/ckb_v0.43.1
./ckb run

Basic instructions for the bootstrap are available on CKB.tools, but you can also use this convenience script below to automate the process. This will download the snapshot data, and then decompress it to the appropriate folder. If ckb is currently running, stop it with ctrl+c, then execute the following commands.

cd ~/projects/ckb_v0.43.1 # Your folder name may be different.
curl -sSf https://raw.githubusercontent.com/Kuzirashi/gw-gitcoin-instruction/master/scripts/install_ckb_node_snapshot_data.sh | sh

After the bootstrap has downloaded and decompressed, you can start the node with the following command.

cd ~/projects/ckb_v0.43.1
./ckb run

2. Setup a CKB Indexer

To setup a Testnet CKB Indexer, follow the steps below. Once the node has started, it can take several hours to fully synchronize with the CKB Node, but you can also speed up this process by using a Bootstrap for a CKB Indexer from CKB.tools.

First, download the version 0.2.1 binary from the CKB Indexer Releases page, or use the commands below to install.

Commands for Linux:

mkdir -p ~/projects/ckb-indexer-0.2.1/
cd ~/projects/ckb-indexer-0.2.1
curl -LO https://github.com/nervosnetwork/ckb-indexer/releases/download/v0.2.1/ckb-indexer-0.2.1-linux.zip
unzip ckb-indexer-0.2.1-linux.zip
tar xzf ckb-indexer-linux-x86_64.tar.gz

Commands for MacOS:

mkdir -p ~/projects/ckb-indexer/
cd ~/projects/ckb-indexer
curl -LO https://github.com/nervosnetwork/ckb-indexer/releases/download/v0.2.1/ckb-indexer-0.2.1-macos.zip
unzip ckb-indexer-0.2.1-macos.zip
unzip ckb-indexer-mac-x86_64.zip

Then start the CKB Indexer:

RUST_LOG=info ./ckb-indexer -s ./indexer-data

    Note: The CKB Indexer requires the CKB Node to be running before it can begin synchronizing.

Basic instructions for the bootstrap are available on CKB.tools, but you can also use this convenience script below to automate the process. This will download the snapshot data, and then decompress it to the appropriate folder. If ckb-indexer is currently running, stop it with ctrl+c, then execute the following commands.

cd ~/projects/ckb-indexer-0.2.1 # Your folder name may be different.
curl -sSf https://raw.githubusercontent.com/Kuzirashi/gw-gitcoin-instruction/master/scripts/install_ckb_indexer_snapshot_data.sh | sh

Local Testnet Node URLs

Once your local Testnet nodes are running and synchronized, they can be accessed using the following URLs:

    Local CKB Node RPC URL: http://localhost:8114
    Local CKB Indexer RPC URL: http://localhost:8116

Public Testnet Node URLs

The Nervos Foundation hosts public nodes for the Testnet, which are available for use with the Gitcoin tasks. However, running a local node is recommended since synchronization with the public nodes is a much slower process that using one locally.

These public nodes are made available if you are unable to setup nodes for any reason. If you do not to setup a node you will not get credit for this task, but you can still continue with the other tasks.

    CKB Node RPC URL: http://3.235.223.161:18114
    CKB Indexer RPC URL: http://3.235.223.161:18116
