## 목차
1. [관심사 분리](#1-관심사-분리)
2. [Dependency Injection](#2-Dependency-Injection)
3. [Cross Cutting Concerns](#3-Cross-Cutting-Concerns)

## 1. 관심사 분리

### 관심사 분리

**construction(생성)과 use(사용)은 아주 다르다**

![image](https://user-images.githubusercontent.com/110509654/228729867-1e078f61-330a-4ad7-bcac-7a2137f609cb.png)

* 소프트웨어 시스템은 (어플리케이션 객체를 제작하고 의존성을 서로 '연결'하는) **준비 과정**과 (준비 과정 이후에 이어지는) **런타임 로직**을 분리해야 한다.
* **객체의 생성과 객체를 사용하는 부분을 분리한다.**

### 시작에 대한 관심사 분리

* 시작 단계는 모든 어플리케이션이 풀어야 할 관심사이다.
* main 함수에서 시스템에 필요한 객체를 생성한 후 어플리케이션에 넘긴다.
* 어플리케이션은 그저 만들어진 객체를 사용한다.
* 모든 객체가 잘 생성되었다는 가정하에 객체를 이용한 개발에 집중할 수 있다.

### 요청에 대한 관심사 분리

**Spring 프레임워크를 통해 요청에 대한 관심사를 분리해 요청 처리에 대한 비즈니스 로직에 집중할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/228730282-cb189ebf-38b9-4514-aab0-f7aad686ab4a.png)

○ Filter, Interceptor, AOP
* 서블릿 필터는 DispatcherServlet 이전에 실행이 되는데 요청 내용을 변경하거나, 요청을 처리하기 전에 작업을 수행할 수 있다.
* Filter와 Interceptor는 Servlet 단위에서 실행된다. 반면 AOP는 메소드 앞에서 Proxy 패턴으로 실행된다.
* 인터셉터는 여러 개를 사용할 수 있고 로그인 처리, 권한체크, 프로그램 실행시간 계산작업, 로그 확인 등의 업무처리에 활용된다.
* AOP는 메서드 앞에서 Proxy 패턴으로 실행된다. 주로 '로깅', '트랜잭션', '에러처리' 등 비즈니스 단의 메서드에서 조금 더 세밀하게 조정하고 싶을 때 사용한다.
  AOP는 주소, 파라미터, 어노테이션 등 다양한 방법으로 대상을 지정할 수 있다.


## 2. Dependency Injection

### Dependency Injection(의존성 주입)

**객체 의존성을 DI 컨테이너에 맡긴다**

![image](https://user-images.githubusercontent.com/110509654/228730787-f9e3bffb-863f-4869-a5e5-8bd00a1102f3.png)

* Setter 메소드 or 생성자 인수를 통해 의존성을 주입한다.
* DI 컨테이너는 요청이 들어올 때 필요한 객체의 인스턴스를 만든 후 의존성을 설정한다.
* ex) Spring IoC Container

### Spring IOC Contatiner

**객체 의존성을 DI 컨테이너에 맡긴다**

![image](https://user-images.githubusercontent.com/110509654/228730938-5e81aa41-95b4-4706-a1f5-b17764f8f0d8.png)


## 3. Cross Cutting Concerns

### Cross Cutting Concerns(횡단 관심 분리)

**어플리케이션 전반에서 가지는 공통적인 관심사를 분리한다**

![image](https://user-images.githubusercontent.com/110509654/228731083-251edb02-cbef-44fc-a31f-f70846fe04c4.png)

* 비즈니스 로직외에 Logging, Transaction 관리, Security 등 신경써야 할 관심사들이 많다.
* 관심사들은 많은 어플리케이션 레이어에 퍼져있는데, 이 관심사들을 분리해 처리하는 것이 효율적이다.

**횡단 관심사 분리의 필요성**

![image](https://user-images.githubusercontent.com/110509654/228731199-8ba8ce1a-fed0-4beb-a414-bae6b62643e3.png)

* **비즈니스 로직에 집중할 수 있다**


### Step1 : Java Proxy API

![image](https://user-images.githubusercontent.com/110509654/228731291-f4f4cec1-ee22-4007-9b9c-4b6248823284.png)

* **Bank 객체에 Proxy API를 통해 영속성을 추가하는 과정**
  * Proxy할 때 가져올 Bank 인터페이스를 만들고, BankImpl이 Bank 인터페이스를 구현한다.

![image](https://user-images.githubusercontent.com/110509654/228731435-f244fb42-41bb-4c23-b03a-90d2dad496e7.png)

* **Bank 객체에 Proxy API를 통해 영속성을 추가하는 과정**
  * Proxy할 때 가져올 Bank 인터페이스를 만들고, BankImpl이 Bank 인터페이스를 구현한다.
  * InvocationHandler를 구현하는 BankProxyHandler를 생성한다. Java Reflection API를 이용해 Bank 인터페이스를 구현하는 객체의 메서드 호출을 가져온다.
    데이터베이스에서 데이터를 가져오는 과정을 추가한다.
  * Proxy API를 호출할 때 BankImpl 객체를 통해 생성한 BankProxyHandler와 Bank 인터페이스를 사용해 프록시된 인터페이스를 사용해 모델과 로직이 분리된 코드를 작성할 수 있다.


### Step2 : 순수 Java AOP Framework

![image](https://user-images.githubusercontent.com/110509654/228731817-401dbfbb-e7aa-4e41-b314-78380071518d.png)


![image](https://user-images.githubusercontent.com/110509654/228731787-48002aa3-1d0c-4e02-954b-851b8d9309ef.png)


* 순수 자바 관점을 구현하는 스프링 AOP, JBoss AOP 프레임워크는 내부적으로 프록시를 사용한다.
* 설정 파일이나 API를 사용해 객체의 역할을 설정한다.
* Bank 객체는 DAO로 프록시되었다.
* 객체를 얻어올 때는 (XML 파일에 설정했던) DI 컨테이너에게 객체를 요청(getBean) 한다.

### Step3 : EJB3 - JPA같은 객체 영속성 관리 표준 API

![image](https://user-images.githubusercontent.com/110509654/228732008-7ef7c649-4113-41ca-9a4f-8123f6893d46.png)

* 모든 정보가 annotation 속에 있어서 코드 자체가 깔끔하고 가독성이 좋다.
* annotation에 있는 영속성 정보 전부 또는 일부를 XML 설정으로 옮겨도 된다.
(실무에서는 annotation 사용을 더 선호한다)


