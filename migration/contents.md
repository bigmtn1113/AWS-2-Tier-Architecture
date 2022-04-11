## Contents Migration

### 사전 작업
- Contents를 저장할 S3 Bucket 생성
- EC2에서 S3로 접근할 수 있도록 IAM 권한 부여

### 과정
#### 1. On-Premise 환경에 AWS CLI 설치
  ```bash
  pip install awscli
  aws --version
  ```
#### 2. aws configure 실행
  ```bash
  aws configure
  # AWS Access Key ID 입력
  # AWS Secret Access Key0 입력
  # Default region name 입력
  # Default output format 입력
  ```
#### 3. S3 Bucket에 Contents 업로드
  ```bash
  aws s3 cp <업로드할 파일> s3://<버킷 이름>      # 여러 파일이나 디렉터리 업로드 시, aws s3 sync 명령어 사용
  ```
