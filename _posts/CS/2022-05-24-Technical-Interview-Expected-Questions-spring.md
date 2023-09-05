---
title: '[기술 면접] Spring 정리'
layout: post
categories: 기술면접
tags: 기술면접
comments: true
---

<details>
<summary> <b> Spring이란?  </b> </summary>
<div markdown="1">

- 자바 오픈소스 프레임워크 중 하나이다.
- 스프링 컨테이너로 자바 객체를 관리하며 DI와 IoC를 통해 결합도를 낮출수 있다.
- AOP를 통해 공통 기능을 분리하여 관리할 수 있다.

</div>
</details>

<details>
<summary> <b> Spring DI/IoC는 동작방식  </b> </summary>
<div markdown="1">

스프링 프레임워크는 느슨한 결합을 기반으로 동작한다.
ioC 컨테이너를 통해 객체 간의 의존성을 주입하면서 느슨한 결합을 유지할 수 있다.

- **의존성 주입(Dependency Inject)**
  - 객체가 필요로 하는 의존성을 직접 생성하거나 참조하지 않고, 빈 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것

- **제어의 역전(Inversion Of Control)**
  - 개발자가 객체 간의 의존성을 관리하는 코드를 작성하는 것이 아닌, 프레임워크가 의존성 관리를 대신 수행하는 것

- 스프링 DI 과정       
  1) 스프링 컨테이너가 객체 생성을 위해 빈을 생성     
  2) 빈이 생성된 후, 스프링은 빈이 의존하는 다른 빈들을 찾아 의존성 주입 수행     
  3) 의존성 주입이 완료된 빈은 초기화됨       
  4) 빈이 더이상 필요하지 않으면 destory 메서드를 호출하여 빈을 종료한다.     

</div>
</details>

<details>
<summary> <b> 의존성 주입 방법  </b> </summary>
<div markdown="1">

- **생성자 주입**:
  - 생성자 호출시점에 딱 1번만 호출되는 것을 보장하며 불변, 필수 의존관계에 사용

- **Setter 주입**:
  - 선택, 변경 가능성이 있는 의존관계에 사용되며 스프링빈을 선택적으로 등록 가능

- **필드 주입**:
  - @Autowired를 사용하는데 외부에서 변경이 불가능하여 테스트하기가 힘듦
  - 주로 테스트코드에서 사용된다.

</div>
</details>

<details>
<summary> <b> Bean이란?  </b> </summary>
<div markdown="1">

- 스프링 컨테이너 안에 들어있는 객체로 필요할때 스프링 컨테이너에서 가져와 사용한다.
- @Bean 어노테이션을 사용하거나 xml설정을 통해 일반 객체를 Bean으로 등록할 수 있다.

- Bean 생성 과정     
  1) 스프링 컨테이너 생성     
  2) 스프링 빈 생성     
  3) 의존 관계 주입    
  4) 초기화 콜백(@PostConstruct)   
  5) 사용   
  6) 소멸 전 콜백(@PreDestroy)  
  7) 종료

</div>
</details>

<details>
<summary> <b> Bean의 Scope 설명  </b> </summary>
<div markdown="1">

- 빈 스코프는 빈이 존재할 수 있는 범위를 뜻하며 싱글톤, 프로토타입, request, session, application 등이 있다.
- 싱글톤은 기본 스코프로 스크링 컨테이너 시작과 종료까지 유지되는 가장 넓은 범위의 스코프이다.
- 프로트타입은 빈의 생성과 의존관계 주입까지만 관여하고 더는 관리하지 않는 매우 짧은 범위의 스코프이다.

</div>
</details>

<details>
<summary> <b> @Bean과 @Component 차이  </b> </summary>
<div markdown="1">

- **@Bean**:
  - 외부 라이브러리를 Bean으로 등록하고 싶은 경우 사용
  - 메서드 레벨에만 적용 가능

- **@Component**:
  - 클래스 레벨에만 적용 가능
  
</div>
</details>




## 참고
- [백엔드 개발자로 입사를 준비하며 받았던 질문, 예상했던 질문, 인터넷 참고한 질문(CC BY-NC)](https://github.dev/ksundong/backend-interview-question)