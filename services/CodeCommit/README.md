# CodeCommit

## Source
### Repositories
- Repository settings
  - Repository name - ts-prd-taesankim.tk-repo

<br/>

### ※ 참고
WordPress 디렉터리(/var/www/html/wordpress)와 연결  
/var/www/html/wordpress에서 변경 사항 적용 후, git push 하면 CodeCommit으로 변경 사항이 저장됨

CodeDeploy를 이용하여 배포할 경우 CodeCommit Repository에 appspec.yml 파일이 있어야 함  
scripts 파일들을 참조할 경우 scripts 파일의 경로를 appspec.yml에 명시해야 하며, scripts 파일들도 CodeCommit에 있어야 함

[CodeCommit 사용법 참고](https://github.com/kva231/Cloud-System-Engineer-Study/blob/master/05.%20AWS/%EA%B8%B0%ED%83%80/Linux%EC%97%90%EC%84%9C%20CodeCommit%20%EC%82%AC%EC%9A%A9.md)  
[CodeDeployDemoFiles 참고](https://github.com/kva231/CodeDeployDemoFiles)
