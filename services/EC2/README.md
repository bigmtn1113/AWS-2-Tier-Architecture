# EC2

## Instances
### Instances
- ts-prd-pub-taesankim.tk-a-bastion
  - Step 2: Choose an Instance Type
    - Instance Type - t3.small
  - Step 3: Configure Instance Details
    - Network - ts-vpc
    - Subnet - ts-sub-pub-a
    - Auto-assign Public IP - Enable
    - DNS Hostname - Enable resource-based IPv4 (A record) DNS requests
  - Step 4: Add Storage
    - default
  - Step 5: Add Tags
    - Key - Name
    - Value - ts-prd-pub-taesankim.tk-a-bastion
  - Step 6: Configure Security Group
    - Assign a security group
      - Select an existing security group - ts-prd-pub-taesankim.tk-a-bastion-sg
  - Step 7: Review Instance Launch
    - Choose an existing key pair
      - Select a key pair - Bastion-Key-Pair

### Launch templates
- Launch template name and description
  - Launch template name - ts-prd-pri-taesankim.tk-lt_v1
  - Auto Scaling guidance - Provide guidance to help me set up a template that I can use with EC2 Auto Scaling
  - Template tags
    - Key - Name
    - Value - ts-prd-pri-taesankim.tk-lt_v1
- Application and OS Images (Amazon machine Image)
  - My AMIs
    - Owned by me - ts-prd-pri-taesankim.tk-ami
- Instance type
  - Instance type - t3.medium
- Key pair (login)
  - Key pair name - WAS-Key-Pair
- Network settings
  - Firewall (security groups) - Select existing security group
    - Security groups - ts-prd-pri-taesankim.tk-sg
- Resource tags
  - Key - Name
  - Value - ts-prd-pri-taesankim.tk-asg
  - Resource types - Instances
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
  - Load balancer name - ts-prd-pub-taesankim.tk-lb
  - Scheme - Internet-facing
- Network mapping
  - VPC - ts-vpc
  - Mappings
    - ap-northeast-2a - ts-sub-pub-alb-a
    - ap-northeast-2c - ts-sub-pub-alb-c
- Security groups
  - Security groups - ts-prd-pub-taesankim.tk-lb-sg
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
      - Target goup - ts-prd-pri-taesankim.tk-tg
    - Default SSL/TLS certificate
      - From ACM - taesankim.tk
- Tags
  - Key - Name
  - Value - ts-prd-pub-taesankim.tk-lb

### Target Groups
- Basic configuration
  - Choose a target type - Instances
  - Target group name - ts-prd-pri-taesankim.tk-tg
  - Protocol - HTTP
  - Port - 80
  - VPC - ts-vpc
- Health checks
  - Health check protocol - HTTP
  - Health check path - /heath_check.html
- Tags
  - Key - Name
  - Value - ts-prd-pri-taesankim.tk-tg

<br/>

## Auto Scaling
### Auto Scaling Groups
- Choose launch template or configuration
  - Name - ts-prd-pri-taesankim.tk-asg
  - Launch template
    - Launch template - ts-prd-pri-taesankim.tk-lt_v1
    - Version - Default(1)
- Choose instance launch options
  - Network
    - VPC - ts-vpc
    - Availability Zones and subnets
      - ap-northeast-2a | ts-sub-pri-svr-a
      - ap-northeast-2c | ts-sub-pri-svr-c
- Configure advanced options
  - Load balancing - Attach to an existing load balancer
  - Attach to an existing load balancer - Choose from your load balancer target groups
    - Existing load balancer target groups - ts-prd-pri-taesankim.tk-tg | HTTP
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
    - Scaling policy name - Target-Tracking-Policy
    - Metric type - Average CPU utilization
    - Target value - 50

<br/>

### ※ 참고
Bastion 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI에서 수동 생성  
WAS 인스턴스는 EC2 Image Builder를 통해 만들어진 AMI를 Auto Scaling에 적용시켜 자동 생성

위에 명시된 Load Balancer의 Listeners 설정은 ALB를 만든 후 Listners 편집을 통해 설정 가능
