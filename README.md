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

## 🟩 Install Node.js

### For **Linux/WSL**:

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt update && sudo apt install -y nodejs
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
---

## 🧬 Clone RL-Swarm Repository

```bash
git clone https://github.com/gensyn-ai/rl-swarm.git
```

---

## 🖥️ (Optional) Create a Screen Session (for VPS)

```bash
screen -S gensyn
```

---

## 📂 Navigate to RL-Swarm Directory

```bash
cd rl-swarm
```

---

## 🏗️ Create & Activate Python Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```
---

## 🚦 Run the Swarm Node

```bash
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




### **Note**

- If you see `0x0000000000000000000000000000000000000000` in the Connected EOA Address section, your contribution is not being recorded.  
  **Delete the existing `swarm.pem` file and start again with a new email.**

---

## 🤖 Need Help

 📺 **Guides & Updates:** [@LEGENDARYLOOTERSSS](https://t.me/LEGENDARYLOOTERSSS)

 If U have any issue then open a issue on this repo or Dm me on Telegram~

Thank You! Happy Coding!📈
```
