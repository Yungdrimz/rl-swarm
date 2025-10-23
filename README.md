# Run RL Swarm (Testnet) Node ON 16GB RAM VPS
<p align="center">
<img src="https://github.com/user-attachments/assets/08fa2ef7-2e68-4860-8c0b-1aeb437dde32" alt="Demo" width="90%" height="200" />
</p>

RL Swarm is a fully open-source framework developed by GensynAI for building reinforcement learning (RL) training swarms over the internet. This guide walks you through setting up an RL Swarm node and a web UI dashboard to monitor swarm activity.

## Hardware Requirements
Currently in the new recent update, Gensyn testnet is running and training the [reasoning-gym](https://github.com/open-thought/reasoning-gym/tree/main) swarm datasets on the Testnet. This swarm is supporting the current list of default models:
* Gensyn/Qwen2.5-0.5B-Instruct
* Qwen/Qwen3-0.6B
* nvidia/AceInstruct-1.5B
* dnotitia/Smoothie-Qwen3-1.7B
* Gensyn/Qwen2.5-1.5B-Instruct

Your hardware requirements will vary depending on model you choose. Since this guide is for CPU users with 16GB RAM, the model I will be using is:
* Qwen/Qwen3-0.6B

## Step 1) Install Dependencies

**1. Update System Packages**
```bash
sudo apt update && sudo apt upgrade -y
```
**2. Install General Utilities and Tools**
```bash
sudo apt install screen curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

**3. Install Python**
```bash
sudo apt install python3 python3-pip python3-venv python3-dev -y
```

**4. Install Node**
```
sudo apt update
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo bash -
sudo apt install -y nodejs
node -v
npm install -g yarn
yarn -v
```

**5. Install Yarn**
```bash
curl -o- -L https://yarnpkg.com/install.sh | bash
```
```bash
export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH"
```
```bash
source ~/.bashrc
```

---

## Step 2) Get HuggingFace Access token
**1- Create account in [HuggingFace](https://huggingface.co/)**

**2- Create an Access Token with `Write` permissions [here](https://huggingface.co/settings/tokens) and save it**

---

## Step 3) Clone the Repository
```bash
git clone https://github.com/Yungdrimz/rl-swarm
```

---

## Step 4) Run the swarm
If you are an **existing user**, you must have your node's `swarm.pem` present in `rl-swarm` directory before starting the node.

**1. Create a screen session**
```bash
screen -S gensyn
```

**2. Get into the `rl-swarm` directory**
```
cd rl-swarm
```

**3. Create & Activate a Virtual Environment**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**4. Start the swarm Node**
```
./run_rl_swarm.sh
```
## Step 5) Login
**1- You have to receive `Waiting for userData.json to be created...` in logs**

![image](https://github.com/user-attachments/assets/140f7d32-844f-4cf0-aac4-a91e9a14c1aa)

**2- Open login page in browser**
* **Local PC:** Open `http://localhost:3000/` in your browser
* **VPS Users: Tunnel to external URL:**
  * 1- Open a new terminal
  * 2- Install **localtunnel**:
    ```
    sudo npm install -g localtunnel
    ```
  * 3- Get a password:
    ```
    curl https://loca.lt/mytunnelpassword
    ```
  * The password is actually your VPS IP
  * 4- Get URL
    ```
    lt --port 3000
    ```
  * Visit the prompted url, and enter your password to access Gensyn login page

**3- Login with your preferred method**

![image](https://github.com/user-attachments/assets/f33ea530-b15f-4af7-a317-93acd8618a9f)

* After login, your terminal starts installation.

**4- Answer prompts:**
* `Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N]` >>> Press `N` to join testnet
  * `HuggingFace` needs `2GB` upload bandwidth for each model you train, you can press `Y`, and enter your access-token.
* `Enter the name of the model you want to use in huggingface repo/name format, or press [Enter] to use the default model.` >>> Click enter to select any of the two by default, or copy and paste any of this model below. It works well on a 16GB CPU
  
    ```
    Qwen/Qwen3-0.6B
    ```
    ```
    Gensyn/Qwen2.5‑0.5B‑Instruct
    ```

---

## 5) Join Judge
During setup, you'll be asked if you'd like to participate in the AI Prediction Market.

Example:
```
Would you like to participate in the AI Prediction Market? (Y/n)
```
* You'll be entered into the prediction market by default, by pressing `ENTER` or answering `Y` to the Prediction Market prompt
* There is a separate leaderboard for Judge in the [gensyn dashboard](https://dashboard.gensyn.ai/)

This is an experiment we're running in which:

RL Swarm models enter the market and bet on the correct answer to a reasoning problem. Evidence is revealed gradually, and models update beliefs by placing new bets as information arrives. Early correct bets yield higher rewards, favoring quick, confident models. The Judge evaluates final evidence and determines successful bets.

---

### Node Name
* Now your node started running, Find your name after word `Hello`, like mine is `[sniffing spotted spider]` as in the image below (You can use `CTRL+SHIFT+F` to search Hello in terminal)


<img width="764" height="231" alt="hello" src="https://github.com/user-attachments/assets/e88e3317-74bf-41e0-a090-f4850c6ed389" />

---
## NOTE
**You need to backup `swarm.pem`, if you want to recover your animal's name, animals are connected to your email**
### `VPS`:
Connect your VPS using `Mobaxterm` client to be able to move files to your local system. Back up these files:
* `/root/rl-swarm/swarm.pem`

### Screen commands
* Minimize: `CTRL` + `A` + `D`
* Return: `screen -r gensyn`
* Stop and Kill: `screen -XS gensyn quit`


---
