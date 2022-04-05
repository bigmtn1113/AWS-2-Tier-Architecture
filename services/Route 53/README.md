# Route 53

## Route 53
### Hosted zones
- Hosted zone configuration
  - Domain name - taesankim.tk
- taesankim.tk
  - Records
    - Record name - ~~.taesankim.tk
    - Record type - CNAME
    - Value - ~~.acm-validations.aws.

    --
    - Record name - taesankim.tk
    - Record type - A
    - Route traffic to
      - Alias to Application and Classic Load Balancer
      - Asia Pacific (Seoul) [ap-northeast-2]
      - ~~.elb.amazonaws.com.

    --
    - Record name - www.taesankim.tk
    - Record type - A
    - Route traffic to
      - Alias to Application and Classic Load Balancer
      - Asia Pacific (Seoul) [ap-northeast-2]
      - ~~.elb.amazonaws.com.
    
    --
    - Record name - img.taesankim.tk
    - Record type - A
    - Route traffic to
      - Alias to CloudFront distribution
      - US East (N.Virginia)
      - ~~.cloudfront.net.

<br/>

### ※ 참고
NS, SOA 레코드는 호스팅 영역 생성 시 자동 생성 (여기선 표기 X)  
Value/Route traffic to는 Alias 비활성화/활성화 차이

taesankim.tk, www.taesankim.tk 로 접근 시 ALB로 라우팅  
img.taesankim.tk로 접근 시 CloudFront로 라우팅
