# VPC

## VPC
### VPCs
- Name - VPC
  - IPv4 CIDR - 10.0.0.0/18

### Subnets
- Subnet Name - Public-Subnet
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.0.0/24
  - ※ Objects
    - Bastion
    - NAT GW

- Subnet Name - Public-Subnet-2
  - Availability Zone - ap-northeast-2c
  - IPv4 CIDR - 10.0.1.0/24
  - ※ Objects
    - NAT GW

- Subnet Name - Public-Subnet-3
  - Availability Zone - ap-northeast-2a
  - IPv4 CIDR - 10.0.10.0/24
  - ※ Objects
    - ALB

서브넷 이름 - Public-Subnet-4
가용 영역 - ap-northeast-2c	용도: ALB
IPv4 CIDR - 10.0.11.0/24

서브넷 이름 - Private-Subnet
가용 영역 - ap-northeast-2a	용도: WAS
IPv4 CIDR - 10.0.20.0/24

서브넷 이름 - Private-Subnet-2
가용 영역 - ap-northeast-2c	용도: WAS
IPv4 CIDR - 10.0.21.0/24

서브넷 이름 - Private-Subnet-3
가용 영역 - ap-northeast-2a	용도: Aurora
IPv4 CIDR - 10.0.30.0/24

서브넷 이름 - Private-Subnet-4
가용 영역 - ap-northeast-2c	용도: Aurora
IPv4 CIDR - 10.0.31.0/24

서브넷 이름 - Private-Subnet-5
가용 영역 - ap-northeast-2a	용도: ElastiCache for Redis
IPv4 CIDR - 10.0.40.0/24

서브넷 이름 - Private-Subnet-6
가용 영역 - ap-northeast-2c	용도: ElastiCache for Redis
IPv4 CIDR - 10.0.41.0/24

<br/>

### ※ 참고
현재 사용 서브넷 IP 대역이 **10.0.0.0/24 ~ 10.0.41.0/24** 이므로 이 서브넷 IP 대역을 수용하려면 VPC Prefix가 18보다 작은 숫자여야 함

10.0.0.0/16 ~ 10.0.255.255/16  
10.0.0.0/17 ~ 10.0.127.255/17  
**10.0.0.0/18 ~ 10.0.63.255/18**  
10.0.0.0/19 ~ 10.0.31.255/19  
