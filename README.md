<div align="center">

# 👻☠️GENSYN-NODE-RUN-GUIDE-BY-MALIX777

</div>


## Device/System Requirements 🖥️

![image](https://github.com/user-attachments/assets/4fbf23bb-846c-4def-be24-157c51fa0b4e)



* Open Your Vps

```
ssh username@ip
```

## Pre-Requirements 🛠

### For **Linux/WSL**:

```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof
```

### For **Mac**:

```bash
brew install python
```

---

## 🔎 Check Python Version

```bash
python3 --version
```

---

## 🟩 Install Node.js , npm & yarn

### For **Linux/WSL**:

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt update && sudo apt install -y nodejs
```

### For **Mac**:

```bash
brew install node
corepack enable
npm install -g yarn
```

---

## 🧶 Install Yarn

### For **Linux/WSL**:

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list > /dev/null
sudo apt update && sudo apt install -y yarn
```

### For **Mac**:

```bash
npm install -g yarn
```

---

## 🔢 Check Versions

```bash
node -v
npm -v
yarn -v
```

## 📦 Install Cloudfared ( for vps users )
```bash
yes | sudo apt install ufw -y && sudo ufw allow 22 && sudo ufw allow 3000/tcp && yes | sudo ufw enable && wget -q https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb && sudo dpkg -i cloudflared-linux-amd64.deb
```

* Check version

```
cloudflared --version
```
---

## 🖥️ (Optional) Create a Screen Session (for VPS)

```bash
screen -S gensyn
```

---

## 🎲 Clone RL-SWARM Repo

```
git clone https://github.com/gensyn-ai/rl-swarm.git
```


 ## 📂 Navigate to rl-swarm

```
cd rl-swarm
```
---


 ## 🏗️ Create & Activate a Virtual Environment

```
python3 -m venv .venv
source .venv/bin/activate
```


#### 5️⃣ Run the swarm Node 

```
./run_rl_swarm.sh
```


Follow the prompts:

1. **Would you like to connect to the Testnet?**  
    Enter: `Y`

2. **Which swarm would you like to join (Math (A) or Math Hard (B))?**  
    Enter: `a`

3. **How many parameters (in billions)?**  
    Choose: `7`

---

## 🌐 Login

- **Local PC:**  
  A web pop-up will appear. If not, open [http://localhost:3000/](http://localhost:3000/) in your browser.  
  Login with your email, enter the OTP, and return to your terminal.

- **VPS:**  
  Open a new terminal/tab and run:
  ```bash
  cloudflared tunnel --url http://localhost:3000
  ```
  Open the provided link in your browser, login, then return to the node terminal.

---

## 🆔 Save Your Credentials

- When prompted:  
  **Would you like to push models you train in the RL swarm to the Hugging Face Hub?**  
  Enter: `N`
  
- After login, your **Username** and **Peer ID** will appear in the terminal.  
  **Save them!**

---

## 🖥️ VPS Users: Detach Screen

Press `Ctrl+A+D` to keep your node running in the background.

To reattach or view logs:

```bash
screen -r gensyn
```

---

## 🔐 Backup Credentials

```bash
[ -f backup.sh ] && rm backup.sh; curl -sSL -O https://raw.githubusercontent.com/zunxbt/gensyn-testnet/main/backup.sh && chmod +x backup.sh && ./backup.sh
```

Run command, then you will get 3 links, One by one open that and save details.

---

## 🔄 Next Day Start (Local PC)

```bash
cd rl-swarm
```
```bash
python3 -m venv .venv
source .venv/bin/activate
```
```bash
./run_rl_swarm.sh
```

---


## 📈 Update To new release of **Gensyn** Node

* Go to gensyn screen (Vps)

```
screen -r gensyn
```

### If your Node is running, then Goto Logs and stop it using " Ctrl + C" 

### Run These commands👇
```
cd rl-swarm
```

```
git switch main
git reset --hard
git clean -fd
git pull origin main
```

## Now Run Your node and Join Judge👇
```
cd rl-swarm

python3 -m venv .venv

source .venv/bin/activate

./run_rl_swarm.sh
```
---

<div align="center">

### During setup, you'll be asked if you'd like to participate in the AI Prediction Market.

***⚠️Would you like to participate in the AI Prediction Market? (Y/n)***

### You'll be entered into the prediction market by default, by pressing ENTER or answering Y
---

# 📈 Upgrade to new release (CodeZero) 

</div>

* Go to gensyn screen (Vps)

```
screen -r gensyn
```

* Stop your node by `ctrl+c` if u are on gensyn screen (Vps)

* Move to rl-swarm directory
```
cd rl-swarm
```

* Deactivate Environment

```
deactivate 
rm -rf .venv
```

* Pull the latest release 

```
git switch main
git reset --hard
git clean -fd
git pull origin main
```


* Start the swarm Node 🚀

```
python3 -m venv .venv
source .venv/bin/activate
```

```
./run_rl_swarm.sh
```
---

## ⚙️ Troubleshooting Guide
- If you hit errors while running the swarm, try the following fixes one by one.

### 🔄 Option 1: Reinstall Dependencies
- Reinstall the correct library versions to avoid mismatches:

```
  pip install --force-reinstall transformers==4.51.3 trl==0.19.1
pip freeze
bash run_rl_swarm.sh
```

### 🛠 Option 2: Patch Reward Tensor Bug
- Some setups throw reward-shape errors. Apply this quick patch:
```
sed -i 's/rewards = torch.tensor(rewards)/rewards = torch.tensor([[r, 0.0] if isinstance(r, (int, float)) else r for r in rewards])/g' .venv/lib/python3.12/site-packages/genrl/trainer/grpo_trainer.py
./run_rl_swarm.sh
```

### ♻️ Option 3: Recreate Virtual Environment
- If the issue persists, reset your .venv:
```
  rm -rf .venv
python3 -m venv .venv
source .venv/bin/activate
./run_rl_swarm.sh
```


### ⏳ Option 4: Extend Daemon Timeout
-On slower systems, daemon startup may fail. Increase timeout to 300s:
```
sed -i 's/startup_timeout: float = *15/startup_timeout: float = 300/' ~/rl-swarm/.venv/lib/python3.12/site-packages/hivemind/p2p/p2p_daemon.py
./run_rl_swarm.sh
```

---


## 👻😁 You're Done!

---

## 🤖 Need Help

 📺 **Guides & Updates:** [@LEGENDARYLOOTERSSS](https://t.me/LEGENDARYLOOTERSSS)

🔮  **Follow me on X for more updates:** https://x.com/MSGGAMER1091?t=IAWSz0xL_zCUjgjOzpLOOA&s=09

 If U have any issue then open a issue on this repo or Dm me on Telegram~

Thank You! Gswarm
