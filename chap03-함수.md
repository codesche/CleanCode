## 목차
1. [SOLID](#1-solid)
2. [간결한 함수 작성하기](#2-간결한-함수-작성하기)
3. [안전한 함수 작성하기](#3-안전한-함수-작성하기)
4. [함수 리팩터링](#4-함수-리팩터링)


## 1. SOLID

객체지향 설계의 5가지 원칙

**1) SRP : 단일 책임 원칙**

*한 클래스는 하나의 책임만 가져야 한다.*

* 클래스는 하나의 기능만 가지며, 어떤 변화에 의해 클래스를 변경해야 하는 이유는 오직 하나뿐이어야 한다.
* SRP 책임이 분명해지면, 변경에 의한 연쇄작용에서 자유로워질 수 있다.
* 가독성 향상과 유지보수가 편하다.
* 실전에서는 쉽지 않지만 항상 상기하며 작업해야 한다. (정말 쉽지 않음...)

**2) OCP : 개방-폐쇄 원칙**

*소프트웨어 요소는 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.*

* 변경을 위한 비용은 가능한 줄이고, 확장을 위한 비용은 가능한 극대화 해야 한다.
* 요구사항의 변경이나 추가사항이 발생하더라도, 기존 구성요소에는 수정이 일어나지 않는 상태에서 기존 구성요소를 쉽게 확장하여 재사용할 수 있어야 한다.
* 객체지향의 추상화와 다형성을 활용한다.


**3) LSP : 리스코프 치환 원칙**

*서브 타입은 언제나 기반 타입으로 교체할 수 있어야 한다.*

* 서브 타입은 기반 타입이 약속한 규약(접근제한자, 예외 포함)을 지켜야 한다.
* 클래스 상속, 인터페이스 상속을 이용해 확장성을 얻는다.
* 다형성과 확장성을 극대화하기 위해 인터페이스를 사용하는 것이 더 좋다.
* 합성(composition)을 이용할 수도 있다.


**4) ISP : 인터페이스 분리 원칙**

*자신이 사용하지 않는 인터페이스는 구현하지 말아야 한다.*

* 가능한 최소한의 인터페이스만 구현한다.
* 만약 어떤 클래스를 이용하는 클라이언트가 여러 개고, 이들이 클래스의 특정 부분만 이용할 경우, 여러 인터페이스로 분류하여 클라이언트가 필요한 기능만 전달한다. 
* SRP가 클래스의 단일 책임이라면, ISP는 인터페이스의 단일 책임이다. 


**5) DIP : 의존성 역전 원칙**

*상위 모델은 하위 모델에 의존하면 안 된다. 둘 다 추상화에 의존해야 한다. 추상화는 세부 사항에 의존해서는 안 된다. 세부 사항은 추상화에 따라 달라진다.*

* 하위 모델의 변경이 상위 모듈의 변경을 요구하는 위계관계를 끊는다.
* 실제 사용관계는 그대로이지만, 추상화를 매개로 메시지를 주고 받으면서 관계를 느슨하게 만든다.

```java
class PaymentController {
    @RequestMapping(value = "/api/payment", method = RequestMethod.POST)
    public void pay(@RequestBody ShinhanCardDto.PaymentRequest req) {
        shinhanCardPaymentService.pay(req);
    }
}

class ShinhanCardPaymentService {
    public void pay(ShinhanCardDto.PaymentRequest req) {
        shinhanCardApi.pay(req);
    }
```

이 상황에서 새로운 카드사가 추가될 경우 확장에 유연하지 않다...

```java
@RequestMapping(value = "/api/payment", method = RequestMethod.POST)
public void pay(@RequestBody CardPaymentDto.PaymentRequest req) {
    if (req.getType() == CardType.SHINHAN) {
        shinhanCardPaymentService.pay(req);
    } else if (req.getType() == CardType.WOORI) {
        wooriCardPaymentService.pay(req);
    }
}
```

![image](https://user-images.githubusercontent.com/110509654/212463698-b8f03277-1d1f-40cf-8716-0fa4ce8b1dde.png)


```java
class PaymentController {
    @RequestMapping(value = "/payment", method = RequestMethod.POST)
    public void pay(@RequestBody CardPaymentDto.PaymentRequest req) {
        final CardPaymentService cardPaymentService = cardPaymentFactory.getType(req.getType());
        cardPaymentService.pay(req);
    }
}

public interface CardPaymentService {
    void pay(CardPaymentDto.PaymentRequest req);
}


public class shinhanCardPaymentService implements CardPaymentService {
    @Override
    public void pay(CardPaymentDto.PaymentRequest req) {
        shinhanCardApi.pay(req);
    }
}
```

## 2. 간결한 함수 작성하기

**복잡한 함수는 보기에도 길고 여러가지 기능이 섞여있어서 불편하게 느껴진다. **

```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    boolean isTestPage = pageData.hasAttribute("Test");
    if (isTestPage) {
        WikiPage testPage = pageData.getWikiPage();
        StringBuffer newPageContent = new StringBuffer();
        includeSetupPages(testPage, newPageContent, isSuite);
        newPageContent.append(pageData.getContent());
        includeTeardownPages(testPage, newPageContent, isSuite);
        pageData.setContent(newPageContent.toString());
    }
    return pageData.getHtml();
}
```

**간결한 함수 작성 : 작은 단위로 분류하여 함수내 추상화 수준을 동일하게 맞춘다.**

```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData)) {
        includeSetupAndTearDownPages(pageData, isSuite);
    }
    return pageData.getHtml();
}
```

**한 가지만 하기(SRP), 변경에 닫게 만들기(OCP) :** 

'계산도 하고, Money도 생성?

```java
public Money calculatePay(Employee e) throws InvalidEmployeeType {
    switch (e.type) {
        case COMMISSIONED:
            return calculateCommissionedPay(e);
        case HOURLY:
            return calculateHourlyPay(e);
        case SALARIED:
            return calculateSalariedPay(e);
        default:
            throw new InvalidEmployeeType(e.type);
    }
}
```

**계산과 타입관리를 분리한다. 타입에 대한 처리는 최대한 Factory 쪽에서만!!!**

```java
public abstract class Empolyee {
    public abstract boolean isPayday();
    public abstract Money calculatePay();
    public abstract boid deliverPay(Money pay);
}

public interface EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType;
}

public class EmployeeFactoryImpl implements EmployeeFactory {
    public Employee makeEmployee(EmployeeRecord r) throws InvalidEmployeeType {
        switch (r.type) {
            case COMMISSIONED:
                return CommissionedEmployee(r);
            case HOURLY:
                return HourlyEmployee(r);
            case SALARIED:
                return SalariedEmployee(r);
            default:
                throw new InvalidEmployeeType(r.type);
        }
    }
}
```

**함수 인수 : 인수의 갯수는 0~2개가 적당. 3개 이상인 경우는???**

```java
// 객체를 인자로 넘기기
Circle makeCircle(double x, double y, double radius);   // x
Circle makeCircle(Point center, double radius);         // o

// 가변 인자를 넘기기 -> 특별한 경우가 아니면 사용 빈도수 낮음
String.format(Strinig format, Object...args);
```

## 3. 안전한 함수 작성하기

**부수 효과(Side Effect) 없는 함수**

값을 반환하는 함수가 외부 상태를 변경하는 경우 : 함수와 관계없는 외부 상태를 변경시킨다.

```java
public class UserValidator {
    private Cryptographer cryptographer;
    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

## 4. 함수 리팩터링

* 기능을 구현하는 서투른 함수를 작성 : 길고, 복잡하고, 중복도 있음
* 테스트 코드를 작성 : 함수 내부의 분기와 엣지값마다 빠짐없이 테스트 코드 작성
* 리팩터링 : 코드를 다듬고, 함수를 쪼개고, 이름을 바꾸고, 중복을 제거함 



