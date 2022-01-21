빌드 관리 도구란?

- 프로젝트에서 작성한 JAVA 코드와 프로젝트 내에 필요한 각종 xml, properties, jar 파일들을 JVM 이나 WAS가 인식할 수 있도록 패키징 해주는 빌드과정을 자동화 해주는 도구
- 애플리케이션을 개발하면서, 일반적으로 개발에 필요한 다양한 외부 라이브러리들을 다운로드해야한다. 이 때 각 라이브러리들을 번거롭게 모두 다운받을 필요없이, 빌드 도구 설정 파일에 필요한 라이브러리 종류와 버전, 종속성 정보를 명시하여 필요한 라이브러리들을 설정파일을 통해 자동으로 다운로드 해주고 이를 간편히 관리해주는 도구이다.



Maven?

- JAVA용 프로젝트 관리도구
- 빌드중인 프로젝트, 빌드 순서, 다양한 외부 라이브러리 종속성 관계를 pom.xml 파일에 명시한다.
- 외부 저장소에서 필요한 라이브러리와 플러그인을 다운로드 한 다음, 로컬시스템의 캐시에 모두 정리한다.

 

Gradle?

- 프로젝트 빌드 관리 도구
- Groovy언어를 사용한다. (xml 파일을 사용하는 Maven보다 코드가 훨씬 간결하다.)
- Gradle은 프로젝트의 어느 부분이 업데이트되었는지 알기 때문에 빌드에 점진적으로 추가할 수 있다.
- 업데이트가 이미 반영된 빌드의 부분은 더 이상 재실행되지 않는다.(빌드시간이 단축될 수 있다.)

 

Maven vs Gradle

- Gradle은 작업 의존성 그래프를 기반으로 하는 반면 Maven은 고정적이고 선형적인 단계의 모델을 기반으로 한다.
- Gradle은 어떤 task가 업데이트 되었고 안되었는지를 체크하기 때문에 점진적인 빌드를 허용한다. 이미 업데이트된 테스크에 대해서는 작업이 실행되지 않으므로 빌드 시간이 훨씬 단축된다. -> 빌드 설정 규모가 커질수록 Maven과 빌드시간 차이가 커진다.
- Gradle은 병렬에 안전한 캐시를 허용한다. -> 2개 이상의 프로젝트에서 같은 캐시를 사용할 경우 서로 overwirte되지 않도록 checksum기반(중복검사)의 캐시를 사용하고 캐시를     repository와 동기화 시킬 수 있다.

 

 

Gradle 기초 사용법

 

~~~java
repositories {
​	mavenCentral()
}
~~~



 

해당 레포지토리에서 오픈소스 종속성을 다운로드하고 사용할 수 있다.

Spring 에선 주로 mavenCentral() 이 사용된다. Maven Central - 오픈 라이브러리를 호스팅하는 인기있는 저장소

https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:case-for-maven-local

 

~~~groovy
plugins {
	id 'java'
	id 'org.springframework.boot' version '2.1.7.RELEASE'
}
~~~



일반적인 실행을 위한 jar파일

Id를 사용해서 특정 라이브러리를 다운받는다.

version 을 사용해서 세밀하게 컨트롤 가능하다.

https://docs.gradle.org/current/userguide/plugins.html

 

~~~groovy
dependency {
	id 'org.springframework.boot' version '2.1.7.RELEASE'
}
~~~

컴파일 혹은 런타임의 특정 상황에 classPath에서 사용할 수 있도록 프로젝트에서 요구하는 jar파일