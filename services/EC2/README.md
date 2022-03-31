# EC2

## Instances
### Instances
- Bastion
  - Step 2: Choose an Instance Type
    - Instance Type - t3.small
  - Step 3: Configure Instance Details
    - Network - VPC
    - Subnet - Public-Subnet
    - Auto-assign Public IP - Enable
    - DNS Hostname - Enable resource-based IPv4 (A record) DNS requests
    - Monitoring - Enable CloudWatch detailed monitoring
  - Step 4: Add Storage
    - default
  - Step 5: Add Tags
    - Key - Name
    - Value - Bastion
  - Step 6: Configure Security Group
    - Assign a security group
      - Select an existing security group - Bastion-SG
  - Step 7: Review Instance Launch
    - Choose an existing key pair
      - Select a key pair - Bastion-Key-Pair

<br/>

### ※ 참고
Bastion 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI에서 수동 생성  
WAS 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI를 Auto Scaling에 적용시켜 자동 생성
