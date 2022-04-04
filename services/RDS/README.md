# RDS

## RDS
### Databases
- Database creation method - Standard
- Engine options
  - Engine type - Amazon Aurora
  - Edition - Amazon Aurora MySQL-Compatible Edition
  - Available versions - Aurora (MySQL 5.7) 2.07.2
- Templates - Production
- Settings
  - DB cluster identifier - ts-prd-pri-taesankim-tk-aurora
  - Master username - admin
  - Master password - Password12#$
- DB instance class - db.t3.small
- Multi-AZ deployment - Create an Aurora Replica or Reader node in a different AZ
- Connectivity
  - VPC - ts-vpc
  - Subnet group - ts-prd-pri-rds
  - VPC security group - ts-prd-pri-taesankim.tk-rds-sg
- Additional configuration
  - Database options
    - Initial database name - wordpress
    - DB cluster parameter group - taesankim.tk-5.7
    - DB parameter group - taesankim.tk-5.7

### Subnet groups
- Subnet group details
  - Name - ts-prd-pri-rds
  - VPC - ts-vpc
- Add subnets
  - Availability Zones
    - ap-northeast-2a
    - ap-northeast-2c
  - Subnets
    - 10.0.30.0/24 (ts-sub-pri-rds-a)
    - 10.0.31.0/24 (ts-sub-pri-rds-c)

### Parameter groups
- Group name - taesankim.tk-5.7
  - Parameter group family - aurora-mysql5.7
  - Type - DB Cluster Parameter Group
- Group name - taesankim.tk-5.7
  - Parameter group family - aurora-mysql5.7
  - Type - DB Parameter Group
