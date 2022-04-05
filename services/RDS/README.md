# RDS

## RDS
### Databases
- Database creation method - Standard
- Engine options
  - Engine type - Amazon Aurora
  - Edition - Amazon Aurora MySQL-Compatible Edition
  - Available versions - Aurora MySQL 3.01.0 (compatible with MySQL 8.0.23)
- Templates - Production
- Settings
  - DB cluster identifier - ts-prd-pri-taesankim-tk-aurora
  - Master username - admin
  - Master password - Password12#$
- DB instance class - db.t3.medium
- Multi-AZ deployment - Create an Aurora Replica or Reader node in a different AZ
- Connectivity
  - VPC - ts-vpc
  - Subnet group - ts-prd-pri-rds
  - VPC security group - ts-prd-pri-taesankim.tk-rds-sg
- Additional configuration
  - Database options
    - Initial database name - wordpress
    - DB cluster parameter group - taesankim-tk-80
    - DB parameter group - taesankim-tk-80
  - Monitoring
    - Enable Enhanced monitoring - Not enabled
  - Log exports
    - Audit log
    - Error log
    - General log
    - Slow query log

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
- Parameter group details
  - Parameter group family - aurora-mysql8.0
  - Type - DB Cluster Parameter Group
  - Group name - taesankim-tk-80

--
- Parameter group details
  - Parameter group family - aurora-mysql8.0
  - Type - DB Parameter Group
  - Group name - taesankim-tk-80

<br/>

### ※ 참고
Aurora를 사용할 시 option group 선택 불가  
엔진 옵션을 MySQL을 선택하면 직접 생성한 option group 적용 가능
