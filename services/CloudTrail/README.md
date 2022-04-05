# CloudTrail

## CloudTrail
### Trails
- Trail attributes
  - General details
    - Trail name - ts-cloudtrail
    - Storage location - Create new S3 bucket
    - Log file SSE-KMS encryption - Not enabled
  - CloudWatch Logs
    - CloudWatch Logs - Enabled
    - Log group - New
    - IAM Role - New
    - Role name - CloudTrailRoleForCloudWatchLogs_ts-cloudtrail
- Log events
  - Events
    - Event type
      - Management events
  - Management events
    - API activity
      - Read
      - Write

<br/>

### ※ 참고
CloudWatch는 AWS 서비스 및 리소스의 활동에 중심적으로 상태 및 성능 보고. 무슨 일이 일어나고 있는가  
CloudTrail은 AWS 계정의 API 활동을 기록하는 웹 서비스. 누가 무엇을 하는가
