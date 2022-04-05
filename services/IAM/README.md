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

--
- Trusted entity
  - Trusted entity type - AWS service
  - Use case - CodeDeploy
- Permissions
  - Permissions policies
    - AWSCodeDeployRole
    - AWSCodeDeployRoleForBlueGreen
- Role details
  - Role name - AWSCodeDeployRole


<br/>

### ※ 참고
AmazonEC2RoleforAWSCodeDeploy - EC2에 설치된 CodeDeploy 에이전트가 애플리케이션 배포에 사용하는 파일(Application revision)을 S3에서 가져올 수 있게 허용하는 정책. S3에 대한 권한이 명시되어 있음

원래 CodeDeploy를 사용하려면 EC2에 AmazonEC2RoleforAWSCodeDeploy 권한을 적용해야 함  
그러나 VPC Endpoint를 사용할 때 필요한 AmazonS3FullAccess 권한이  
AmazonEC2RoleforAWSCodeDeploy 권한까지 포함되므로 AmazonS3FullAccess 권한을 부여한 것

--  
AWSCodeDeployRoleForBlueGreen - 인라인 정책. Blee/Green 배포 방식을 선택했을 때 발생하는 에러를 해결하기 위한 정책
- iam:PassRole
- ec2:CreateTags
- ec2:RunInstances
