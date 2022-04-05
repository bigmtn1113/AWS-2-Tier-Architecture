# CodePipeline

## Pipeline
### Pipelines
- Pipeline settings
  - Pipeline name - ts-prd-taesankim.tk-asg-pipeline
  - Service role - New service role
  - Role name - AWSCodePipelineServiceRole-ts-prd-taesankim.tk-asg-pipeline
  - Allow AWS CodePipeline to create a service role so it can be used with this new pipeline
- Source
  - Source provider - AWS CodeCommit
  - Repository name - ts-prd-taesankim.tk-repo
  - Branch name - master
- Deploy
  - Deploy provider - AWS CodeDeploy
  - Region - Asia Pacific (Seoul)
  - Application name - ts-prd-pri-taesankim.tk-app
  - Deployment group - ts-prd-pri-taesankim.tk-asg-dg

<br/>

### ※ 참고
이 프로젝트에서 Build 과정은 불필요하니 skip
