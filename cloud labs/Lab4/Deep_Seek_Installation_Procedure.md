# Lab 4: Installing and Deploying DeepSeek-R1 1.5B on Huawei Cloud

![DeepSeek Lab](images/S5.png)

## Objective
Deploy the DeepSeek-R1 1.5B large language model using Huawei Cloud ECS and Ollama.

---

## Prerequisites

- Access the **Lab Desktop**
- Login via **IAM User** using provided credentials on [Huawei Cloud](https://console.huaweicloud.com)

---

## Step 1: Preparing the Lab Environment

### 1.1 Create an ECS

- Go to: **Service List > Elastic Cloud Server > Buy ECS**
- Click **Custom Config** tab:
  - **Billing Mode**: Pay-per-use
  - **Region**: AP-Singapore
  - **Architecture**: x86
  - **Flavor**: `c6.xlarge.2` (4 vCPUs | 8 GiB RAM)
  - **Image**: CentOS 8.2 64bit (40 GiB)
  - **System Disk**: 40 GiB
  - **VPC/Security Group**: Default (create if not available)
  - **EIP**: Auto assign, Dynamic BGP, Traffic billing, 100 Mbps bandwidth (recommended)
  - **ECS Name**: `ecs-cent`
  - **Password**: e.g `Huawei1234%`
- Click **Submit > Agree and Submit**


![ECS](images/S2.png)
---

### 1.2 Login to ECS

- Use **CloudShell** or SSH to connect to the ECS
- Enter password: `Huawei1234%`

---

## Step 2: Installing Ollama

### Option 1: GitHub Installation (may be unstable)

```
curl -fsSL https://ollama.com/install.sh | sh
ollama -v
```

![Ollama Installed](images/S3.png)

## Option 2: Download from OBS (recommended)

```
wget https://sandbox-experiment-files.obs.cn-north-4.myhuaweicloud.com/deepseek/ollama-linux-amd64.tgz
sudo tar -C /usr -xzf ollama-linux-amd64.tgz
sudo chmod +x /usr/bin/ollama
```

Create ollama user if missing:

`id ollama || sudo useradd -r -s /bin/false -m -d /usr/share/ollama ollama`

Create systemd service:

```
cat << EOF | sudo tee /etc/systemd/system/ollama.service
[Unit]
Description=Ollama Service
After=network-online.target

[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
ExecStart=/usr/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
EOF
```

Enable and start the service:

```
sudo systemctl daemon-reload
sudo systemctl enable ollama
sudo systemctl start ollama
ollama -v
```

## Step 3: Deploying DeepSeek-R1 7B

Option 1: Pull from Ollama (slower)

```
ollama pull deepseek-r1:7b
```

![Deep Seek Installing (R1:7b)](images/S4.png)

```
ollama run deepseek-r1:7b
```
![Deep Seek Installed (R1:7b)](images/S5.png)

If interrupted, press Ctrl+C and rerun. Ollama supports resumable downloads.

---
