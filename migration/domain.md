## Domain Migration

### 사전 작업
- Hosting 중인 Domain name 존재. ex) taesankim.tk

<br/>

### 과정
#### 1. Route 53에서 Hosting Zone 생성
- Hosting 중인 Domain name과 같은 이름의 hosting zone 생성

#### 2. Records 생성
- 기존에 hosting 중인 records를 Route 53에서 생성한 hosting zone에 똑같이 A records로 생성

#### 3. NS record 업데이트
- 기존 hosting 중인 NS records를 Route 53에서 생성한 hosting zone의 NS records로 업데이트

<br/>

### ※ 참고
Records가 많을 경우엔 기존 hosting records의 집합인 영역 파일을 다운받아 사용  
NS record를 업데이트 할 때 오랜 시간이 소요될 수 있으니, A records를 미리 hosting zone에 생성해 둘 것
