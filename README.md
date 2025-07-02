
```
sudo apt-get update && sudo apt-get upgrade -y
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt update && sudo apt install -y nodejs
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen ufw -y
```
```
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update && sudo apt install -y docker-ce && sudo systemctl enable --now docker
sudo usermod -aG docker $USER && newgrp docker
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose
```
```
sudo ufw allow 40400/tcp 
sudo ufw allow 40400/udp
sudo ufw enable
sudo ufw status
sudo ufw allow 22
sudo ufw allow ssh
sudo ufw enable
sudo ufw allow 40400
sudo ufw allow 8080
sudo ufw reload
```
# Install the Aztec CLI

```
bash -i <(curl -s https://install.aztec.network)
```
* Set the correct version for the testnet
```
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
screen -S aztec
```
# Load your wallet with Sepolia Faucet 

  🔺🔺--- Execute below given command to Start Your node & Dont forget to make changes in it-

```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls http://38.143.58.54:8545 \
  --l1-consensus-host-urls http://38.143.58.54:3500 \
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  --sequencer.coinbase YourAddress \
  --p2p.p2pIp Your_ip
```

 ------👇Save These Info/Data👇 ------

Aztec Sequencer Node ( XXXXX dc)
```
• Ethereum sepolia rpc : 

• Beacon_sepolia_RPC : 

• PVT KEY : 

• MM Public Address : 

• IP ( cloud vps) : 

• Block Number : 

• Base64 encoded string : 
```
------ 👆Save These Info/Data👆 ------

