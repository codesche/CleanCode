## 목차
1. [자료구조 VS 객체](#1-자료구조-VS-객체)
2. [디미터의 법칙](#2-디미터의-법칙)
3. [DTO](#3-DTO)
4. [Active Record](#4-Active-Record)


## 1. 자료구조 vs 객체
![image](https://user-images.githubusercontent.com/110509654/227235457-6b6c78d2-b291-4707-96b7-c68c402da31e.png)

**○ 예시 - Shape**
![image](https://user-images.githubusercontent.com/110509654/227235929-89ba00ab-5619-4a58-af39-bd111ce3cb64.png)


![image](https://user-images.githubusercontent.com/110509654/227236145-7a67459e-0c6f-42a5-ac15-d7c3fb19dbdc.png)


**상황에 맞는 선택을 하면 된다**
* 자료구조를 사용하는 절차적인 코드는 기본 자료 구조를 변경하지 않으면서 새 함수를 추가하기 쉽다.
* 절차적인 코드는 새로운 자료 구조를 추가하기 어렵다. 그러려면 모든 함수를 고쳐야 한다.
* 객체지향 코드는 기존 함수를 변경하지 않으면서 새 클래스를 추가하기 쉽다.
* 객체지향 코드는 새로운 함수를 추가하기 어렵다. 그러려면 모든 클래스를 고쳐야 한다.


## 2. 디미터의 법칙
![image](https://user-images.githubusercontent.com/110509654/227238147-83ea2c86-d9be-4707-9559-613140b98ca7.png)

**클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다**
* 클래스 C
* 자신이 생성한 객체
* 자신의 인수로 넘어온 객체
* C 인스턴스 변수에 저장된 객체

**디미터의 법칙에 어긋나는 상황**
![image](https://user-images.githubusercontent.com/110509654/227239181-2ddb1539-4b95-47ed-822e-d688649f4774.png)


## 3. DTO

**○ DTO(Data Transfer Object) = 자료구조**

**다른 계층 간 데이터를 교환할 때 사용**
* 로직 없이 필드만 갖는다.
* 일반적으로 클래스명이 Dto(or DTO)로 끝난다.
* getter/setter를 갖기도 한다.
* Java Beans : 데이터 표현이 목적인 자바 객체
  * 멤버 변수는 private 속성이다.
  * getter와 setter를 가진다.  


## 4. Active Record
![image](https://user-images.githubusercontent.com/110509654/227240827-2bde6de2-5935-4020-9d22-fcecfbfac810.png)

**○ Active Record = 자료구조**

**Database row를 객체에 맵핑하는 패턴**
* 비즈니스 로직 메서드를 추가해 객체로 취급하는 건 바람직하지 않다.
* 비즈니스 로직을 담으면서 내부 자료를 숨기는 객체는 따로 생성한다.
* 하지만 객체가 많아지면 복잡하고, 가까운 곳에 관련 로직이 있는 것이 좋으므로 현업에서는 Entity에 간단한 메서드를 추가해 사용한다.


**○ Active Record vs Data Mapper**


**Active Record**

![image](https://user-images.githubusercontent.com/110509654/227241382-2d436dfd-9a60-4686-9aeb-8d42b5a476b1.png)

* 객체가 row를 담을 뿐 아니라 database에 대한 접근을 포함한다.
* Person의 속성을 담을 뿐 아니라, 생성 수정도 객체 안에서 수행할 수 있다.
* 사례 - Ruby on rails

**Data Mapper**

![image](https://user-images.githubusercontent.com/110509654/227242574-12715192-fb59-4e2f-a708-01d69c9cbe61.png)

* row를 담는 객체와 database에 접근할 수 있는 객체가 분리되어 있다.
* Person은 값만 담고 있고, 생성, 수정 등 액션은 Person Mapper에서 담당한다.
* 사례 - Hibernate

