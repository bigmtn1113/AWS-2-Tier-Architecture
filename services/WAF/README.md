# WAF

## WAF
### Web ACLs
- Name - ts-prd-pub-taesankim.tk-lb-waf
  - Resource type - Regional resources
  - Region - Asia Pacific (Seoul)
  - Associated AWS resources - ts-prd-pub-taesankim.tk-lb
  - Rules
    - Core rule set
    - Linux operating system
    - PHP application
    - SQL database
    - WordPress application

- Name - ts-prd-img.taesankim.tk-cf-waf
  - Resource type - Regional resources
  - Region - CloudFront distributions
  - Associated AWS resources - img.taesankim.tk
  - Rules
    - Core rule set

<br/>

### ※ 참고
Rules는 Add managed rule groups 클릭 후, AWS managed rule groups에서 선택
