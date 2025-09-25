# Mawari Guardian Node Setup Guide (Testnet)

This guide provides a detailed, step-by-step walkthrough for setting up a Mawari Guardian Node on the testnet. It is designed for beginners with minimal command-line experience.

---

## Table of Contents
1.  [**Prerequisites**](#prerequisites)
    -   [Hardware Requirements](#hardware-requirements)
    -   [Server Preparation](#server-preparation)
2.  [**Installation**](#installation)
    -   [Step 1: Install Docker](#step-1-install-docker)
    -   [Step 2: Install the Mawari Guardian Node CLI](#step-2-install-the-mawari-guardian-node-cli)
3.  [**Configuration and Launch**](#configuration-and-launch)
    -   [Step 3: Create a New Account](#step-3-create-a-new-account)
    -   [Step 4: Start the Node](#step-4-start-the-node)
4.  [**Managing Your Node**](#managing-your-node)
    -   [Check Status](#check-status)
    -   [View Logs](#view-logs)
    -   [Stop the Node](#stop-the-node)
    -   [Update the Node](#update-the-node)

---

## Prerequisites

Before we begin, we need to ensure your server environment is ready.

### Hardware Requirements

You will need a Virtual Private Server (VPS) with the following minimum specifications:

-   **CPU:** 4 Cores
-   **RAM:** 8 GB
-   **Storage:** 100 GB (SSD is highly recommended for better performance)
-   **Operating System:** **Ubuntu 22.04 LTS** (This guide is based on this version)

*(You can rent a suitable VPS from providers like Vultr, DigitalOcean, Hetzner, or Contabo.)*

### Server Preparation

First, connect to your fresh Ubuntu 22.04 server via SSH. Then, run the following command to update all system packages to their latest versions.

```bash
# This command updates the package list and then upgrades all installed packages.
# The -y flag automatically confirms any prompts.
sudo apt update && sudo apt upgrade -y
```

---

## Installation

With the server prepared, let's install the necessary software.

### Step 1: Install Docker

The Mawari Guardian Node runs inside Docker containers. We'll use the official script to install it easily.

```bash
# Download the official Docker installation script.
curl -fsSL https://get.docker.com -o get-docker.sh

# Run the script with sudo privileges to install Docker.
sudo sh get-docker.sh
```

Next, add your current user to the `docker` group. This allows you to run Docker commands without needing to type `sudo` every time.

```bash
# Add the current user ($USER) to the 'docker' group.
sudo usermod -aG docker $USER
```

**IMPORTANT:** For this change to take effect, you must **log out of your server and log back in**.

### Step 2: Install the Mawari Guardian Node CLI

The CLI (Command-Line Interface) is the tool you'll use to control your node. Install it with this single command:

```bash
# This command downloads and executes the official installation script from Mawari's GitHub repository.
bash -c "$(curl -fsSL [https://raw.githubusercontent.com/mawari/guardian-node-cli/main/install.sh](https://raw.githubusercontent.com/mawari/guardian-node-cli/main/install.sh))"
```

A successful installation will greet you with a welcome message.

---

## Configuration and Launch

Now it's time to create an identity for your node and get it running.

### Step 3: Create a New Account

Your node needs a wallet account to be identified on the network and to receive rewards.

```bash
mawari-node-cli create-account
```

After running the command, your terminal will display:
1.  **Public Address:** Your wallet's address, used for receiving funds.
2.  **Private Key:** The secret key to access your wallet.
3.  **Mnemonic Phrase:** A 12 or 24-word phrase to recover your wallet.

> 🚨 **SECURITY WARNING** 🚨
>
> - **NEVER SHARE** your **Private Key** or **Mnemonic Phrase** with anyone.
> - **WRITE THEM DOWN AND STORE THEM SECURELY OFFLINE** (e.g., on a piece of paper in a safe).
> - If you lose these, you will permanently lose access to your wallet and any rewards it contains.

### Step 4: Start the Node

Everything is now set up. Start your node with this simple command:

```bash
mawari-node-cli start
```

This command will download the required Docker images and start the containers. The first launch may take a few minutes as your node begins to sync with the Mawari network.

---

## Managing Your Node

Here are the essential commands for managing your running node.

### Check Status

To check if your node is online and operating correctly:

```bash
mawari-node-cli status
```

### View Logs

To troubleshoot issues or see detailed activity:

```bash
mawari-node-cli logs
```

### Stop the Node

To stop the node for maintenance or other reasons:

```bash
mawari-node-cli stop
```

### Update the Node

To update your node to the latest version released by the Mawari team:

```bash
mawari-node-cli update
```

---

## Congratulations! 🎉

You have successfully installed and launched a Mawari Guardian Node on the testnet. Welcome to the network!
````
