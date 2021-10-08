---
layout: post
title: 상속 실습
date: 2020-06-23
author: Hongjoong Kim
categories: 과제리뷰
tags: [java]
---

## 문제

### 실습: SpecialMember, Member를설계하시오

```java
Member m = new Member(“김길동”);

m.setGrade(“3”);

m.hello(); // 안녕하세요 김길동입니다

SpecialMember sm= new SpecialMember(“홍길동”);

sm.setGrade(“1”);

sm.setSpecialPoint(100); // SpecialMember만 specialPoint관리

Member m2 = sm;

m2.hello(); // 안녕하세요 스패설멤버홍길동입니다
```

## 풀이

```java
package p20200623;
/*
 * * 실습: SpecialMember, Member를설계하시오

Member m = new Member(“김길동”);         // 여기서 알 수 있는 정보 : 1. Member라는 이름의 클래스를 만들어서 객체를 생성해라.
                                                            2. 인스턴스 이름은 m으로 해라
                                                            3. <<중요>> "스트링"을 파라미터로 받는 생성자를 만들어라!!
                                                            4. 그 생성자의 실행 내용은 아마도 받아온 스트링을 이름 변수에 저장하는 것일거다.
m.setGrade(“3”);                        // Member 클래스에 그레이드라는 변수도 들어있겠구나. 타입은 인트일듯.
                                                                                      게터세터를 만들어야겠다.
                                                                                      
m.hello(); //  안녕하세요 김길동입니다               // Member클래스에 헬로라는 메소드를 만들어야겠구나. 시스아웃 내용은 안녕하세요 "이름"입니다. 찍으면 될 것 같음.

SpecialMember sm= new SpecialMember(“홍길동”);  // 스페셜멤버라는 클래스가 등장함. 이 클래스를 호출할땐 sm인스턴스를 사용해야겠음. 얘 역시 생성자로 스트링 받아와야 함

sm.setGrade(“1”);                              // 얘도 그레이드가 있네? 여기서 눈치챌것 -> 상속을 이용하라는 소리구나!

sm.setSpecialPoint(100); // SpecialMember만 specialPoint관리   // 스페셜 멤버 메소드엔 물려받은 변수 외에 추가로 스페셜 포인트라는 변수가 있다. 얘도 게터세터 만들것

Member m2 = sm;                                // Member 인스턴스인 m2에 사이즈에 sm이 들어감 여기서 상속 확정

m2.hello(); // 안녕하세요 스패설멤버홍길동입니다              // 이름이 똑같은 메소드인데 스페셜멤버라는 단어가 추가됨. 자식 클래스에 오버라이딩으로 헬로 메소드 하나 더 만들면 되겠다.
 * 
 */

class Member{    //위에서 이해한대로 멤버메소드 먼저 만들었다.
	
	protected String name;  // 자식이 건드릴 수 있게 프로텍티드를 줬음. 처음에 프라이빗 줬다가 에러남. 자식도 게터세터 활용하면 접근할 수 있나? 잘 모르겠음.
	protected int grade; 
	Member(){}              // 내가 생성자를 임의로 하나라도 만들면! 디폴트 생성자가 자동생성되지 않음. 이거 한 클래스만 쓸 땐 상관 없는데, 자식쪽에서 자꾸 에러가 난다! 
	                        // 생성자 만들땐 디폴트도 같이 만드는 습관을 들이는게 좋을듯? 검증 필요. 이 부분 선생님께 다시 질문하고 싶다.
	Member(String name){    // 위에서 판단한대로 스트링을 받아 쓰는 생성자를 만들었음. 즉 인스턴스를 만들 때 파라미터에 스트링 값을 주면 처음부터 name에 해당 값이 들어간 상태로 생성된다.
		this.name = name;   // 위쪽 name에 받아온 name 넣으라는 내용. 세터랑 똑같음. 파라미터 이름 안겹치게 하면 디스 필요 없음.
	}
	public String getName() {return name;}  // 게터세터 설명 생략
	public void setName(String name) {this.name = name;}
	public int getGrade() {return grade;}
	public void setGrade(int grade) {this.grade = grade;}
	
	public void hello() {  //위에서 판단했던 헬로 메소드
		System.out.printf("안녕하세요 %s입니다.%n" , name);
	}
}

class SpecialMember2 extends Member{  //멤버의 자식 클래스인 스페셜멤버 클래스 생성. 2 붙인건 연습할때 다른 파일에서 이미 스페셜멤버를 써서 그랬음
	private int specialPoint;
	public SpecialMember2(String name) { // 상동. 얘는 자식 없어서 디폴트 안만들었음. 얘도 자식이 생기면 디폴트가 필요해질까? 습관 들이는게 나을듯.
		super.name = name;               // 부모 클래스의 name 변수에 받아온 name 넣으라는 의미의 super
	}

	public int getSpecialPoint() {return specialPoint;}  // 게터세터
	public void setSpecialPoint(int specialPoint) {this.specialPoint = specialPoint;}
	
	public void hello() {  //헬로 메소드. 오버라이딩 되기 때문에 스페셜멤버 인스턴스로 헬로를 호출하면 이게 실행됨.
		                   //만약 이 클래스에 헬로 메소드가 없는데 sm.hello();를 입력하면 Member 클래스(부모)의 헬로가 실행됨. 거기도 없으면? Object까지 올라감(부모의 부모)
		                   //근데 Object에 헬로 메소드가 없을테니 에러가 날 것임. 이게 오버라이딩.
		System.out.printf("안녕하세요 스페셜멤버 %s입니다.%n" , super.name);
	}
	
}

public class Practice4 {
	public static void main(String[] args) {  //메인 메소드에 선생님이 입력한 조건대로 명령문을 써넣으니 이런 결과가 나오게 되었습니다.
		Member m = new Member("홍길동");
		m.setGrade(3);
		m.hello();
		SpecialMember2 sm = new SpecialMember2("홍길동");
		sm.setGrade(1);
		sm.setSpecialPoint(100);
		Member m2 = sm;
		m2.hello();
	}
}

```