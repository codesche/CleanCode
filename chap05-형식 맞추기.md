## 목차
1. [포맷팅이 중요한 이유](#1-포맷팅이-중요한-이유)
2. [클린코드 포맷팅](#2-클린코드-포맷팅)
3. [Java Class Declarations](#3-Java-Class-Declarations)
4. [Team Coding Convention](#4-Team-Coding-Convention)

## 1. 포맷팅이 중요한 이유
![image](https://user-images.githubusercontent.com/110509654/226862432-dd41d0f2-1120-4ab4-9798-785f2803eaf7.png)

○ **가독성에 필수적이다** 
* 코드를 수월하게 읽어나갈 수 있다.
* 아마추어처럼 보이지 않는다.
* 포맷팅으로 인해 코드를 잘못해석해 버그를 발생할 수 있는 위험을 줄인다.


## 2. 클린코드 포맷팅

적절한 길이 유지 : ~200 lines, < 500 lines

**○ 200 라인**
* 코드 길이를 200줄 정도로 제한하는 것은 반드시 지킬 엄격한 규칙은 아니지만, 일반적으로 큰 파일보다는 작은 파일이 이해하기 쉽다.
* 코드 길이가 200라인을 넘어간다면, 클래스가 여러 개의 일을 하고 있을 수 있다. (SRP에 위배됨!)

**○ 밀접한 개념은 가까이**
* 행 묶음은 완결된 생각 하나를 표현하기 때문에 개념은 빈 행으로 분리한다.
* 변수는 사용되는 위치에서 최대한 가까이 선언한다.
![image](https://user-images.githubusercontent.com/110509654/226863576-51f11b4a-6df6-4639-949a-0ca78a60fd56.png)


## 3. Java Class Declarations

![image](https://user-images.githubusercontent.com/110509654/226864522-20b47440-ff91-4352-9230-cb6a97dea41f.png)

**○ Class 내부 코드 순서**
1. static 변수: public -> protected -> package -> private 
2. instance 변수 : public -> protected -> package -> private
3. 생성자
4. 메서드 : public 메서드에서 호출되는 private 메서드는 그 아래에 둔다. 가독성 위주로 그룹핑.

![image](https://user-images.githubusercontent.com/110509654/226865362-8eb99652-26d6-4baf-96eb-a7b995653237.png)


## 4. Coding Convention
✔ Coding Convention : 팀의 코딩 스타일에 관한 약속

**○ Team Coding Convention**
개발 언어의 컨벤션이 우선이지만, 애매한 부분은 팀 컨밴션을 따른다.

ex) Coding Convention 예시
![image](https://user-images.githubusercontent.com/110509654/226865834-6ef93f4f-88d2-4b61-ad1e-89d43267057f.png)

**○ 참고할 만한 컨벤션**
* Google Java Style Guide : https://google.github.io/styleguide/javaguide.html
* Naver Hackday Java Convention : https://naver.github.io/hackday-conventions-java/

