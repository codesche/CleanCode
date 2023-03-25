## 목차
1. [경계란](#1-경계란)
2. [경계 짓기 (1) 우리 코드를 보호하기](#2-경계-짓기-(1)-우리-코드를-보호하기)
3. [경계 짓기 (2) 우리 코드를 보호하기](#3-경계-짓기-(2)-우리-코드를-보호하기)
4. [외부 라이브러리 테스트하기](#4-외부-라이브러리-테스트하기)

## 1. 경계란

![image](https://user-images.githubusercontent.com/110509654/227696263-34d04648-84f4-4f01-841e-72b0a669052c.png)

* 오픈소스, 라이브러리를 안쓰는 프로젝트는 없다.
* 우리가 만든 코드에 외부에서 들어온 코드를 병합해야 한다.
* 외부 코드는 외부에서 만든 코드인데, 외부 시스템과 호출하거나 단순히 외부에서 만들어진 코드일 수 있다.
* 우리 코드와 외부 코드를 깔끔하게 통합시키기 위해 경계를 잘 지어야 한다.

## 2. 경계 짓기 (1) 우리 코드를 보호하기

**○ 캡슐화(Encapsulation)**

**객체의 실체 구현을 외부로부터 감추는 방식**

![image](https://user-images.githubusercontent.com/110509654/227696358-b61e3186-fbd1-454a-a3e4-85d85c79e09f.png)

**○ Sensor를 관리해야 한다. Sensor는 외부에서 사용된다**

![image](https://user-images.githubusercontent.com/110509654/227696421-23920cc5-fd01-45a3-af9d-5c20e8be6b68.png)


* Sensor Id와 Sensor 객체로 저장하고 싶어서, Map을 사용한다.
* 하지만 Map을 그대로 사용하면 Map이 가진 clear()가 외부로 노출된다.
* Sensor의 '외부'코드 관점에서 Sensor 객체의 값들만 가져오고 싶다.
* 캡슐화를 한다!

![image](https://user-images.githubusercontent.com/110509654/227696446-869970d1-7352-4dfe-b366-27d72e04c90b.png)


## 3. 경계 짓기 (2) 우리 코드를 보호하기

![image](https://user-images.githubusercontent.com/110509654/227696460-1ac6436a-01ee-4eab-94ff-20a7a15f60b7.png)

![image](https://user-images.githubusercontent.com/110509654/227696470-cba14282-9bfe-4cdd-87a4-c8fafc235ec6.png)

**○ 외부 코드와 호환하기 - Adapter 패턴**

**외부 코드를 호출할 때, 우리가 정의한 인터페이스 대로 호출하기 위해 사용하는 패턴**

![image](https://user-images.githubusercontent.com/110509654/227696505-1121aae1-c542-4d91-aa5c-b470f3b8624e.png)
![image](https://user-images.githubusercontent.com/110509654/227696518-305039ee-5253-425c-bd2d-5c3bdb5f7f33.png)

**○ Adapter 패턴 in Elastic Search**

![image](https://user-images.githubusercontent.com/110509654/227696549-8e0b1b41-5ca4-4891-9b49-d39e14ced076.png)

![image](https://user-images.githubusercontent.com/110509654/227696557-6daa6b12-dd79-41b7-b4fc-573e30e17124.png)

* 우리가 원하는 방식인 read할 때 ByteBuffer[]로 parameter를 보내면, 외부 코드인 nettyChannel에 ByteBuf 타입으로 parameter를 변환하여 전달한다.
* Page[] 타입 parameter로도 전달할 수 있다. Adapter에 매서드를 추가해 우리가 원하는 타입의 파라미터를 전달할 수 있다.
* 만약 adapter를 통한 변환을 거치지 않았다면 nettyChannel에 데이터를 전달할 때마다 타입을 변환하는 과정이 필요했고, 이는 중복을 발생시켰을 것이다.

![image](https://user-images.githubusercontent.com/110509654/227696620-e2e4fdff-731e-4008-9837-0fbe2d6b9dc7.png)


## 4. 외부 라이브러리 테스트하기

**○ Learning Test를 작성해 라이브러리를 테스트한다**

![image](https://user-images.githubusercontent.com/110509654/227696656-1731bfbf-c59a-47e7-9a3a-2b15aebd6468.png)

**외부 코드를 배우고, 안정성도 미리 검증할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/227696691-18807298-41f5-4d43-a4c1-61b51dcd4902.png)
