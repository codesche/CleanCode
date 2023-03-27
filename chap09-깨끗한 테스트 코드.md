## 목차
1. [테스트 코드의 중요성](#1-테스트-코드의-중요성)
2. [테스트의 종류](#2-테스트의-종류)
3. [Unit Test의 작성](#3-Unit-Test-작성)
4. [FIRST 원칙](#4-FIRST-원칙)
5. [오픈소스 속 Unit Test](#5-오픈소스-속-Unit-Test)

## 1. 테스트 코드의 중요성

![image](https://user-images.githubusercontent.com/110509654/227957212-45e4f9cf-4777-4a21-977a-77b2970b2477.png)

* 테스트 코드는 실수를 바로잡아준다.
* 테스트 코드는 반드시 존재해야 하며, 실제 코드 못지 않게 중요하다.
(테스트 코드 짜는 연습을 많이 해야 함)
* **테스트 케이스는 변경이 쉽도록 한다.** 코드에 유연성, 유지보수성, 재사용성을 제공하는 버팀목이 바로 단위테스트다. 
  테스트 케이스가 있으면 변경이 두렵지 않다. 테스트 케이스가 없다면 모든 변경이 잠정적인 버그다. 테스트 커버리지가 높을수록
  버그에 대한 공포가 줄어든다.
* 지저분한 테스트 코드는 테스트를 안하는 것만도 못하다.

![image](https://user-images.githubusercontent.com/110509654/227958316-12755be2-d5ce-46ab-a3e2-a5d176093d1f.png)


**테스트는 자동화되어야 한다.**

![image](https://user-images.githubusercontent.com/110509654/227958529-de386f78-06ef-4179-a3c4-fe134870b362.png)


## 2. 테스트의 종류

![image](https://user-images.githubusercontent.com/110509654/227958673-73876520-7d4e-474f-8f18-c985072fcbb3.png)

* Unit Test: 프로그램 내부의 개별 컴포넌트의 동작을 테스트한다. 배포하기 전에 자동으로 실행되도록 많이 사용한다.
* Integration Test: 프로그램 내부의 개별 컴포넌트들을 합쳐서 동작을 테스트한다. Unit Test는 각 컴포넌트를 고립시켜
테스트하기 때문에 컴포넌트의 interaction을 확인하는 Integration Test가 필요하다.
* E2E Test: End to End Test. 실제 유저의 시나리오대로 네트워크를 통해 서버의 EndPoint를 호출해 테스트한다.


## 3. Unit Test 작성

|테스트 라이브러리|내용|
|:---:|:---:|
|![image](https://user-images.githubusercontent.com/110509654/227959844-5376e360-f8f9-409b-96f5-2a918ec6e194.png)|![image](https://user-images.githubusercontent.com/110509654/227959915-bba9c8a7-2352-4718-8a4a-cd298cd8c1c4.png)|

=> JUnit5 + mockito를 많이 사용한다

**Test Double**

![image](https://user-images.githubusercontent.com/110509654/227960146-ee31d8db-8293-4902-8a97-f1ef7b1b7b70.png)

**○ Stub**
* 원래의 구현을 최대한 단순한 것으로 대체한다.
* 테스트를 위해 프로그래밍된 항목에만 응답한다.

**○ Spy**
* Stub의 역할을 하면서 호출에 대한 정보를 기록한다.
* 이메일 서비스에서 메세지가 몇 번 전송되었는지 확인.

**○ Mock**
* 행위를 검증하기 위해 가짜 객체를 만들어 테스트하는 방법
* 호출에 대한 동작을 프로그래밍할 수 있다.
* Stub은 상태를 검증하고 Mock은 행위를 검증한다.


### give-when-then 패턴을 사용하자

![image](https://user-images.githubusercontent.com/110509654/227961012-b0e48998-466b-4e1d-abe9-6c8b35f240f5.png)

* **given:** 테스트에 대한 pre-condition
* **when:** 테스트하고 싶은 동작 호출
* **then:** 테스트 결과 확인

**Spring Boot Application Test 예제**

![image](https://user-images.githubusercontent.com/110509654/227961410-a62bf93a-c062-46a2-8421-874cbcefee30.png)

**ExampleController - main 코드**

![image](https://user-images.githubusercontent.com/110509654/227961567-edd3727c-441f-4edd-a1f3-5c95e6159b00.png)

**ExampleController - Unit Test**

![image](https://user-images.githubusercontent.com/110509654/227961696-c1d1bc69-0059-4039-969c-55035d2868a9.png)

![image](https://user-images.githubusercontent.com/110509654/227961913-0a4e5d08-f552-45b3-a7ed-6be56f6fd97c.png)

* PersonRepository mock 사용
* given-when-then 구조
* repository에서 값을 읽어왔을 때와 읽어오지 못했을 때 2가지 경우를 테스트

**Integration Test(Database)**

![image](https://user-images.githubusercontent.com/110509654/227962057-0eea92b5-7f73-47d8-8292-864431cc1bed.png)

![image](https://user-images.githubusercontent.com/110509654/227962305-ed1422bd-9798-4f80-87f4-f7e76528b508.png)


* PersonREpository이 데이터베이스와 연결될 수 있는지 확인
* in-memory DB인 h2로 테스트
* findByLastName가 정상적으로 동작하는지 확인


**Integration Test(Service)**

![image](https://user-images.githubusercontent.com/110509654/227962482-8adf6c76-23fe-492f-9424-7917da75aab3.png)

![image](https://user-images.githubusercontent.com/110509654/227962561-230b9292-21dd-49db-95b6-d6e4957539ad.png)

* WireMock을 이용해 mock 서버를 띄운다.
* client가 실제 서버가 아닌 mock 서버로 요청하게 해서 client의 동작을 테스트한다.


## 4. FIRST 원칙

![image](https://user-images.githubusercontent.com/110509654/227962965-21d82c78-6087-4cf9-9279-ea073d0d6baa.png)

* **Fast: 빠르게**
  * 테스트는 빨리 돌아야 한다. 자주 돌려야 하기 때문이다.

* **Independent: 독립적으로**
  * 각 테스트를 독립적으로 작성한다. 서로에게 의존하면 실패한 원인을 찾기 어려워진다. (다른 테스트의 실패로 인한건지, 코드 오류인지)

* **Repeatable: 반복가능하게**
  * 테스트는 어떤 환경에서도 반복 가능해야 한다. 실제 환경, QA 환경, 모든 환경에서 돌아가야 한다.

* **Self-Validating: 자가검증하는**
  * 테스트는 bool값으로 결과를 내야 한다.

* **Timely: 적시에**
  * 테스트하려는 실제 코드를 구현하기 직전에 구현한다. 


## 5. 오픈소스 속 Unit Test

**Trino (PrestoSQL)**

![image](https://user-images.githubusercontent.com/110509654/227963877-ddcc4ea0-a76a-4b0b-8a8f-24c43ad40f0d.png)

* calculateLiteralValue를 테스트하고 있다.
* 호출과 동시에 assert로 결과값을 검증한다.
* 테스트 하나에 여러 assert가 사용된다. 책에서 권장하는 방식이 아니지만, '조건'을 달리하며 테스트 하는 경우 많이 사용된다.
* 테스트 클래스명이 Test로 시작한다. 원래 ~Test로 끝나는 게 일반적이다. 팀 간의 컨벤션이 일반적인 컨벤션보다 우선이다.


**Junit5 Samples**

![image](https://user-images.githubusercontent.com/110509654/227964546-8970ae5d-90a8-4d74-be3b-cbdda0e5767f.png)

* @DisplayName은 테스트 클래스나 메서드에 보여질 이름을 입력하는 것이다. 테스트의 목적을 명확하게 작성할 수 있다.
* @ParameterizedTest는 하나의 테스트 메서드로 여러 가지 parameter를 테스트할 수 있다. @CsvSource의 값을 parameter로 넘긴다.
* JUnit5가 테스트에 관한 유용한 기능을 많이 가지고 있기 때문에 실무에서 많이 사용한다.





