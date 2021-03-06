# Docker, Kubernetes, VM의 개념과 차이

## Docker란?

- 컨테이너 기반의 가상화 플랫폼

**Containter란?**

- App & App을 구동하는 환경을 격리한 공간

**Docker의 사용 목적**

- 컨테이너를 활용하여 빌드, 배포, 실행을 단순화
- 대규모 서비스에서는 개발 서버와 운영 서버의 환경을 개발 환경과 동일하게 맞춰야 하는데, Docker의 컨테이너로 해결

**Docker 배포 방법**

- 배포할 파일 빌드 (maven install)
- Docker 빌드
- Docker 이미지 생성
- Shell script로 컨테이너 실행

**Docker vs VM**

- VM은 컴퓨터 리소스를 고정적으로 분할하여 사용하고, Docker는 필요한 만큼만 컨테이너에 할당하여 사용하기 때문에 자원을 효율적으로 사용할 수 있다.
- VM은 환경을 확실히 분리해주긴 하지만 컴퓨터 리소스를 고정적으로 분할해서 사용하기 때문에 A가 40% B가 50%의 리소스를 사용하게 된다면 추후 추가하는 C는 리소스를 10%밖에 사용하지 못함

**Docker vs k8s**

- Docker는 이미지를 컨테이너에 띄우고 실행하는 기술
- k8s는 도커를 기반으로 컨테이너를 관리하는 서비스

**k8s(kubernetes)란?**

- 다수의 컨테이너를 자동으로 운영하기 위한 오케스트레이션 도구

**오케스트레이션이란?**

- 다수의 컨테이너를 관리하는 시스템

**k8s의 특징**

- 자동화된 도구(self-healing): 컨테니어들을 모니터링하며 하나라도 죽으면, 그것을 빠르게 재시작 시킴
- 로드 밸런싱: 트래픽이 과도하게 몰릴 경우 k8s가 자동으로 새로운 컨테이너를 만들 수 있음
- 무중단 서비스: 기업에서는 서버 업데이트를 위해 사용자들의 이용량이 적은 새벽 시간을 활용하는데, k8s는 점진적 업데이트를 제공하기 때문에 서비스 중단 없이 어플리케이션을 업데이트 할 수 있음
- 호환성: AWS -> GCP와 같이 구축된 환경을 이전하고 싶을 때, 컨테이너 기반으로 구성 되어 있기 때문에 자유롭게 환경 이전이 가능
