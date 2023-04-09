
## 목차
1. [나쁜 코드](#1-나쁜-코드)
2. [클린 코드](#2-클린-코드)
3. [의미 있는 이름 짓기](#3-의미-있는-이름-짓기)
4. [Google Java Naming Guide](#4-google-java-naming-guide)


## 1. 나쁜 코드

**성능이 나쁜 코드** : 불필요한 연산이 들어가서 개선의 여지가 있는 코드

**의미가 모호한 코드** : 이해하기 어려운 코드, 네이밍과 그 내용이 다른 코드

**중복된 코드** : 비슷한 내용인데 중복되는 코드들은 버그를 낳음

### 1.1 나쁜 코드가 나쁜 이유

**1.** **깨진 유리창의 법칙**
- 나쁜 코드는 깨진 유리창처럼 계속 나쁜 코드가 만들어지도록 한다

**2.** **생산성 저하**  
- 나쁜 코드는 팀 생산성을 저하시킨다
- 기술부채를 만들어 수정을 더 어렵게 한다

**3.** **새로운 시스템을 만들어야 한다**
- 현재 시스템을 유지보수하며 대체할 새로운 시스템 개발은 현실적으로 매우 어렵다 
- 레거시 코드를 고치기란 여간 어려운 게 아님

### 1.2 나쁜 코드를 짜는 이유

**1.** **일정이 촉박해서**
- 일정 안에 새로운 기능을 완성해야 한다
- 하지만.. 나쁜 코드는 생산성을 저하시키기 때문에 완성을 시키더라도 나중에 유지보수 때 꽤나 고생함

**2.** **영향 범위가 넓어서**
- 생각보다 영향 범위가 넓어서 건드릴 경우 다른 부분에 버그가 발생할 우려 때문에 나쁜 코드를 짬
- 하지만.. 기술부채는 버젓이 부메랑처럼 우리에게 돌아온다..

## 2. 클린 코드

★ **비야네 스트롭스트룹(C++ 창시자)**

"나는 우아하고 효율적인 코드를 좋아한다. 논리가 간단해야 버그가 숨어들지 못한다. 의존성을 최대한 줄여야 유지보수가 쉬워진다.
오류는 명백한 전략에 의거해 철저히 처리한다. 성능을 최적으로 유지해야 사람들이 원칙 없는 최적화로 코드를 망치려는 유혹에 빠지지 않는다."
****깨끗한 코드는 한 가지를 제대로 한다.****


★ **그래디 부치(객체지향 대가)**

"깨끗한 코드는 단순하고 직접적이다. **깨끗한 코드는 잘 쓴 문장처럼 읽힌다.** 깨끗한 코드는 결코 설계자의 의도를 숨기지 않는다.
오히려 명쾌한 추상화와 단순한 제어문으로 가득하다."

**클린 코드란?**

**1. 성능이 좋은 코드**

**2. 의미가 명확한 코드 = 가독성이 좋은 코드**

**3. 중복이 제거된 코드**

★ **보이스카우트 룰** : "전보다 더 깨끗한 코드로 만든다" => 개발 이전보다 개발 이후의 코드가 더 깔끔해야 한다 


## 3. 의미 있는 이름 짓기

**잘못된 사례**
```java
int a;
String b;

System.out.printf("User Requested %s. count = %d", b, a);
```
=> 변수의 정의가 명확하지 않음

**좋은 사례**
```java
int itemCount;
String itemName;

System.out.printf("User Requested %s. count = %d", itemName, itemCount);
```

```java
class SalesItem {
  ItemCode code;
  String name;
  int count;
}

SalesItem selectedItem = salesItemRepository.getItemByCode(purchaseRequest.getItemCode())

System.out.printf("User Requested %s. count = %d",
                  selectedItem.getName(), selectedItem.getCount());
```


**루프 속 i j k 사용하지 않기!**

배열 순회시 index를 의미하는 i를 사용하지 않고 advanced for 문으로 대체

![image](https://user-images.githubusercontent.com/110509654/212076734-244bfea8-5001-480c-8351-7281361c6c3e.png)

lambda를 사용할 수도 있음

![image](https://user-images.githubusercontent.com/110509654/212077338-04cd5562-3118-4ddf-8733-0621bd1fa637.png)


**i, j, k 대신 맥락에 맞는 이름을 찾아 코딩한다**

(i, j => row, col / width, height)

(i, j, k => row, col, depth)

**통일성 있는 단어 사용하기**

Member/Customer/User

Service/Manager

Repository/Dao


**변수명에 타입 넣지 않기**

```java
// bad example
String nameString => name 

Int itemPriceAmount => itemPrice

Account[] accountArray => accounts

public interface IShapeFactory => ShapeFactory          // 헝가리안 표기법 사용 X

public class ShapeFactoryImpl => CircleFactory

// good example
List<Account> accountList => accounts, accountList

Map<Account> accountMap

```

## 4. Google Java Naming Guide

**1. All lower case, no underscores**

```java
com.example.deepspace     // good
com.example.deepSpace     // bad
com.example.deep_space    // bad
```

**2. UpperCamelCase(대문자로 시작)**

```java
// 클래스는 명사, 명사구
Character, ImmutableList

// 인터페이스는 명사, 명사구, 형용사
List, Readable

// 테스트 클래스는 Test로 끝내기
HashTest, HashIntegrationTest
```

**3. LowerCamelCase(소문자로 시작)**

```java
// 메서드는 동사, 동사구
sendMessage, stop

// jUnit 테스트인 경우 underscore가 사용되기도 함
// <methodUnderTest>_<state> 패턴
pop_emptyStack
```

