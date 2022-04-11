## Data Migration

### 사전 작업
- mysqldump를 저장할 S3 Bucket 생성
- S3로 접근할 수 있는 권한을 가진 사용자로 진행
- DB로 mysqldump 파일을 전달하는 용도의 EC2 인스턴스 생성
- EC2에서 S3 Bucket에 있는 파일을 다운로드할 수 있도록 EC2에 IAM 권한 설정
- EC2에서 DB로 접근할 수 있도록 보안 그룹 설정

<br/>

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
#### 3. On-Premise 환경에서 mysqldump 파일 생성
  ```bash
  mysqldump -u <On-Premise DB username> -p --all-databases > <mysqldump 파일 명>
  ```
#### 4. S3 Bucket에 mysqldump 파일 업로드
  ```bash
  aws s3 cp <mysqldump 파일 명> s3://<버킷 이름>
  ```
#### 5. EC2 인스턴스에 접속 후, S3 Bucket에 있는 mysqldump 파일 다운로드
  ```bash
  aws s3 cp s3://<버킷 이름/mysqldump 파일 명> <파일을 다운로드할 경로>
  ```
#### 6. EC2 인스턴스에서 DB로 접속 후, mysqldump 파일 실행
  ```bash
  mysql -u <DB username> -p -h <DB host>
  ```
  ```sql
  MySQL [(none)]> source <mysqldump 파일 명>
  ```

<br/>

### ※ 참고
On-Premise DB는 mysql  
Migration을 적용할 DB는 Aurora  
EC2 인스턴스는 기존 Bastion EC2를 사용
