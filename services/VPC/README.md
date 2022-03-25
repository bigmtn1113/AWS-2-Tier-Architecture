# VPC

## VPC
### VPCs
- Name - VPC
  - IPv4 CIDR - 10.0.0.0/18

### Subnets
- Name - Public-Subnet
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.0.0/24
  - ※ Objects
    - Bastion
    - NAT GW

- Name - Public-Subnet-2
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.1.0/24
  - ※ Objects
    - NAT GW

- Name - Public-Subnet-3
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.10.0/24
  - ※ Objects
    - ALB

- Name - Public-Subnet-4
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.11.0/24
  - ※ Objects
    - ALB

- Name - Private-Subnet
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.20.0/24
  - ※ Objects
    - WAS

- Name - Private-Subnet-2
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.21.0/24
  - ※ Objects
    - WAS

- Name - Private-Subnet-3
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.30.0/24
  - ※ Objects
    - Aurora

- Name - Private-Subnet-4
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.31.0/24
  - ※ Objects
    - Aurora

- Name - Private-Subnet-5
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.40.0/24
  - ※ Objects
    - ElastiCache for Redis

- Name - Private-Subnet-6
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.41.0/24
  - ※ Objects
    - ElastiCache for Redis

### Route Tables
- Name - Public-Route-Table
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - Internet-GW
  - Subnets
    - Public-Subnet
    - Public-Subnet-2
    - Public-Subnet-3
    - Public-Subnet-4

- Name - Private-Route-Table
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - NAT-GW
  - Subnets
    - Private-Subnet
    - Private-Subnet-2

- Name - Private-Route-Table-2
  - Destination and Target
    - 10.0.0.0/18 - local
    - 0.0.0.0/0 - NAT-GW-2
  - Subnets
    - Private-Subnet-3
    - Private-Subnet-4
    - Private-Subnet-5
    - Private-Subnet-6

### Internet Gateways
- Name - Internet-GW

### Elastic IPs
- Name - NAT-GW-EIP

- Name - NAT-GW-2-EIP

### Endpoints
- Name - VPC-Endpoint
  - Service category - AWS services
  - Services
    - Name - com.amazonaws.ap-northeast-2.s3
    - Type - Gateway
  - VPC - VPC
  - Route tables
    - Private-Routing-Table

<br/>

### ※ 참고
현재 사용 서브넷 IP 대역이 **10.0.0.0/24 ~ 10.0.41.0/24** 이므로 이 서브넷 IP 대역을 수용하려면 VPC Prefix가 18보다 작은 숫자여야 함

10.0.0.0/16 ~ 10.0.255.255/16  
10.0.0.0/17 ~ 10.0.127.255/17  
**10.0.0.0/18 ~ 10.0.63.255/18**  
10.0.0.0/19 ~ 10.0.31.255/19  
