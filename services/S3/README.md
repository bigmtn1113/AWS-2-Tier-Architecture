# S3

## S3
### Buckets
- General configuration
  - Bucket name - ts-prd-taesankim.tk-s3
  - AWS Region - Asia Pacific (Seoul) ap-northeast-2
- Object Ownership - ACLs disabled
- Block Public Access settings for this bucket - Block all public access
- Bucket Versioning - Enable
- Tags
  - Key - Name
  - Value - ts-prd-taesankim.tk-s3

<br/>

### ※ 참고
퍼블릭 액세스를 모두 차단해서 객체로의 접근 차단  
WAS에서 Image에 접근해야 할 경우엔 **CloudFront의 OAI**를 이용해 접근하도록 설정
