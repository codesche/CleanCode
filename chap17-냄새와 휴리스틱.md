## 목차
1. [철학](#1-철학)
2. [공동 창작 매너](#2-공동-창작-매너)
3. [객체 지향 패턴](#3-객체-지향-패턴)
4. [오류 처리](#4-오류-처리)
5. [테스트](#5-테스트)
6. [개선](#6-개선)

## 1. 철학

### 나쁜 코드가 나쁜 이유

![image](https://user-images.githubusercontent.com/110509654/231726921-e71afa1a-e4ba-46a2-9c4c-24cb1add3bb9.png)

**○ 생산성 저하**

나쁜 코드는 팀 생산성을 저하시킨다. 기술부채를 만들어 수정을 더 어렵게 한다.

**○ 클린 코드**

* 성능이 **좋은** 코드
* 의미가 **명확한** 코드 = **가독성**이 좋은 코드
* 중복이 **제거된** 코드
* **생산성 상승**

### 창발적 설계 4번째 규칙, 실용적 관점에서 타협한다

![image](https://user-images.githubusercontent.com/110509654/231727342-ffbf06af-5768-45ae-a5ba-f54dd09f16d0.png)

* 여러가지 규칙에 극단적으로 심취해 클래스와 메서드를 무수하게 만들지 않는다.
* 결국 좋은 코드를 만드는 이유는 생산성을 올리기 위한 것이다.
* 실용적인 관점에서 타협해야 한다.

### 보이스카우트 룰

![image](https://user-images.githubusercontent.com/110509654/231727542-80b0883b-f723-4393-874f-93ae9f8767d7.png)

**전보다 더 깨끗한 코드로 만든다!!**


## 2. 공동 창작 매너

### Team Coding Convention

![image](https://user-images.githubusercontent.com/110509654/231727754-882a0941-c332-47fe-a5b5-a6480164b128.png)


## 3. 객체 지향 패턴

### 캡슐화

**객체의 실제 구현을 외부로부터 감추는 방식**

![image](https://user-images.githubusercontent.com/110509654/231727956-d731a0ca-a903-4c7b-91ad-dce910ed5399.png)

### 외부 코드와 호환하기 - Adapter 패턴

![image](https://user-images.githubusercontent.com/110509654/231728154-22bb82c7-0fb3-482a-bb32-801f324164ef.png)

**외부 코드를 호출할 때, 우리가 정의한 인터페이스 대로 호출하기 위해 사용하는 패턴**

### 높은 결합도, 낮은 응집도

![image](https://user-images.githubusercontent.com/110509654/231728273-e5cb373a-680b-43ec-9ccb-1bcad287a46a.png)

### SOLID 원칙 - 객체 지향 설계의 5가지 원칙

* SRP : 단일 책임 원칙
* OCP : 개방-폐쇄 원칙
* LSP : 리스코프 치환 원칙
* ISP : 인터페이스 분리 원칙
* DIP : 의존성 역전 원칙

**○ SRP(단일 책임 원칙)**

![image](https://user-images.githubusercontent.com/110509654/231728810-eb3c1e86-154f-4cc6-a6db-1dfa7cca0c62.png)

**한 클래스는 하나의 책임만 가져야 한다**

* 클래스는 하나의 기능만 가지며, 어떤 변화에 의해 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 한다.
* SRP 책임이 분명해지기 때문에, 변경에 의한 연쇄작용에서 자유로워질 수 있다.
* 가독성 향상과 유지보수가 용이해진다.
* 실전에서는 쉽지 않지만 늘 상기해야 한다.

**○ OCP(개방-폐쇄 원칙)**

![image](https://user-images.githubusercontent.com/110509654/231729186-a8e334c3-d86b-4ae2-8158-6f2ad6748de2.png)

**소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.**

* 변경을 위한 비용은 가능한 줄이고, 확장을 위한 비용은 가능한 극대화해야 한다.
* 요구사항의 변경이나 추가사항이 발생하더라도, 기존 구성요소에는 수정이 일어나지 않고, 기존 구성 요소를 쉽게 확장해서 재사용한다.
* 객체지향의 추상화와 다형성을 활용한다.

**○ LSP(리스코프 치환 원칙)**

![image](https://user-images.githubusercontent.com/110509654/231729735-19933690-2aff-4f5b-af38-f1132d835ac1.png)

**서브 타입은 언제나 기반 타입으로 교체할 수 있어야 한다.**

* 서브 타입은 기반 타입이 약속한 규약(접근제한자, 예외 포함)을 지켜야 한다.
* 클래스 상속, 인터페이스 상속을 이용해 확장성을 획득한다.
* 다형성과 확장성을 극대화하기 위해 인터페이스를 사용하는 것이 더 좋다.
* 합성(composition)을 이용할 수도 있다.

**○ ISP(인터페이스 분리 원칙)**

![image](https://user-images.githubusercontent.com/110509654/231729864-46c2b049-5c65-4a0f-a78c-1a18804dfab0.png)

**자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다.**

* 최소한의 인터페이스만 구현한다.
* 만약 어떤 클래스를 이용하는 클라이언트가 여러 개고, 이들이 클래스의 특정 부분만 이용한다면, 여러 인터페이스로 분류하여 클라이언트가 필요한 기능만 전달한다.
* SRP가 클래스의 단일 책임이라면, ISP는 인터페이스의 단일 책임.

**DIP(의존성 역전 원칙)**

![image](https://user-images.githubusercontent.com/110509654/231730254-022d1c26-82a4-47ec-93be-99bee020899c.png)

**상위 모델은 하위 모델에 의존하면 안 된다. 둘 다 추상화에 의존해야 한다. 추상화는 세부 사항에 의존해서는 안 된다. 세부 사항은 추상화에 따라 달라진다.**

* 하위 모델의 변경이 상위 모듈의 변경을 요구하는 위계관계를 끊는다.
* 실제 사용관계는 그대로이지만, 추상화를 매개로 메시지를 주고 받으면서 관계를 느슨하게 만든다.

## 4. 오류 처리

### Unchecked Exception을 사용하자

![image](https://user-images.githubusercontent.com/110509654/231730714-63eb31f0-6567-49ed-b627-91045de53494.png)

### Exception 가계도

![image](https://user-images.githubusercontent.com/110509654/231730866-2379c30c-26ec-4269-82f1-468d3d64947e.png)

**Checked vs Unchecked Exception**

* **Exception**을 상속하면 Checked Exception 명시적인 예외처리가 필요하다.
  * 예) IOException, SQLException

* **RuntimeException**을 상속하면 UncheckedException 명시적인 예외처리가 필요하지 않다.
  * 예) NullPointerException, IllegalArgumentException, IndexOutOfBoundException

### 실무 예외 처리 패턴

* getOrElse : 예외 대신 기본값을 리턴한다
  * null이 아닌 기본값, 도메인에 맞는 기본값
* getOrElseThrow : null 대신 예외를 던진다 (기본값이 없을 경우) 

## 5. 테스트

### Test Pyramid

![image](https://user-images.githubusercontent.com/110509654/231742967-459a2ff0-11af-4981-9996-009e06fa7ff6.png)

### First 원칙

![image](https://user-images.githubusercontent.com/110509654/231743033-6a5fd4b1-d328-4f0c-89e0-227ce3591e60.png)

* Fast: 빠르게
  * 테스트는 빨리 돌아야 한다. 자주 돌려야 하기 때문이다.
* Independent: 독립적으로
  * 각 테스트를 독립적으로 작성한다. 서로에게 의존하면 실패한 원인을 찾기 어려워진다. (다른 테스트의 실패로 인한 건지, 코드 오류인지)
* Repeatable: 반복가능하게
  * 테스트는 어떤 환경에서도 반복 가능해야 한다. 실제 환경, QA 환경, 모든 환경에서 돌아가야 한다.
* Self-Validating: 자가검증하는
  * 테스트는 bool 값으로 결과를 내야 한다.
* Timely: 적시에
  * 테스트하려는 실제 코드를 구현하기 직전에 구현한다.

## 6. 개선

### 점진적으로 개선하기

**○ 프로그램을 망치는 가장 좋은 방법 중 하나는 개선이라는 이름 아래 구조를 크게 뒤집는 행위다**

![image](https://user-images.githubusercontent.com/110509654/231743676-5b8a0c8f-fbf2-4b30-8c56-8ee96ea616b6.png)















