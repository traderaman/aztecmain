
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
```
# Load your wallet with Sepolia Faucet 

  🔺🔺--- Execute below given command to Start Your node & Dont forget to make changes in it-

```
#!/bin/bash

LOG_DIR="$HOME/aztec_node_logs"
LOG_FILE="$LOG_DIR/aztec_sequencer_$(date +%Y%m%d).log"

mkdir -p "$LOG_DIR"

echo "--- Aztec Node Auto-Restart Script ---" | tee -a "$LOG_FILE"
echo "Log file for today: $LOG_FILE" | tee -a "$LOG_FILE"
echo "------------------------------------" | tee -a "$LOG_FILE"

if [ -z "$AZTEC_PRIVATE_KEY" ]; then
    read -p "Enter your private key (ofc this will not store anywhere): " AZTEC_PRIVATE_KEY
    if [ -z "$AZTEC_PRIVATE_KEY" ]; then echo "Private Key cannot be empty. Exiting."; exit 1; fi
fi

if [ -z "$AZTEC_COINBASE" ]; then
    read -p "Enter your address: " AZTEC_COINBASE
    if [ -z "$AZTEC_COINBASE" ]; then echo "Coinbase Address cannot be empty. Exiting."; exit 1; fi
fi

if [ -z "$L1_RPC_URLS" ]; then
    read -p "Enter your sepolia rpc url: " L1_RPC_URLS
    if [ -z "$L1_RPC_URLS" ]; then echo "L1 RPC URL cannot be empty. Exiting."; exit 1; fi
fi

if [ -z "$L1_CONSENSUS_URLS" ]; then
    read -p "Enter your beacon rpc url: " L1_CONSENSUS_URLS
    if [ -z "$L1_CONSENSUS_URLS" ]; then echo "L1 Consensus URL cannot be empty. Exiting."; exit 1; fi
fi

if [ -z "$P2P_PUBLIC_IP" ]; then
    read -p "Enter your vps ip address: " P2P_PUBLIC_IP
    if [ -z "$P2P_PUBLIC_IP" ]; then echo "Public IP cannot be empty. Exiting."; exit 1; fi
fi

if [ -z "$AZTEC_API_PORT" ]; then
    AZTEC_API_PORT="8080"
    echo "Using default Aztec API Port: $AZTEC_API_PORT" | tee -a "$LOG_FILE"
fi

AZTEC_MAX_TX_POOL_SIZE="1000000000"

echo "--- Node Details Confirmed ---" | tee -a "$LOG_FILE"
echo "Private Key: ${AZTEC_PRIVATE_KEY:0:6}...${AZTEC_PRIVATE_KEY: -4}" | tee -a "$LOG_FILE"
echo "Coinbase: ${AZTEC_COINBASE:0:6}...${AZTEC_COINBASE: -4}" | tee -a "$LOG_FILE"
echo "L1 RPC URL: $L1_RPC_URLS" | tee -a "$LOG_FILE"
echo "L1 Consensus URL: $L1_CONSENSUS_URLS" | tee -a "$LOG_FILE"
echo "P2P Public IP: $P2P_PUBLIC_IP" | tee -a "$LOG_FILE"
echo "Aztec API Port: $AZTEC_API_PORT" | tee -a "$LOG_FILE"
echo "P2P Max Tx Pool Size: $AZTEC_MAX_TX_POOL_SIZE" | tee -a "$LOG_FILE" # Display the new setting
echo "------------------------------" | tee -a "$LOG_FILE"

while true; do
    echo "Attempting to start node at $(date)..." | tee -a "$LOG_FILE"

    aztec start \
        --node \
        --archiver \
        --sequencer \
        --network alpha-testnet \
        --l1-rpc-urls "$L1_RPC_URLS" \
        --l1-consensus-host-urls "$L1_CONSENSUS_URLS" \
        --sequencer.validatorPrivateKey "$AZTEC_PRIVATE_KEY" \
        --sequencer.coinbase "$AZTEC_COINBASE" \
        --p2p.p2pIp "$P2P_PUBLIC_IP" \
        --port "$AZTEC_API_PORT" \
        --p2p.maxTxPoolSize "$AZTEC_MAX_TX_POOL_SIZE" \
        >> "$LOG_FILE" 2>&1

    echo "Aztec node exited at $(date). Restarting in 5 seconds..." | tee -a "$LOG_FILE"
    sleep 5
done
```

LOGS:
```
tail -f $(ls -t $HOME/aztec_node_logs/aztec_sequencer_*.log | head -1)
```

