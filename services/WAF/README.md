# WAF

## WAF
### Web ACLs
- Name - Web-ACL-for-ALB
  - Resource type - Regional resources
  - Region - Asia Pacific (Seoul)
  - Associated AWS resources - WAS-ALB
  - Rules
    - Core rule set
    - Linux operating system
    - PHP application
    - SQL database
    - WordPress application

- Name - Web-ACL-for-CloudFront
  - Resource type - Regional resources
  - Region - CloudFront distributions
  - Associated AWS resources - cloudfront.taesankim.tk가 대체 도메인으로 되어 있는 배포 선택
  - Rules
    - Core rule set

<br/>

### ※ 참고
Rules는 Add managed rule groups 클릭 후, AWS managed rule groups에서 선택
