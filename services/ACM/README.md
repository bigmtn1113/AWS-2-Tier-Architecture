# ACM

## ACM
### Request certificate
- Region - ap-northeast-2 (Seoul)
  - Certificate type - Request a public certificate
  - Domain names
    - Fully qualified domain name
      - taesankim.tk
      - *.taesankim.tk
  - Validation method
    - DNS validation

- Region - us-east-1 (N. Virginia)
  - Certificate type - Request a public certificate
  - Domain names
    - Fully qualified domain name
      - taesankim.tk
      - *.taesankim.tk
  - Validation method
    - DNS validation

<br/>

### ※ 참고
ALB 접근 및 CloudFront를 통해 S3로의 접근할 때 HTTPS로 접근하도록 하기 위한 인증서 설정
인증서 요청 후, 각 Domain에 대한 레코드를 Route 53에 생성해야 Status가 Issued 됨
