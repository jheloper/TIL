# 기본 개념

1995년 제임스 고슬링이 고안한 객체 지향 프로그래밍 언어.

최근, 모바일 플랫폼인 안드로이드의 점유율이 상승하면서 자바 언어의 시장성도 성장하고 있다.

자바는 자바가상머신(Java Virtual Machine, JVM) 위에서 실행, 운영체제에 구애받지 않는 **플랫폼 독립성**을 갖고 있다.

IDE - 통합개발환경, 자바는 주로 [이클립스](www.eclipse.org)를 사용한다.

## 객체 지향 프로그래밍
- 기본 틀을 갖고 손쉽게 확장가능하다.
- 유지보수의 편의성을 가진다.
- 현실세계를 모방하여, 객체들이 서로 "상호작용"하도록 만든 기법.

## 소프트웨어 위기론
- 소프트웨어의 발전이 하드웨어의 발전을 따라가지 못하고
- 소프트웨어의 규모가 커지고
- 소프트웨어 수정, 보완할 것이 많아졌다.
- "소프트웨어의 확장이 계속 가능해야 한다."

## 자바의 3가지 플랫폼
- SE(Standard Edition) - 개인용, 응용프로그램 제작
- EE(Enterprise Edition) - 기업용, 서버사이드프로그램 제작 - 서블릿, JSP 등
- ME(Mobile Edition) - 모바일용 - 안드로이드로 대체

## 기타
- 자바는 임베디드 환경보다는 인터넷 환경에 적절하다.
- 라이브러리 : 소프트웨어 개발에 사용되는 하위 프로그램들의 모임. 공통으로 사용될 수 있는 기능을 모듈화한 것이다.
- JAR : 자바 아카이브 파일. 자바 플랫폼에 소프트웨어나 라이브러리를 배포하기 위한 패키지 파일 포맷이다.
- API : 애플리케이션 프로그램 인터페이스. 소스코드 수준에서 정의되는 인터페이스. API는 사양이기 때문에 구현체와는 독립적이다.
- 소스 코드 : 제작에 사용되는 고급언어 = .java
- 바이트 코드 : 자바의 기계어 = .class
- 소스 코드 파일(.java)를 컴파일(javac.exe)하여 바이트 코드 파일(.class)로 변환. 실행은 자바 런처(java.exe)로 바이트 코드를 실행하는 것이다.

## 리터럴(Literal)

리터럴이란 변수에 들어가는 데이터 값을 말한다. 그 자체로 데이터인 것을 리터럴이라고 한다.

- 정수는 기본 리터럴이 int.
- 소수는 기본 리터럴이 double.
- 리터럴이 double인 소수를 float로 컨버팅하기 위해서는 숫자 뒤에 f를 붙이면 됨. => `예) 3.14; >> 3.14f;`
- "" 가 나온 문자열은 기본 리터럴이 string.
- ''가 나온 문자는 기본 리터럴이 char.
- true, false가 나온 경우는 기본 리터럴이 boolean.
- ""안에서 ""를 사용하고 싶을 때, 이스케이프를 사용한다. (\를 붙여 문법이 아닌 문자로 인식하게 하는 것.)
- ""안에서 여러 줄을 표현하고 싶을 때, /를 사용한다.