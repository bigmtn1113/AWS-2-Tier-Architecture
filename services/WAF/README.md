# WAF

## WAF
### Web ACLs
- Web ACL details
  - Name - ts-prd-pub-taesankim-tk-lb-waf
  - Resource type - Regional resources
  - Region - Asia Pacific (Seoul)
  - Associated AWS resources - ts-prd-pub-taesankim-tk-lb
  - Rules
    - AWS managed rule groups
      - Core rule set
      - Linux operating system
      - PHP application
      - SQL database
      - WordPress application

--
- Web ACL details
  - Name - ts-prd-img-taesankim-tk-cf-waf
  - Resource type - CloudFront distributions
  - Region - Global (CloudFront)
  - Associated AWS resources - img.taesankim.tk
  - Rules
    - AWS managed rule groups
      - Core rule set

<br/>

### ※ 참고
Rules는 Add managed rule groups 클릭 후, AWS managed rule groups에서 선택
