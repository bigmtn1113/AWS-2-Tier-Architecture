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

### Launch templates
- Launch template name and description
  - Launch template name - WAS-Launch-Template
  - Auto Scaling guidance - Provide guidance to help me set up a template that I can use with EC2 Auto Scaling
  - Template tags
    - Key - Name
    - Value - WAS-Launch-Template
- Application and OS Images (Amazon machine Image)
  - My AMIs
    - Owned by me - Recipe-For-WAS-AMI
- Instance type
  - Instance type - t3.medium
- Key pair (login)
  - Key pair name - WAS-Key-Pair
- Network settings
  - Firewall (security groups) - Select existing security group
    - Security groups - WAS-SG
- Resource tags
  - Key - Name
  - Value - WAS
- Advanced details
  - IAM instance profile - EC2InstanceRole

<br/>

## Network & Security
### Key Pairs
- Bastion-Key-Pair
  - Key pair
    - Name - Bastion-Key-Pair
    - Key pair type - RSA
    - Private key file format - .pem

- WAS-Key-Pair
  - Key pair
    - Name - WAS-Key-Pair
    - Key pair type - RSA
    - Private key file format - .pem

<br/>

## Load Balancing
### Load Balancers
- Load balancer types - Application Load Balancer
- Basic configuration
  - Load balancer name - WAS-ALB
  - Scheme - Internet-facing
- Network mapping
  - VPC - VPC
  - Mappings
    - ap-northeast-2a - Public-Subnet-3
    - ap-northeast-2c - Public-Subnet-4
- Security groups
  - Security groups - WAS-ALB-SG
- Listeners and routing
  - Listener - HTTP:80
    - Protocol - HTTP
    - Port - 80
    - Default action - Redirect
      - Itemized URL
      - Protocol - HTTPS
      - Port - 443
    - Protocol - HTTPS
    - Port - 443
    - Default action - Forward to
      - Target goup - WAS-TG
    - Default SSL/TLS certificate
      - From ACM - taesankim.tk
- Tags
  - Key - Name
  - Value - WAS-ALB

### Target Groups
- Basic configuration
  - Choose a target type - Instances
  - Target group name - WAS-TG
  - Protocol - HTTP
  - Port - 80
  - VPC - VPC
- Health checks
  - Health check protocol - HTTP
  - Health check path - /heath_check.html
- Tags
  - Key - Name
  - Value - WAS-TG

<br/>

## Auto Scaling
### Auto Scaling Groups
- Choose launch template or configuration
  - Name - WAS-ASG
  - Launch template
    - Launch template - WAS-Launch-Template
    - Version - Default(1)
- Choose instance launch options
  - Network
    - VPC - VPC
    - Availability Zones and subnets
      - ap-northeast-2a | Private-Subnet
      - ap-northeast-2c | Private-Subnet-2
- Configure advanced options
  - Load balancing - Attach to an existing load balancer
  - Attach to an existing load balancer - Choose from your load balancer target groups
    - Existing load balancer target groups - WAS-TG | HTTP
  - Health checks
    - Health check grace period - 120 seconds
  - Additional settings
    - Monitoring - Enable group metrics collection within CloudWatch
- Configure group size and scaling policies
  - Group size
    - Desired capacity - 2
    - Minimum capacity - 2
    - Maximum capacity - 4
  - Scaling policies - Target tracking scaling policy
    - Scaling policy name - WAS-Target-Tracking-Policy
    - Metric type - Average CPU utilization
    - Target value - 50

<br/>

### ※ 참고
Bastion 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI에서 수동 생성  
WAS 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI를 Auto Scaling에 적용시켜 자동 생성

위에 명시된 Load Balancer의 Listeners 설정은 ALB를 만든 후 Listners 편집을 통해 설정 가능
