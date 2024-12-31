# 🛠️ Cysic Verifier Node Guide  

Welcome to the **Cysic Verifier Node Guide**! This document outlines the steps and requirements for setting up and operating the Cysic Verifier Node program. Follow these instructions carefully to ensure a smooth installation and operation.

---

## 💻 Recommended Hardware Requirements  

To ensure optimal performance of the Cysic Verifier Node program, your device should meet the following minimum specifications:  

- **CPU**: Single Core  
- **Memory**: 8 GB  
- **Disk Space**: 512 MB  
- **Bandwidth**: 100 KB/s upload/download  
- **Supported Operating Systems**: Windows, Linux, Mac  

---

## ⚙️ Installation Steps  

### Step 1: Update Your System  

Run the following command to update your system and install the necessary dependencies:  

```bash
sudo apt-get update -y && sudo apt-get upgrade -y && sudo apt-get install make screen build-essential unzip lz4 gcc git jq -y
```
---

## 🛠 Step 2: Download and Run the Setup Script

Use the command below to download and execute the setup script. Replace `0x-Fill-in-your-reward-address-here` with your actual reward address (EVM wallet address).

```bash
curl -L https://github.com/cysic-labs/phase2_libs/releases/download/v1.0.0/setup_linux.sh > ~/setup_linux.sh && bash ~/setup_linux.sh <EVM-WALLET>
```
---

## Step 3: Start the Verifier Program

After completing Step 2, start the verifier program with the following commands:

```bash
cd ~/cysic-verifier/ && bash start.sh
```
Wait until you see the message "sync data from server", then press CTRL+C to stop the process.

## 🌀 Step 4: Configure the Systemd Service

To create and configure a `systemd` service for the verifier, run the following command:

```bash
sudo tee /etc/systemd/system/cysic.service > /dev/null <<EOF
[Unit]
Description=Cysic Verifier
After=network.target

[Service]
User=$USER
WorkingDirectory=/root/cysic-verifier
ExecStart=bash /root/cysic-verifier/start.sh
Restart=on-failure
RestartSec=10
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
### Step 5: Enable and Start the Service
To enable the service, reload the systemd daemon, and start the verifier program, run the following commands:

```bash
sudo systemctl enable cysic
sudo systemctl daemon-reload
sudo systemctl start cysic
```
## ✅ Step 6: View Logs  
Monitor the logs to confirm the service is running correctly:  

```bash
sudo journalctl -u cysic -f --no-hostname -o cat
```

You will get something like this:

![image](https://github.com/user-attachments/assets/80496694-0a16-4be6-b39a-ca4185e1b6a7)

*Cross Verify on cysic Website* :   https://testnet.cysic.xyz/m/dashboard/verifier 
