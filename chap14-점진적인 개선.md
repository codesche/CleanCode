## 목차
1. [책의 예제](#1-책의-예제)
2. [점진적으로 개선하기](#2-점진적으로-개선하기)
3. [IDE를 활용해 점진적으로 개선하기](#3-IDE를-활용해-점진적으로-개선하기)

## 1. 책의 예제

### 명령형 인수 구문 분석기
**코드 초안**
* 모든 로직이 하나의 클래스에 들어가 있다.
* 처음부터 지저분한 코드를 짜려는 생각은 없었고, 코드를 어느 정도 손봤지만 새로운 인수 유형이 들어오면서 문제가 발생했다.
* 이제는 개선해야 할 때라는 걸 깨닫고, **변경 전후 시스템이 동일하게 돌아간다는 사실을 확인하기 위해 테스트들을 작성해두었다**.
* **점진적으로** 개선해나갔다.

![image](https://user-images.githubusercontent.com/110509654/230588066-ab1bdcc3-82a0-47ed-9b05-6ae2a479c65a.png)


**코드 완성본**
* Args 클래스에서 코드 중복을 최소화하고, ArgsException 클래스를 분리했다. ArgumentMarshaler 클래스를 통해 여러 인수에 대한 추후 확장성을 만들어냈다.
* **코드만 분리해도 설계가 좋아진다**. 관심사를 분리하면 코드를 이해하고 보수하기 훨씬 더 쉬워진다.

### 책의 예제를 통해 배울 점
* 한번 정도 따라 읽어가며 저자가 '점진적으로' 코드를 개선해나가는 사고 흐름을 따라가면 좋다.
* 부담없이 가볍게 읽어본다. **자신이 스스로 점진적으로 코드를 개선해보는 경험을 통해 더 많이 배우게 된다**


## 2. 점진적으로 개선하기

### 점진적으로 개선하기

![image](https://user-images.githubusercontent.com/110509654/230588427-16b6fb8e-942f-4a81-8da8-03190fb5dcff.png)

=> 프로그램을 망치는 가장 좋은 방법 중 하나는 개선이라는 명분 아래 구조를 크게 뒤집는 행위다


## 3. IDE를 활용해 점진적으로 개선하기

### Extract Method : 메서드 추출 기능

**코드 블럭을 메서드로 추출할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230588666-b01a0532-9a14-4b92-b67d-90ba590af464.png)

### Change Signature : 메소드 파라미터 추가, 삭제 및 변경

**메서드의 파라미터를 추가하거나 변경할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230588817-5b419147-ae64-41c3-875a-3b649bb23340.png)

### Rename : 이름 변경

**메서드나 변수 이름을 변경할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230588896-56105b05-1d29-416d-952c-44d95366ab3f.png)

### Extract Variable : 변수 추출 기능

**변수를 추출할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230588986-de905322-4421-4634-8689-9ea7ca31a42a.png)

### Extract Field : 멤버 변수 추출 기능

**특정 값을 멤버 변수로 설정할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230589125-237bf16f-0a1e-43f1-9223-7f8ca6c0c702.png)

### Extract Constant : 상수 추출 기능

**특정 값을 상수로 추출할 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230589242-d8297411-bb1c-46be-a2ee-952a08b78441.png)

### Pull Members Up & Pull Members Down

**하위 클래스의 메서드를 상위로 올리거나 & 상위 클래스의 메서드를 하위로 내릴 수 있다**

![image](https://user-images.githubusercontent.com/110509654/230589494-0cc37833-7f94-4da6-8adc-9556ce4df43a.png)

