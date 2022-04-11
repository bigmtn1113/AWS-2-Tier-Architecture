# CloudFront

## CloudFront
### Distributions
- Origin
  - Origin domain - ts-prd-taesankim.tk-s3.s3.ap-northeast-2.amazonaws.com
  - Name - ts-prd-taesankim.tk-s3
  - S3 bucket access
    - use OAI
    - Origin access identity - access-identity-ts-prd-taesankim.tk-s3.s3.ap-northeast-2.amazonaws.com
    - Bucket policy - update the bucket policy
- Default cache behavior
  - Viewer
    - Viewer protocol policy - Redirect HTTP to HTTPS
- Settings
  - AWS WAF web ACL - ts-prd-img.taesankim.tk-cf-waf
  - Alternate domain name (CNAME) - img.taesankim.tk
  - Custom SSL certificate - taesankim.tk

<br/>

### ※ 참고
CloudFront OAI를 이용해 퍼블릭 엑세스를 차단한 S3 Bucket에 접근  
CloudFront에 인증서를 적용하기 위해선 N. Virginia에 인증서가 존재해야 함
