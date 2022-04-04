# CloudFront

## CloudFront
### Distributions
- Origin domain - ts-prd-taesankim.tk-s3.s3.ap-northeast-2.amazonaws.com
  - S3 bucket access
    - use OAI
    - Origin access identity - access-identity-ts-prd-taesankim.tk-s3.s3.ap-northeast-2.amazonaws.com
    - Bucket policy - update the bucket policy
  - Viewer protocol policy - Redirect HTTP to HTTPS
  - AWS WAF web ACL - ts-prd-img.taesankim.tk-cf-waf
  - Alternate domain name (CNAME) - img.taesankim.tk
  - Custom SSL certificate - taesankim.tk
  - Default root object - index.html

<br/>

### ※ 참고
CloudFront에 인증서를 적용하기 위해선 N. Virginia에 인증서가 존재해야 함
