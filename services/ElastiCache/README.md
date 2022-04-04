# ElastiCache

## ElastiCache
### Redis
- Cluster engine - Redis
- Location - Amazon Cloud
- Redis settings
  - Name - ts-prd-pri-taesankim-tk-redis
  - Engine version compatibility - 6.2
  - port - 6379
  - Parameter group - taesankim.tk-6.x
  - Node type - cache.t4g.small
  - Number of replicas - 2
  - Multi-AZ
- Advanced Redis settings
  - Subnet group - redis-subnet-group
- Security
  - Security groups - ElastiCache-For-Redis-SG

### Parameter groups
- Family - redis6.x
- Name - taesankim.tk-6.x

### Subnet groups
- Name - ts-prd-pri-redis
- VPC ID - VPC
- Availability Zone or Outpost, Subnet ID
  - ap-northeast-2a, 10.0.40.0/24
  - ap-northeast-2c, 10.0.41.0/24

<br/>

### ※ 참고
**사용자 세션 관리** 목적으로 주로 사용  
WordPress가 느리기 때문에 **인메모리 캐시**인 ElastiCache for Redis를 사용하면 더 빠르게 이용 가능  
WordPress에서 Redis Object Cache 플러그인 설치 후, 연결
