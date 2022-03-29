# ACM

## ACM
### Request certificate
- Region - ap-northeast-2 (Seoul)
  - Certificate type - Request a public certificate
  - Fully qualified domain name
    - taesankim.tk
    - *.taesankim.tk
  - validation method - DNS
  - Tags
    - key - Name
    - value - Public-Certificate-For-ALB

- Region - us-east-1 (N. Virginia)
  - Certificate type - Request a public certificate
  - Fully qualified domain name
    - img.taesankim.tk
    - *.taesankim.tk
  - validation method - DNS
  - Tags
    - key - Name
    - value - Public-Certificate-For-CloudFront

<br/>

### ※ 참고
ALB 접근 및 CloudFront를 통해 S3로의 접근할 때 HTTPS로 접근하도록 하기 위한 인증서 설정
