# VPC

## VPC
### VPCs
- VPC settings
  - Name tag - ts-vpc
  - IPv4 CIDR - 10.0.0.0/18

### Subnets
- VPC
  - VPC - ts-vpc
- Subnet settings
  - Subnet 1 of 10
    - Subnet name - ts-sub-pub-a
    - Availability Zone - ap-northeast-2a
    - IPv4 CIDR - 10.0.0.0/24

  - Subnet 2 of 10
    - Subnet name - ts-sub-pub-c
    - Availability Zone - ap-northeast-2c
    - IPv4 CIDR - 10.0.1.0/24

  - Subnet 3 of 10
    - Subnet name - ts-sub-pub-alb-a
    - Availability Zone - ap-northeast-2a
    - IPv4 CIDR - 10.0.10.0/24

  - Subnet 4 of 10
    - Subnet name - ts-sub-pub-alb-c
    - Availability Zone - ap-northeast-2c
    - IPv4 CIDR - 10.0.11.0/24

  - Subnet 5 of 10
    - Subnet name - ts-sub-pri-svr-a
    - Availability Zone - ap-northeast-2a
    - IPv4 CIDR - 10.0.20.0/24

  - Subnet 6 of 10
    - Subnet name - ts-sub-pri-svr-c
    - Availability Zone - ap-northeast-2c
    - IPv4 CIDR - 10.0.21.0/24

  - Subnet 7 of 10
    - Subnet name - ts-sub-pri-rds-a
    - Availability Zone - ap-northeast-2a
    - IPv4 CIDR - 10.0.30.0/24

  - Subnet 8 of 10
    - Subnet name - ts-sub-pri-rds-c
    - Availability Zone - ap-northeast-2c
    - IPv4 CIDR - 10.0.31.0/24

  - Subnet 9 of 10
    - Subnet name - ts-sub-pri-redis-a
    - Availability Zone - ap-northeast-2a
    - IPv4 CIDR - 10.0.40.0/24

  - Subnet 10 of 10
    - Subnet name - ts-sub-pri-redis-c
    - Availability Zone - ap-northeast-2c
    - IPv4 CIDR - 10.0.41.0/24

### Route Tables
- Route table settings
  - Name - ts-rt-pub
  - VPC - ts-vpc
  - Routes
    - Destination and Target
      - 10.0.0.0/18 - local
      - 0.0.0.0/0 - ts-prd-igw
  - Subnet associations
    - Subnet and IPv4 CIDR
      - ts-sub-pub-a - 10.0.0.0/24
      - ts-sub-pub-c - 10.0.1.0/24
      - ts-sub-pub-alb-a - 10.0.10.0/24
      - ts-sub-pub-alb-c - 10.0.11.0/24

--
- Route table settings
  - Name - ts-rt-pri-1
  - - VPC - ts-vpc
  - Routes
    - Destination and Target
      - 10.0.0.0/18 - local
      - 0.0.0.0/0 - ts-prd-nat-a
  - Subnet associations
    - Subnet and IPv4 CIDR
      - ts-sub-pri-svr-a - 10.0.20.0/24
      - ts-sub-pri-svr-c - 10.0.21.0/24

--
- Route table settings
  - Name - ts-rt-pri-2
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - ts-prd-nat-c
  - Subnet associations
    - Subnet and IPv4 CIDR
      - ts-sub-pri-rds-a - 10.0.30.0/24
      - ts-sub-pri-rds-c - 10.0.31.0/24
      - ts-sub-pri-redis-a - 10.0.40.0/24
      - ts-sub-pri-redis-c - 10.0.41.0/24

### Internet Gateways
- Internet gateway settings
  - Name tag - ts-prd-igw
  - VPC - ts-vpc

### Elastic IPs
- Tags
  - Key - Name
  - Value - ts-prd-nat-a-eip

--
- Tags
  - Key - Name
  - Value - ts-prd-nat-c-eip

### Endpoints
- Endpoint settings
  - Name tag - ts-prd-vpc-s3
  - Service category - AWS services
  - Services
    - Name - com.amazonaws.ap-northeast-2.s3
    - Type - Gateway
  - VPC - ts-vpc
  - Route tables
    - ts-rt-pri-1

### NAT Gateways
- NAT gateway settings
  - Name - ts-prd-nat-a
  - Subnet - ts-sub-pub-a
  - Connectivity type - Public
  - EIP - ts-prd-nat-a-eip

--
- NAT gateway settings
  - Name - ts-prd-nat-c
  - Subnet - ts-sub-pub-c
  - Connectivity type - Public
  - EIP - ts-prd-nat-c-eip

<br/>

## Security
### Security Groups
- Basic details
  - Security group name - ts-prd-pub-taesankim.tk-a-bastion-sg
  - VPC - ts-vpc
- Inboud rules
  - Type - SSH
  - Protocol - TCP
  - Port range - 22
  - Source - Admin IP
- Tags
  - Key - Name
  - Value - ts-prd-pub-taesankim.tk-a-bastion-sg

--
- Basic details
  - Security group name - ts-prd-pub-taesankim.tk-lb-sg
  - VPC - ts-vpc
- Inboud rules
  - Type - HTTP
  - Protocol - TCP
  - Port range - 80
  - Source - 0.0.0.0/0  
  --
  - Type - HTTPS
  - Protocol - TCP
  - Port range - 443
  - Source - 0.0.0.0/0
- Tags
  - Key - Name
  - Value - ts-prd-pub-taesankim.tk-lb-sg

--
- Basic details
  - Security group name - ts-prd-pri-taesankim.tk-sg
  - VPC - ts-vpc
- Inboud rules
  - Type - HTTP
  - Protocol - TCP
  - Port range - 80
  - Source - ts-prd-pub-taesankim.tk-lb-sg  
  --
  - Type - SSH
  - Protocol - TCP
  - Port range - 22
  - Source - ts-prd-pub-taesankim.tk-a-bastion-sg
- Tags
  - Key - Name
  - Value - ts-prd-pri-taesankim.tk-sg

--

- Basic details
  - Security group name - ts-prd-pri-taesankim.tk-rds-sg
  - VPC - VPC
- Inboud rules
  - Type - MYSQL/Aurora
  - Protocol - TCP
  - Port range - 3306
  - Source - ts-prd-pri-taesankim.tk-sg  
  --
  - Type - MYSQL/Aurora
  - Protocol - TCP
  - Port range - 3306
  - Source - ts-prd-pub-taesankim.tk-a-bastion-sg
- Tags
  - Key - Name
  - Value - ts-prd-pri-taesankim.tk-rds-sg

--

- Basic details
  - Security group name - ts-prd-pri-taesankim.tk-redis-sg
  - VPC - VPC
- Inboud rules
  - Type - Custom TCP
  - Protocol - TCP
  - Port range - 6379
  - Source - ts-prd-pri-taesankim.tk-sg  
  --
  - Type - Custom TCP
  - Protocol - TCP
  - Port range - 6379
  - Source - ts-prd-pub-taesankim.tk-a-bastion-sg
- Tags
  - Key - Name
  - Value - ts-prd-pri-taesankim.tk-redis-sg

<br/>

### ※ 참고
현재 사용 서브넷 IP 대역이 **10.0.0.0/24 ~ 10.0.41.0/24** 이므로 이 서브넷 IP 대역을 수용하려면 VPC Prefix가 18보다 작은 숫자여야 함

10.0.0.0/16 ~ 10.0.255.255/16  
10.0.0.0/17 ~ 10.0.127.255/17  
**10.0.0.0/18 ~ 10.0.63.255/18**  
10.0.0.0/19 ~ 10.0.31.255/19  
