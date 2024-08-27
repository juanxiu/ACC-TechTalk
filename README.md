# ACC-TechTalk

### 1. ECR 리포지토리에 도커 이미지 푸쉬
- 로컬에서 컨테이너 띄우고 애플리케이션 테스트 후 ECR에 이미지 푸쉬하기. 
### 2. ECS 구성 
- Task Definition 생성
  - 컨테이너 구성에서 ECR 리포지토리의 이미지 URI 를 넣기.
  - 컨테이너 포트 번호는 스프링부트 애플리케이션이므로 8080 으로 설정하기.
- ECS Cluster 생성
- ECS Service 생성
  - 네트워킹에서 ECS Service 보안그룹은 로드밸런서 소스에 대한 TCP 8080와 0.0.0.0/0에 대한 HTTP 80 포트를 인바운드 규칙으로 허용할 것.
  - 그리고 VPC와 AZ가 서로 다른 Private Subnet 을 선택하기.
  - 로드밸런서는 ALB, 리스너는 80포트, 보안그룹은 8080 포트를 인바운드 규칙으로 허용할 것.
 
### 3. 배포 성공 
- 로드밸런서 DNS 네임으로 애플리케이션 배포 성공

### 4. 에러 
- 로드밸런서 대상그룹 unhealthy 이슈
- 해결: 보안그룹의 인바운드 규칙 문제
  
→ 컨테이너에서 호스트 포트와 컨테이너 포트 8080으로 바꿈. 

→ 로드밸런서 보안그룹을 포트 번호 8080으로 바꿈. (로드밸런서 리스너는 80임)

→ ecs 보안그룹도 인바운드 규칙에 8080 포트 추가해줌. 

→ 새 서비스 생성해서 ecs 보안그룹, 로드밸런서 다시 지정해줌.

<img width="924" alt="%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-08-18%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%204 31 31" src="https://github.com/user-attachments/assets/b2181a7f-fcd3-46cd-8c1d-bbb49a4f430a">


