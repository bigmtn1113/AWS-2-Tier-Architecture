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

배포 유형이 Blue/green일 경우, 새로 만들어지는 인스턴스에 CodeDeploy Agent가 설치되어 있는지 확인  
AllowTraffic이 계속 진행 중일 경우, 배포 대상 인스턴스의 health check 확인

[배포 시간이 너무 길 경우, 참고](https://github.com/kva231/Cloud-System-Engineer-Study/blob/master/05.%20AWS/%EA%B8%B0%ED%83%80/CodeDeploy%20%EB%B0%B0%ED%8F%AC%20%EC%8B%9C%EA%B0%84%20%EC%A4%84%EC%9D%B4%EA%B8%B0.md)
