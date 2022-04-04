# VPC

## VPC
### VPCs
- Name - ts-vpc
  - IPv4 CIDR - 10.0.0.0/18

### Subnets
- Name - ts-sub-pub-a
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.0.0/24
  - ※ Objects
    - Bastion
    - NAT GW

- Name - ts-sub-pub-c
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.1.0/24
  - ※ Objects
    - NAT GW

- Name - ts-sub-pub-alb-a
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.10.0/24
  - ※ Objects
    - ALB

- Name - ts-sub-pub-alb-c
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.11.0/24
  - ※ Objects
    - ALB

- Name - ts-sub-pri-svr-a
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.20.0/24
  - ※ Objects
    - WAS

- Name - ts-sub-pri-svr-c
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.21.0/24
  - ※ Objects
    - WAS

- Name - ts-sub-pri-rds-a
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.30.0/24
  - ※ Objects
    - Aurora

- Name - ts-sub-pri-rds-c
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.31.0/24
  - ※ Objects
    - Aurora

- Name - ts-sub-pri-redis-a
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.40.0/24
  - ※ Objects
    - ElastiCache for Redis

- Name - ts-sub-pri-redis-c
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.41.0/24
  - ※ Objects
    - ElastiCache for Redis

### Route Tables
- Name - ts-rt-pub
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - ts-prd-igw
  - Subnets
    - ts-sub-pub-a
    - ts-sub-pub-c
    - ts-sub-pub-alb-a
    - ts-sub-pub-alb-c

- Name - ts-rt-pri-1
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - ts-prd-nat-a
  - Subnets
    - ts-sub-pri-svr-a
    - ts-sub-pri-svr-c

- Name - ts-rt-pri-2
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - ts-prd-nat-c
  - Subnets
    - ts-sub-pri-rds-a
    - ts-sub-pri-rds-c
    - ts-sub-pri-redis-a
    - ts-sub-pri-redis-c

### Internet Gateways
- Name - ts-prd-igw

### Elastic IPs
- Name - ts-prd-nat-a

- Name - ts-prd-nat-c

### Endpoints
- Name - ts-prd-vpc-s3
  - Service category - AWS services
  - Services
    - Name - com.amazonaws.ap-northeast-2.s3
    - Type - Gateway
  - VPC - VPC
  - Route tables
    - ts-rt-pri-1

### NAT Gateways
- Name - ts-prd-nat-a
  - Subnet - ts-sub-pub-a
  - Connectivity type - Public
  - EIP - ts-prd-nat-a

- Name - ts-prd-nat-c
  - Subnet - ts-sub-pub-c
  - Connectivity type - Public
  - EIP - ts-prd-nat-c

<br/>

## Security
### Security Groups
- Name - ts-prd-pub-taesankim.tk-a-bastion-sg
  - VPC - ts-vpc
  - Inboud rules
    - Type - SSH
    - Protocol - TCP
    - Port range - 22
    - Source - Admin IP

- Name - ts-prd-pub-taesankim.tk-lb-sg
  - VPC - ts-vpc
  - Inboud rules
    - Type - HTTP
    - Protocol - TCP
    - Port range - 80
    - Source - 0.0.0.0/0
    - Type - HTTPS
    - Protocol - TCP
    - Port range - 443
    - Source - 0.0.0.0/0

- Name - ts-prd-pri-taesankim.tk-sg
  - VPC - ts-vpc
  - Inboud rules
    - Type - HTTP
    - Protocol - TCP
    - Port range - 80
    - Source - ts-prd-pub-taesankim.tk-lb-sg
    - Type - SSH
    - Protocol - TCP
    - Port range - 22
    - Source - ts-prd-pub-taesankim.tk-a-bastion-sg

- Name - ts-prd-pri-taesankim.tk-rds-sg
  - VPC - VPC
  - Inboud rules
    - Type - MYSQL/Aurora
    - Protocol - TCP
    - Port range - 3306
    - Source - ts-prd-pri-taesankim.tk-sg
    - Type - MYSQL/Aurora
    - Protocol - TCP
    - Port range - 3306
    - Source - ts-prd-pub-taesankim.tk-a-bastion-sg

- Name - ts-prd-pri-taesankim.tk-redis-sg
  - VPC - VPC
  - Inboud rules
    - Type - Custom TCP
    - Protocol - TCP
    - Port range - 6379
    - Source - ts-prd-pri-taesankim.tk-sg
    - Type - Custom TCP
    - Protocol - TCP
    - Port range - 6379
    - Source - ts-prd-pub-taesankim.tk-a-bastion-sg

<br/>

### ※ 참고
현재 사용 서브넷 IP 대역이 **10.0.0.0/24 ~ 10.0.41.0/24** 이므로 이 서브넷 IP 대역을 수용하려면 VPC Prefix가 18보다 작은 숫자여야 함

10.0.0.0/16 ~ 10.0.255.255/16  
10.0.0.0/17 ~ 10.0.127.255/17  
**10.0.0.0/18 ~ 10.0.63.255/18**  
10.0.0.0/19 ~ 10.0.31.255/19  
