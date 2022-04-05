# IAM

## Access management
### Roles
- Trusted entity
  - Trusted entity type - AWS service
  - Use case - EC2
- Permissions
  - Permissions policies
    - AmazonS3FullAccess
- Role details
  - Role name - AmazonEC2RoleForS3

<br/>

### ※ 참고
AmazonEC2RoleforAWSCodeDeploy은 EC2에 설치된 CodeDeploy 에이전트가 애플리케이션 배포에 사용하는 파일을 S3에서 가져올 수 있게 허용하는 정책이라 S3에 대한 권한이 명시되어 있음  
원래 CodeDeploy를 사용하려면 EC2에 AmazonEC2RoleforAWSCodeDeploy 권한을 적용해야 함  
그러나 VPC Endpoint를 사용할 때 필요한 AmazonS3FullAccess 권한이 AmazonEC2RoleforAWSCodeDeploy 권한까지 포함되므로 AmazonS3FullAccess 권한을 부여한 것
