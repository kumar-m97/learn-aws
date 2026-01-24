# Learn AWS

**##Random Topics are covered##**

## ACL Configuration:  
In AWS Network ACLs (NACLs), rule numbers control evaluation order. Lower numbers are evaluated first.  

### ✅ How rules 100 and 200 work  
AWS evaluates rule 100 first  
If rule 100 matches, AWS applies the action immediately (ALLOW or DENY)  
Rule 200 is ignored if rule 100 already matched  
If rule 100 does NOT match, AWS moves to rule 200  
👉 First match wins. No further rules are checked.  

### Example  
<img width="906" height="271" alt="image" src="https://github.com/user-attachments/assets/3582f268-2993-4ea4-95a0-537c79371b7e" />  

**What happens?**
SSH traffic from 10.0.5.10  
Matches rule 100  
✅ ALLOWED  
Rule 200 never evaluated  

HTTP traffic from 10.0.5.10  
Does not match rule 100  
Matches rule 200  
❌ DENIED  

<img width="1040" height="329" alt="image" src="https://github.com/user-attachments/assets/69c1c3f2-cc15-4964-96d6-b73a4034774d" />  

## VPC Peering Setup  
Scenario: Connect VPC-A (10.0.0.0/16) with VPC-B (172.16.0.0/16)  

**Steps:**
Go to VPC Dashboard → Click "Peering Connections"  
Click "Create peering connection"  
Name: e.g., "VPC-A-to-VPC-B-Peering"  
VPC (Requester): Select VPC-A  
Account: My account (or "Another account" if different)  
Region: This region (or "Another region" for cross-region)  
VPC (Accepter): Select VPC-B  

Click "Create peering connection"  
Accept the peering request:  
The connection will be in "Pending Acceptance" state  
Select the peering connection → Click "Actions" → "Accept request"  

**Update Route Tables (Critical step!):**   
In VPC-A's route table:  
Go to "Route Tables" → Select VPC-A's route table  
Click "Routes" tab → "Edit routes" → "Add route"  
Destination: 172.16.0.0/16 (VPC-B's CIDR)  
Target: Select the peering connection  
Save  

**In VPC-B's route table:**  
Select VPC-B's route table → "Edit routes" → "Add route"  
Destination: 10.0.0.0/16 (VPC-A's CIDR)  
Target: Select the same peering connection  
Save  

**Update Security Groups:** Ensure security groups allow traffic from the other VPC's CIDR blocks  

## Transit Gateway  


## Virtual Private Gateway  
--> Connects on-premise datacenter to AWS resources using VPG and VPN  
<img width="374" height="265" alt="image" src="https://github.com/user-attachments/assets/00bd8bc8-97e1-4ca9-9937-0b76546f58cc" />  
<img width="533" height="266" alt="image" src="https://github.com/user-attachments/assets/4a5341e0-c1b3-4f7e-9fd3-7cb954f1dc6b" />  
<img width="1041" height="581" alt="image" src="https://github.com/user-attachments/assets/cb817c0a-a79e-4a42-bebb-5490519c5dfd" />  
<img width="919" height="369" alt="image" src="https://github.com/user-attachments/assets/e2ed196e-b03e-468a-b02a-5ad30169fc4c" />  
<img width="1001" height="549" alt="image" src="https://github.com/user-attachments/assets/a2075e18-3bc9-4628-a310-cfecde3a01a9" />  
<img width="1108" height="383" alt="image" src="https://github.com/user-attachments/assets/3a81fc89-f08f-40a1-85bf-ca7b24696769" />  
<img width="1070" height="314" alt="image" src="https://github.com/user-attachments/assets/c0e0a5ae-169e-4d46-93bf-df2ea5984229" />  
<img width="624" height="215" alt="image" src="https://github.com/user-attachments/assets/f048a423-6d48-47e0-8316-bf719c41111b" />  
<img width="1035" height="445" alt="image" src="https://github.com/user-attachments/assets/ee638dbe-a269-4946-b87d-65c8b2810138" />  
<img width="976" height="302" alt="image" src="https://github.com/user-attachments/assets/5a0f15dd-fa51-4aa1-aa2a-01261b3cc585" />  
<img width="785" height="266" alt="image" src="https://github.com/user-attachments/assets/e2964858-42a6-4e66-a215-36f36597c525" />  


**Route Propagation use while setting up the routes**:  
<img width="1047" height="496" alt="image" src="https://github.com/user-attachments/assets/03550374-88e6-493f-bd57-cb4a2238fe3c" />  

## Client VPN Setup  
--> It is used to provide individual remote user acess to AWS resources  
**Laptop → VPN → VPC (private access)**  
<img width="542" height="301" alt="image" src="https://github.com/user-attachments/assets/ac1fb309-0ac5-4083-a5c2-c013a2125206" />  

## AWS Direct Connect  
<img width="1055" height="199" alt="image" src="https://github.com/user-attachments/assets/fba4d51c-15bc-400b-bf04-b6b4cb5cce9f" />  
<img width="1041" height="177" alt="image" src="https://github.com/user-attachments/assets/b3e8d4b6-632b-4a3d-9043-cc92c09e63d8" />  
<img width="503" height="204" alt="image" src="https://github.com/user-attachments/assets/56f62fae-22a0-4946-8ee1-00eb15b10f81" />  

## VPC Endpoints  
--> VPC Endpoints allow your vpc to privately connect to AWS services without internet,NAT, or IGW  

### Two types of VPC Endpoints:  
**1. Gatewway endpoints:**  
Used only for: S3,DynamoDB  

**2. Interface Endpoints(Private Endpoints):**
Used for most AWS Services  


## AWS Private Link  
To enable a private connection to services hosted in different VPC within the same AWS account or in different AWS accounts, we use AWS PrivateLink. It enables us to connect our VPC privately to supported AWS services, services hosted by other AWS accounts (VPC endpoint services), and supported AWS Marketplace partner services. We need not to use an Internet Gateway, NAT device, public IP address, AWS Direct Connect connection, or AWS Site-to-Site VPN connection to communicate with the service.    
<img width="1342" height="766" alt="image" src="https://github.com/user-attachments/assets/9f47d452-5f94-4cac-88e1-9aa65983a8d5" />  
### -->Two sides of PrivateLink
**VPC Endpoint**  
This is created in the consumers account to have an endpoint for VPC to enable a private connection to a service.  
**VPC Endpoint Service**  
This is created in the producers account where you have your service up and running. Other AWS principals can access this service using VPC endpoints.  

<img width="439" height="300" alt="image" src="https://github.com/user-attachments/assets/c2d52040-c531-45f1-9bc3-0d38616451e5" />  
<img width="875" height="441" alt="image" src="https://github.com/user-attachments/assets/22ce0a61-5595-4455-b520-f1c727004f56" />  

For more infor refer  
https://medium.com/@knoldus/how-to-use-aws-privatelink-via-aws-console-38720c4dffa5

## NAT Instance and its condifuration  
A NAT Instance is an EC2 instance acting as a NAT device to allow private subnets to access the internet  
Not much used now. Use Nat Gatways instead.  






















