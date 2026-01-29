# VPC (virtual Private Cloud) Peering Between two different AWS regions 

##  Overview
VPC Peering is a networking connection between two Virtual Private Clouds (VPCs) that enables routing traffic between them using private IPv4 addresses.  
AWS allows **inter-region VPC peering**, meaning VPCs can communicate securely even if they are in **different AWS regions**.

---
##  Key Features
- Private communication using AWS backbone network
- Low latency and high bandwidth
- No single point of failure
- No gateway, VPN, or public IP required
- Works across **different AWS regions**
---

##  Architecture
![alt text](IMG/VPC%20_peering.png)

---
##  Step-by-Step Configuration

### Step 1: Create VPC Peering Connection
            1. Open AWS VPC Console
            2. Go to Peering Connections
            3. Click Create peering connection
            4. Configure:
            - Requester VPC: `VPC-A (ap-south-1)`
            - Accepter VPC: `VPC-B (us-east-1)`
            - Select Another region
            5. Click Create

### Step 2: Accept Peering Connection
            1. Switch to the accepter region
            2. Open Peering Connections
            3. Select the pending request
            4. Click Accept Request

### Step 3: Update Route Tables
#### Route Table in VPC-A
| Destination CIDR | Target   |
| ---------------- | -------- |
| 192.24.0.0/16 (Private_Appsubnet) | pcx-xxxx |

#### Route Table in VPC-B
| Destination CIDR | Target   |
| ---------------- | -------- |
| 10.0.0.0/20 (Private_DBsubnet) | pcx-xxxx |

### Step 4: Launch EC2 using vpc of both region 
#### EC2 Region-A
    1. proxy server (ec2)
    2. App server (EC2)

#### EC2 Region-B
    1. DB Server
---

##  Output
#### vpc-A Region
![alt text](IMG/vpc-A_roadmap.png)
![alt text](IMG/peerA.png)
![alt text](IMG/ec2%20-A.png)
![alt text](IMG/RouteTable.png)

#### vpc-B Region
![alt text](IMG/vpc-B_roadmap.png)
![alt text](IMG/peerB.png)
![alt text](IMG/ec2-B.png)
![alt text](IMG/terminal.png)

