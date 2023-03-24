## 목차
1. [예외 처리 방식](#1-예외-처리-방식)
2. [Unchecked Exception을 사용하라](#2-Unchecked-Exception을-사용하라)
3. [Exception 잘 쓰기](#3-Exception-잘-쓰기)
4. [실무 예외 처리 패턴](#4-실무-예외-처리-패턴)
5. [오픈소스 속 Exception 살펴보기](#5-오픈소스-속-Exception-살펴보기)

## 1. 예외 처리 방식
**○ 오류 코드를 리턴하지 말고, 예외를 던져라**

![image](https://user-images.githubusercontent.com/110509654/227426127-d954da58-abb8-43a1-9d23-2388ad0628d3.png)

* 옛날에는 오류를 나타낼 때 에러코드를 던졌다.
* 하지만 예외를 던지는 것이 명확하고, 처리 흐름이 깔끔해진다.


**○ 예외를 던지고, 처리하는 방식**

![image](https://user-images.githubusercontent.com/110509654/227426486-917e026b-5b9a-4889-be2d-97ca4e99e5b9.png)

* 오류가 발생한 부분에서 예외를 던진다.
  * 별도의 처리가 필요한 예외라면 checked exception으로 던진다.
* checked exception에 대한 예외처리를 하지 않는다면 메서드 선언부에 throws를 명시해야 한다.
* 예외를 처리할 수 있는 곳에서 catch하여 처리한다.

## 2. Unchecked Exception을 사용하라
**○ Exception 가계도**

![image](https://user-images.githubusercontent.com/110509654/227426802-860187e5-c857-4197-8053-7645266f1a94.png)

**Checked vs Unchecked Exception**
* **Exception**을 상속하면 Checked Exception 명시적인 예외처리가 필요하다.
  * 예) IOException, SQLException
* **RuntimeException**을 상속하면 UncheckedException 명시적인 예외처리가 필요하지 않다.
  * 예) NullPointerException, IllegalArgumentException, IndexOutOfBoundException

**○ [Effective Java] Exception에 관한 규약**

자바 언어 명세가 요구하는 것은 아니지만, 업계에 널리 퍼진 규약으로 Error 클래스를 상속해 하위 클래스를 만드는 일은 자제한다.
즉, 사용자가 직접 구현하는 unchecked throwable은 모두 RuntimeException의 하위 클래스여야 한다.

Exception, RuntimeException, Error를 상속하지 않는 throwable을 만들 수도 있지만, 이러한 throwable은 정상적인 사항보다 나을 게
하나도 없기 때문에 API 사용자를 헷갈리게 할 뿐이므로 절대 사용하지 않는다.


**○ Checked Exception이 나쁜 이유**

![image](https://user-images.githubusercontent.com/110509654/227427499-bad3bc94-371e-4df0-9666-f031eba24f67.png)

1. 특정 메소드에서 checked exception을 throw하고 상위 메소드에서 그 exception을 catch한다면 모든 중간단계 메소드에 exception을 throw 해야 한다.
2. OCP(개방 폐쇄 원칙) 위배 - 상위 레벨 메소드에서 하위 레벨 메소드의 디테일에 대해 알아야 하기 때문에 OCP 원칙에 위배된다.
3. 필요한 경우 checked exception을 사용해야 되지만 일반적인 경우 득보다 실이 많다.


**○ Unchecked Exception을 사용하자**

안정적인 소프트웨어를 제작하는 요소로 확인된 예외가 반드시 필요하지 않다는 사실이 분명해졌다. C#은 확인된 예외를 지원하지 않는다.
영웅적인 시도에도 불구하고 C++ 역시 확인된 예외를 지원하지 않는다. 파이썬이나 루비도 마찬가지다.
**그럼에도 불구하고 C#, C++, 파이썬, 루비는 안정적인 소프트웨어를 구현하기에 무리가 없다.**


## 3. Exception 잘 쓰기

**○ 예외에 메세지를 담아라**

![image](https://user-images.githubusercontent.com/110509654/227428104-580f8859-fa06-417f-8e52-3896f00e3817.png)


**예외에 의미있는 정보 담기**
* 오류가 발생한 원인과 위치를 찾기 쉽도록, 예외를 던질 때는 전후 상황을 충분히 덧붙인다.
* 실패한 연산 이름과 유형 등 정보를 담아 예외를 던진다.


**○ exception wrapper**

![image](https://user-images.githubusercontent.com/110509654/227428319-407226b9-5305-4512-8801-0e04447a1bf3.png)

![image](https://user-images.githubusercontent.com/110509654/227428354-1b894919-fbd8-4bcb-86af-f00ef5d2c8ea.png)

**예외를 감싸는 클래스를 만든다**
* port.open()시 발생하는 checked exception들을 감싸도록 port를 가지는 LocalPort 클래스를 만든다.
* port.open()이 던지는 checked exception들을 하나의 PortDeviceFailure exception으로 감싸서 던진다.


## 4. 실무 예외 처리 패턴

**실무 예외 처리 패턴**
* **getOrElse** : 예외 대신 기본값을 리턴한다
  * null이 아닌 기본값
  * 도메인에 맞는 기본값


(1) null이 아닌 기본값을 리턴한다

![image](https://user-images.githubusercontent.com/110509654/227428810-293b49a0-6fe4-449f-9090-65686dbc503a.png)

![image](https://user-images.githubusercontent.com/110509654/227428838-552434dd-2a1d-46f8-9e89-6425d52a5fde.png)


(2) 도메인에 맞는 기본값을 가져온다

![image](https://user-images.githubusercontent.com/110509654/227428978-3078d939-019b-4ccf-bae9-00763b896249.png)

![image](https://user-images.githubusercontent.com/110509654/227429019-72d488f3-f9ce-4081-839b-b46833355e29.png)


* **getOrElseThrow** : null 대신 예외를 던진다 (기본값이 없다면)

(1) null 체크 지옥에서 벗어나자

![image](https://user-images.githubusercontent.com/110509654/227429160-cd4927a1-38b2-4ac1-a87d-6ace6b3328b4.png)

(2) 기본값이 없을 때는 null 대신 예외를 던진다

![image](https://user-images.githubusercontent.com/110509654/227429237-7ad0b39c-3589-4cdd-9dee-bf232b0438b4.png)

![image](https://user-images.githubusercontent.com/110509654/227429354-a0a9df8d-97df-4bf6-8b3b-b8774d7af2c2.png)

(3) 파라미터의 null을 점검하라

![image](https://user-images.githubusercontent.com/110509654/227429406-f47bae12-d0c8-46f4-b8d6-d4d24ffe1299.png)

![image](https://user-images.githubusercontent.com/110509654/227429442-012ef93f-e7c7-4faa-ad7a-9aebac27d81f.png)

![image](https://user-images.githubusercontent.com/110509654/227429472-5d48bd40-a8dd-4622-981f-2051b36be1c1.png)


**실무에서는 보통 자신의 예외를 정의한다**

![image](https://user-images.githubusercontent.com/110509654/227429528-7ed0adc8-9cfe-4693-bdc8-231bd98cf505.png)

* 에러 로그에서 stacktrace 해봤을 때 우리가 발생시킨 예외라는 것을 바로 인지할 수 있다.
* 다른 라이브러리에서 발생한 에러와 섞이지 않는다. 우리도 IllegalArgumentException을 던지는 것보다 우리 예외로 던지는 게 어느 부분에서
  에러가 났는지 파악하기에 용이하다.
* 우리 시스템에서 발생한 에러의 종류를 나열할 수 있다.


## 5. 오픈소스 속 Exception 살펴보기

**apps-android-commons**

![image](https://user-images.githubusercontent.com/110509654/227429745-a2253d3b-e5e2-412c-b0a8-1d9920ca186b.png)

1. parameter인 bookmark가 null이면 예외를 던지지 않고 false를 리턴한다 -> bookmark 존재여부에 대한 메서드의 목적에 부합한다.
2. db 리소스를 처리할 때 checked exception인 RemoteException을 별도로 처리하지 않고 RuntimeException으로 바꿔서 던졌다.
3. finally 블록에서 리소스를 close 처리한다 (리소스를 사용했다면 반드시 finally 블록에서 닫아줘야 한다).

**Elastic Search**

![image](https://user-images.githubusercontent.com/110509654/227429998-f2fbd983-e4e4-474b-a21d-f15ab2b9ab44.png)

![image](https://user-images.githubusercontent.com/110509654/227430153-e91506b9-6495-47b0-974b-383419663a22.png)

![image](https://user-images.githubusercontent.com/110509654/227430196-2f7cb266-9ab0-4631-906a-42479d774e66.png)

![image](https://user-images.githubusercontent.com/110509654/227430268-40f41d66-3cdb-45ed-8f8f-c9ab7b5ba9ad.png)


