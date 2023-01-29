## 목차
1. [주석을 최대한 쓰지 말자](#1-주석을-최대한-쓰지-말자)
2. [좋은 주석](#2-좋은-주석)
3. [주석보다 annotation](#3-주석보다-annotation)
4. [JavaDoc](#4-JavaDoc)


## 1. 주석을 최대한 쓰지 말자

```java
// 직원에게 복지 혜택을 받을 자격이 있는지 검사
if ((employee.flags & HOURLY_FLAG) && employee.age > 65))

// 의미있는 이름을 지으면 해결됨
if (employee.isEligibleForFullBenefits())
```

**주석은 나쁜 코드를 보완하지 못한다**
* 코드에 주석을 추가하는 이유는 코드 품질이 나쁘기 때문이다. 자신이 저지른 난장판을 주석으로 설명하지 말고 개선하는데 시간을 보내야 한다.
* 코드로도 의도를 표현할 수 있다!

**주석은 방치된다**
* 코드의 변화에 따라가지 못한 채 주석은 방치된다
* 코드는 컴파일되어 호출되나 주석은 그저 주석이다. 그 자리에 방치되고 결국 의미없는 텍스트가 된다. 
-> '복지 혜택에 연금 혜택 기준이 추가된다면?'

## 2. 좋은 주석

1. 좋은 주석은 구현에 대한 정보를 제공한다
```java
// kk:mm:ss EEE, MMM dd, yyyy 형식
Pattern timeForamt = Pattern.compile("\\d*:\\d:\\d* \\w*, \\w* \\d* \\d*");
```

2. 좋은 주석은 의도와 중요성을 설명해준다
```java
// 스레드를 많이 생성하여 시스템에 영향을 끼쳐 테스트를 만들도록 함
for (int i = 0; i < 25000; i++) {
    SomeThread someThread = ThreadBuilder.builder().build();
}
```

```java
// 유저로부터 입력받을 값을 저장할 때 trim으로 공백제거 필요
String userName = userNameInput.trim();
```

3. // TODO // FIXME


![image](https://user-images.githubusercontent.com/110509654/215362230-6b9dee1c-ce23-4adc-bd84-45f90050513d.png)


* TODO : 앞으로 할 일. 지금은 해결하지 않지만 나중에 해야할 일을 미리 적어둘 때
* FIXME : 문제가 있지만, 당장 수정할 필요는 없을 때. 가능하면 빨리 수정하는 게 좋다

=> IDE에서 하이라이팅되며, 별도의 윈도우에서 볼 수 있다

## 3. 주석보다 annotation

**java.lang.annotation**
* annotation : 코드에 대한 메타 데이터
  * 코드의 실행 흐름에 간섭을 주기도 하고, 주석처럼 코드에 대한 정보를 줄 수 있다
* @Deprecated : 컴파일러가 warning을 발생시킴. IDE에서 사용시 표시가 된다
* @NotThreadSafe : Thread Safe하지 않음을 나타냄 

![image](https://user-images.githubusercontent.com/110509654/215362472-cc264865-bc5b-44e6-9367-9f9322b89c34.png)


## 4. JavaDoc

Java 코드에서 API 문서를 HTML 형식으로 생성해주는 도구

![image](https://user-images.githubusercontent.com/110509654/215362505-cbf7e3c8-4390-4c92-a720-bf023cced7d6.png)

* Class level

![image](https://user-images.githubusercontent.com/110509654/215362525-048d2464-388b-4196-83e1-73d9116803c9.png)

* Field level

![image](https://user-images.githubusercontent.com/110509654/215362539-c4d3aedb-e5ac-49f6-a359-77e07bb4d461.png)


* Method level

![image](https://user-images.githubusercontent.com/110509654/215362553-f994f28d-183c-45f6-8527-d064c7a7b8d3.png)

* JavaDoc 문서

![image](https://user-images.githubusercontent.com/110509654/215362571-0faa3d7b-ad50-47b5-96b8-47b1c69ca018.png)




