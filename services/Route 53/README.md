# Route 53

## Route 53
### Hosted zones
- Domain name - taesankim.tk
  - Records
    - Record name - ~~.taesankim.tk
      - Type - CNAME
      - Value/Route traffic to - ~~.acm-validations.aws.
    - Record name - ~~.taesankim.tk
      - Type - CNAME
      - Value/Route traffic to - ~~.acm-validations.aws.
    - Record name - taesankim.tk
      - Type - A
      - Value/Route traffic to - ~~.elb.amazonaws.com.
    - Record name - www.taesankim.tk
      - Type - A
      - Value/Route traffic to - ~~.elb.amazonaws.com.
    - Record name - img.taesankim.tk
      - Type - A
      - Value/Route traffic to - ~~.cloudfront.net.

<br/>

### ※ 참고
NS, SOA 레코드는 호스팅 영역 생성 시 자동 생성 (여기선 표기 X)

taesankim.tk, www.taesankim.tk 로 접근 시 ALB로 라우팅  
img.taesankim.tk로 접근 시 CloudFront로 라우팅
