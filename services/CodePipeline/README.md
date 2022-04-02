# CodePipeline

## Pipeline
### Pipelines
- Pipeline settings
  - Pipeline name - Pipeline-For-WordPress
  - Service role - New service role
  - Role name - AWSCodePipelineServiceRole
  - Allow AWS CodePipeline to create a service role so it can be used with this new pipeline
- Source
  - Source provider - AWS CodeCommit
  - Repository name - Repository-For-WordPress
  - Branch name - master
- Deploy
  - Deploy provider - AWS CodeDeploy
  - Region - Asia Pacific (Seoul)
  - Application name - WordPress
  - Deployment group - Deployment-Group-For-WordPress

<br/>

### ※ 참고
이 프로젝트에서 Build 과정은 불필요하니 skip
