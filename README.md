# Mawari Guardian Node Setup Guide (Updated September 2025)

This guide provides a detailed, step-by-step walkthrough for setting up a Mawari Guardian Node on the testnet, based on the latest official documentation. The installation process has been significantly updated.

---

## Table of Contents

- [**Part 1: Wallet and Asset Preparation**](#part-1-wallet-and-asset-preparation)
  - [1.1. Create a Main (Owner) Wallet](#11-create-a-main-owner-wallet)
  - [1.2. Connect and Get Testnet Tokens (Faucet)](#12-connect-and-get-testnet-tokens-faucet)
  - [1.3. Mint Your Guardian NFT](#13-mint-your-guardian-nft)
- [**Part 2: Installing the Guardian Node Client**](#part-2-installing-the-guardian-node-client)
  - [2.1. Install Docker](#21-install-docker)
  - [2.2. Run the Guardian Node](#22-run-the-guardian-node)
  - [2.3. Fund the Burner Wallet](#23-fund-the-burner-wallet)
- [**Part 3: Activating the Node (Delegation)**](#part-3-activating-the-node-delegation)

---

## Part 1: Wallet and Asset Preparation

This stage involves setting up your identity and initial assets on the test network.

### 1.1. Create a Main (Owner) Wallet

If you don't already have an EVM-compatible wallet, you'll need to create one. MetaMask is a great option.

1.  Install the MetaMask browser extension from [metamask.io](https://metamask.io).
2.  Follow the on-screen instructions to create a new wallet.

> 🚨 **CRITICAL SECURITY WARNING** 🚨
>
> Write down your **Mnemonic Phrase (Seed Phrase)** and **Private Key**. Store them in a secure, offline location. Never share them with anyone. This is your main wallet for holding your assets.

### 1.2. Connect and Get Testnet Tokens (Faucet)

1.  Go to the [Mawari Network TestNet Page](https://testnet.mawari.net/).
2.  Click the **"Connect Wallet"** button at the top and connect your new MetaMask wallet. Your browser will prompt you to add and switch to the "Mawari Network TestNet". Approve it.
3.  Once connected, copy your wallet address.
4.  Navigate to the **Faucet page**: [https://hub.testnet.mawari.net](https://hub.testnet.mawari.net).
5.  Paste your wallet address into the Faucet field and click "Request".

> 💡 **Tip:** You can request up to 2 tokens. It is highly recommended to **request 2 tokens** now to simplify later steps.

### 1.3. Mint Your Guardian NFT

1.  Return to the [Mawari Network TestNet Page](https://testnet.mawari.net/).
2.  In "Step 2" on the page, click the button to **Mint** a Guardian NFT. You will need to approve the transaction in your MetaMask wallet.

You now have the required tokens and NFT in your Owner Wallet to proceed.

---

## Part 2: Installing the Guardian Node Client

Now, we will install the node software on your server (VPS).

### 2.1. Install Docker

Ensure Docker is installed on your server. If not, you can run the following commands on Ubuntu:
```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
# Add your user to the docker group to run commands without sudo
sudo usermodel -aG docker $USER
```
> ❗ **Important:** You must **log out and log back into your server** after running the `usermodel` command for the changes to take effect.

### 2.2. Run the Guardian Node

This new process runs the node directly via Docker.

1.  **Set the Owner Address Variable**
    Open your server's terminal and run the following command, replacing `0x123abc...` with your **main (Owner) wallet address**:
    ```bash
    export OWNER_ADDRESS=0x123abc...
    ```

2.  **Launch the Docker Container**
    Execute the command below. It will create a `~/mawari` directory, pull the latest node image, and start the container.
    ```bash
    export MNTESTNET_IMAGE=us-east4-docker.pkg.dev/mawarinetwork-dev/mwr-net-d-car-uses4-public-docker-registry-e62e/mawari-node:latest && mkdir -p ~/mawari && docker run -d --pull always -v ~/mawari:/app/cache -e OWNERS_ALLOWLIST=$OWNER_ADDRESS $MNTESTNET_IMAGE
    ```

3.  **Find Your Burner (Operator) Wallet Address**
    The terminal will now display node logs. Look carefully for a line that looks like this:
    `[INFO] Using burner wallet {"address": "0x..."}`
    The `0x...` address is your node's unique **Burner/Operator Wallet Address**. Copy this address and save it—you'll need it for the next steps.

### 2.3. Fund the Burner Wallet

The burner wallet needs MAWARI tokens to pay for on-chain transaction fees.

1.  Open your MetaMask wallet (your main Owner Wallet).
2.  Initiate a **"Send"** transaction.
3.  Send exactly **1 MAWARI token** to the **Burner Wallet Address** you found in the logs.
4.  Check log: show CONTAINER ID ```docker ps -a``` check log: `docker logs -f CONTAINER ID`

---

## Part 3: Activating the Node (Delegation)

The final step is to link the NFT in your main wallet to your running node.

1.  Go to the [Mawari Guardian Dashboard](https://app.testnet.mawari.net/).
2.  Connect your main **Owner Wallet**.
3.  You will see the Guardian NFT(s) you minted earlier.
4.  Select the NFT(s) you wish to delegate to your node.
5.  Click the **"Delegate"** button.
6.  A field will appear. Paste your **Burner/Operator Wallet Address** into this field.
7.  Click **"Delegate"** again and approve the transaction in your MetaMask wallet.

Once the transaction is confirmed, your node will automatically detect the delegation and become fully active. You can monitor the logs in your server's terminal for confirmation messages, and the status on the Guardian Dashboard will update to reflect that your node is running.

Congratulations, your Guardian Node is now correctly set up and running on the Mawari Testnet!
