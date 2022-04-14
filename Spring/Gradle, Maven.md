# **Gradle과 Maven의 개념 및 차이**

## **Gradle 이란?**

- Groovy 기반의 빌드, 프로젝트 구성/관리, 테스트, 배포 도구
- 빌드 속도가 Maven에 비해 10~100배 가량 빠름

Groovy: JVM에서 실행되는 스크립트 언어이며, JVM에서 동작하지만 Java와 달리 소스 코드를 컴파일할 필요가 없다.

## **Gradle의 장점**

- 직관적인 코드와 자동완성
- 다양한 Repository 사용 가능
- 각 작업에 필요한 라이브러리들만 가져오는 작업

## **Gradle이 빌드 속도가 빠른 이유**

- 점진적 빌드(Incremental Build): Gradle은 이미 빌드된 파일들을 모두 빌드하는 것이 아니라 바뀐 파일들만 빌드한다.
- Build Cache: 만약 두 개 이상의 빌드가 돌아가고, 하나의 빌드에서 사용되는 파일들이 다른 빌드들에 사용된다면 Gradle은 빌드 캐시를 이용해 이전 빌드의 결과물을 다른 빌드에서 사용할 수 있다. 이로 인해 다시 빌드하지 않아도 되어 빌드 시간이 줄어들게 된다.
- Daemon Process: 데몬 프로세스는 서비스의 요청에 응답하기 위해 오랫동안 살아있는 프로세스인데, Gradle의 데몬 프로세스는 메모리 상에 빌드 결과물들을 보관한다. 이로 인해 한번 빌드된 프로젝트는 다음 빌드시 매우 적은 시간만 소요된다.

## **build.gradle**

build.gradle 은 gradle에서 빌드 작업에 필요한 기본 설정, 동작 등을 정의하는 파일이다.

예시)

```Java
plugins {
        id 'org.springframework.boot' version '2.3.1.RELEASE'
        id 'io.spring.dependency-management' version '1.0.9.RELEASE'
        id 'java'
    }

    group = 'com.example'
    version = '0.0.1-SNAPSHOT'
    sourceCompatibility = '1.8'

    configurations {
        compileOnly {
            extendsFrom annotationProcessor
        }
    }

    repositories {
        mavenCentral()
    }

    dependencies {
        implementation 'org.springframework.boot:spring-boot-starter-data-jdbc'
        implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
        implementation 'org.springframework.boot:spring-boot-starter-oauth2-client'
        implementation 'org.springframework.boot:spring-boot-starter-security'
        implementation 'org.springframework.boot:spring-boot-starter-web'
        implementation 'org.springframework.kafka:spring-kafka'
        annotationProcessor 'org.projectlombok:lombok'
        testImplementation('org.springframework.boot:spring-boot-starter-test') {
            exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
        }
        testImplementation 'org.springframework.kafka:spring-kafka-test'
        testImplementation 'org.springframework.security:spring-security-test'
    }

    test {
        useJUnitPlatform()
    }
```

- plugins: 프로젝트를 빌드하기 위해 필요한 작업들을 지원하는 플러그인 설정이다.

- repositories: 저장소로 관리하는 블록이며, 필요한 라이브러리들을 다운로드하기 위해 사용된다.
  jCenter(), mavenCentral()은 Gradle의 메소드이며, 이 둘이 주로 사용된다.

- dependencies: 의존성에 관한 설정을 관리하는 블록이며, 필요한 라이브러리의 정보를 입력하면 해당 라이브러리를 사용할 수 있다.

  - implementation: 런타임시 사용
  - testImplementation: 테스트 컴파일시 사용

- ext: gradle의 모든 task에서 사용할 수 있는 일종의 전역 변수를 선언하는 블록이다.

- settings.gradle: 여러가지로 사용할 수 있지만 대부분 멀티 모듈을 사용할때 설정한다.

<br>

## **Maven 이란?**

- POM(Project Object Model)을 사용
  - 프로젝트 정보: 프로젝트 이름, 라이선스 등
  - 빌드 설정: 소스, 리소스, 라이프사이클별 실행한 플러그인 등 빌드와 관련된 설정
  - 빌드 환경: 사용자 환경 별로 달라질 수 있는 프로파일 정보
  - POM 연관 정보: 의존 프로젝트(모듈), 상위 프로젝트, 포함하고 있는 하위 모듈 등
- Java용 프로젝트 관리 도구로 Apache의 Ant 대안으로 출시

## **Maven의 장점**

- Gradle을 사용합시다.
