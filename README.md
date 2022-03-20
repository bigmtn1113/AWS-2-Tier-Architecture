# AWS-2-Tier-Architecture

## Architecture
<p align="center">
  <img src="https://github.com/kva231/AWS-2-Tier-Architecture/blob/master/images/architecture/Architecture.png" width="75%">
</p>

<hr/>

## Services
### ACM
- ALB, CloudFront에 적용시킬 SSL/TLS 인증서 생성 및 관리

### Amazon RDS(Aurora)
- 향상된 성능의 MySQL 사용

### CloudFront
- 전 세계에 퍼져있는 엣지 로케이션에서 글로벌 유저에게 빠르게 콘텐츠 제공
- OAI 사용으로 CloudFront를 통해 S3 접근

### CloudTrail
- 사용자, 역할 또는 AWS 서비스가 수행하는 작업을 이벤트로 기록

### CloudWatch
- 모니터링 및 운영 데이터를 로그, 지표 및 이벤트 형태로 수집

### CodeCommit
- 팀의 코드 협업을 위한 소스 코드 저장소 사용

### CodeDepoly
- 소프트웨어 배포 자동화

### CodePipeline
- CodeCommit에서 코드 변경 사항 발생 시, 자동으로 CodeDeploy가 배포를 진행하도록 파이프라인 구성

### EC2
- Bastion Host 역할을 수행할 서버, Application(WordPress)을 실행할 WAS 서버로 구성
- ALB 트래픽 전달 대상 및 Auto Scaling 대상은 WAS Instances

### EC2 Image Builder
- Bastion AMI, WAS AMI 생성 및 관리

### ElastiCache(Redis)
- Application 지연 시간을 줄이기 위한 인 메모리 데이터 스토어

### IAM
- User groups, Users, Roles, Policies 등 관리

### Route 53
- 도메인 생성 및 관리
- ALB, CloudFront로 라우팅 수행

### S3
- 콘텐츠 이미지 저장

### VPC
- VPCs, Subnets, Route Tables, Internet Gateways, Elastic IPs, Endpoints, NAT Gateways, Security Groups 등 관리

### WAF
- SQL Injection, XSS 공격 외에도 여러 공격으로부터 Web Application이나 API를 보호하는 방화벽
