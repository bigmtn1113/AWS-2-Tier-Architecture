# CodeDeploy

## Deploy
### Applications
- Application configuration
  - Application name - ts-prd-pri-taesankim.tk-app
  - Compute platform - EC2/On-premises
- ts-prd-pri-taesankim.tk-app
  - Deployment groups
    - Deployment group name - ts-prd-pri-taesankim.tk-asg-dg
  - Service role - AWSCodeDeployRole
  - Deployment type - Blue/green
  - Environment configuration - Automatically copy Amazon EC2 Auto Scaling group
    - Amazon EC2 Auto Scaling group - ts-prd-pri-taesankim.tk-asg
  - Deployment settings
    - Traffic rerouting - Reroute traffic immediately
    - Terminate the original instances in the deployment group
      - Days - 0
      - Hours - 1
      - Minutes - 0
    - Deployment configuration - CodeDeployDefault.HalfAtATime
  - Load balancer
    - Application Load Balancer or Network Load Balancer
      - Target gourp - ts-prd-pri-taesankim.tk-tg

<br/>

### ※ 참고
배포 후 기존 인스턴스 종료 시간은 시간상 0/0/5로 설정하고 진행  
배포 구성도 마찬가지로 시간상 CodeDeployDefault.AllAtOnce로 설정하고 진행
