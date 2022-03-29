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
  - DB cluster identifier - Aurora-Cluster-For-WordPress
  - Master username - admin
  - Master password - Password12#$
- DB instance class - db.t3.small
- Multi-AZ deployment - Create an Aurora Replica or Reader node in a different AZ
- Connectivity
  - VPC - VPC
  - Subnet group - aurora-subnet-group
  - VPC security group - Aurora-SG
- Additional configuration
  - Database options
    - Initial database name - wordpress
    - DB cluster parameter group - aurora-cluster-parameter-group
    - DB parameter group - aurora-parameter-group

### Subnet groups
- Subnet group details
  - Name - aurora-subnet-group
  - VPC - VPC
- Add subnets
  - Availability Zones
    - ap-northeast-2a
    - ap-northeast-2c
  - Subnets
    - 10.0.30.0/24 (Private-Subnet-3)
    - 10.0.31.0/24 (Private-Subnet-4)

### Parameter groups
- Group name - aurora-cluster-parameter-group
  - Parameter group family - aurora-mysql5.7
  - Type - DB Cluster Parameter Group
- Group name - aurora-parameter-group
  - Parameter group family - aurora-mysql5.7
  - Type - DB Parameter Group
