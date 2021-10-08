---
layout: post
title: 제어문 실습
date: 2020-06-24
author: Hongjoong Kim
categories: 과제리뷰
tags: [java]
---

## 문제

```
실습:

선택하세요. [0:나가기, 1:학생입력, 2:학생수출력, 3:학과별 학점평균,4:학생목록출력]

[학생입력]

학번: 111

이름: 홍길동

학과: 수학과

학점: 90
​

[학과수 출력]

총학생수: 5

평균점수: 85
​

[학과별 학점평균]

학과를 입력하세요: 수학과

평균점수: 85
​

[학생목록출력]

학번: 111

이름: 홍길동

학과: 수학과

학점: 90


학번: 112

이름: 김길동

학과: 국학과

학점: 85

선택 후 작업 수행하면 다시 ‘선택하세요’가 나타난다

​
학과: 수학과(10),국어과(20), 영어과(30)
```

## 풀이

`Student 클래스`
```java
package p20200624;

import java.util.Scanner;

class Student{ // 학생을 추상화한 클래스 Student를 생성하였습니다.
	private String number, name, dep;  // 우리는 학번, 이름, 학과, 점수가 있는 객체를 "학생"이라 부르도록 하겠습니다.
	private int score;
	
	public String getNumber() {  // Student 클래스의 멤버변수(number,name등)은 private이기 때문에 다른 클래스에서 접근할 수 없습니다. 따라서 이를 읽고 쓰기 위한 게터/세터 메소드를 작성하겠습니다.
		return number;           // 게터 - 리턴값이 있음. 이건 스트링. 즉, 이 메소드를 실행한 이후 getNumber()라는 텍스트는 스트링 값을 갖게 된다는 이야기.
		                         // 여기선 number를 리턴하게 되어있네요. 해당 인스턴스에 저장된 number를 읽어와서 메소드의 결과로 돌려주라는 뜻입니다. 이래서 getter죠
	}
	public void setNumber(String number) {  //이 메소드는 매개변수를 요구하네요. 즉 setNumber() 메소드를 실행하기 위해선 파라미터(괄호 안)에 특정 값을 넣어주어야 한다는 뜻입니다. 
		                                    //여기선 스트링 값을 요구할 것이고, 그 받아온 값을 number라 부르겠다는 의미입니다.
		this.number = number;               //this.number는 위쪽 멤버변수 number를 가리키고 number는 매개변수로 받은 스트링값을 의미합니다. 즉 받아온 값을 멤버변수 number에 넣어라. setter죠
	}                                       //동작 수행만 하면 되고 딱히 돌려받아야 할 값은 없습니다. 따라서 리턴값은 없고 void가 들어갔네요.
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getDep() {
		return dep;
	}
	public void setDep(String dep) {
		this.dep = dep;
	}
	public int getScore() {
		return score;
	}
	public void setScore(int score) {
		this.score = score;
	}
}

class StudentService{  // 여러 기능들을 수행할 메소드를 StudentService 클래스에 몰아넣었습니다.
	int index = 0;     // 학생들을 한 칸씩 차례차례 넣기 위해 인덱스라는 이름의 정수 변수를 만들어 줍니다.
	Student[] students = new Student[50]; //Student 타입의 데이터로 이루어진 배열을 만듭니다. 이름은 students라고 지었습니다. 크기는 50칸입니다.
	
	public void input(Student student) {  //새 학생을 students 배열에 입력하는 메소드를 만들었습니다. 파라미터는 Student student. 즉 이 메소드를 호출할 때 매개변수로 Student 타입의 자료를 달라는 뜻입니다.
		students[index] = student; // students 배열의 index번째 칸에 방금 받아온 student를 넣어줍니다.
		index++; // 그리고 인덱스를 1 증가시킵니다. 이 과정이 없으면 무한히 0번째 칸에 덮어씌워지겠죠. StudentService 인스턴스는 최초 한 번 만든 후 계속 유지할것이므로 변화하는 index값은 쭉 저장됩니다.
	}
	
	public void totAvg() { //모든 학생들의 평균점수를 구하는 메소드입니다. 동작 수행만 필요한 구조이므로 리턴값, 매개변수 모두 없습니다.
		int sum = 0;       // 합계, 평균을 저장해둘 변수 선언.
		int avg = 0;
		for(int i = 0; i<index; i++) {    //i<index가 중요합니다. 배열의 길이는 50이지만 현재 저장된 학생 수 까지만 돌리겠다는 의미.
			sum += students[i].getScore(); //sum 변수에 i번째 학생의 점수를 더해줍니다. 게터로 점수를 불러오는 형태죠. 만약 Student의 멤버변수가 퍼블릭이었다면 students[i].score;의 형태가 됐겠네요.
		}
		avg = sum/index; // 다 더해줬으면 합계를 학생 수로 나눠준 후 그걸 평균에 넣어줍니다.
		System.out.printf("총 학생수 : %d명%n평균점수 : %d점%n", index, avg); //출력문
	}
	
	public void depAvg(int dep) { //10. 수학과  20. 국어과  30. 영어과  //학과별 평균을 구하는 메소드입니다. 외부에서 스캐너로 정수를 받아온 후 그 숫자로 스위치를 돌렸습니다. 스트링 받아와도 상관 없습니다.
		int sum = 0;
		int avg = 0;
		int count = 0; // 위와 같습니다만 학과별 학생 수를 계산하기 위한 count 변수가 추가되었습니다.
		switch(dep) { // 만약 받아온 숫자가 dep(매개변수)면,
		case 10 : 
			for(int i = 0; i<index; i++) {
				if((students[i].getDep()).equals("수학과")) { //students[i]에게 학과 게터를 사용 후, 그 값이 "수학과"와 같으면, 이라는 의미입니다. 문자열 비교이므로 ==가 아닌 .equals 사용
					sum += students[i].getScore(); count++; //sum에 해당 학생의 점수를 더하고 카운트를 1 증가시켜라. 
				}
			}
			break;
		case 20 : 
			for(int i = 0; i<index; i++) {
				if((students[i].getDep()).equals("국어과")) {
					sum += students[i].getScore(); count++;
				}
			}
			break;
		case 30 : 
			for(int i = 0; i<index; i++) {
				if((students[i].getDep()).equals("영어과")) {
					sum += students[i].getScore(); count++;
				}
			}
			break;
		default : System.out.println("정확한 학과번호를 입력하세요");	//엉뚱한 값이 들어왔을 때 출력될 디폴트 항목입니다.
			break;
		}
		if(count !=0) { // 만약 카운트가 0이라면 0 나누기 0 형태가 되어 오류가 발생합니다. 이걸 방지하기 위해 이프 분기를 하나 만들었습니다.
			avg = sum/count;
			System.out.printf("평균점수 : %d점%n",avg); // 카운트가 1 이상이라면 계산 후 출력.
		}
		else {System.out.println("해당 학과에 등록된 학생이 없습니다.");} // 아니면 오류메세지 출력.
	}
	
	public void print() {  // 총 학생 수를 출력하는 메소드입니다.
		for(int i = 0; i<index; i++) {
			System.out.printf("학번 : %s%n%n"
							+ "이름 : %s%n%n"
							+ "학과 : %s%n%n"
							+ "학점 : %d%n%n"
							+ "--------------%n%n"
							,students[i].getNumber(),students[i].getName(),students[i].getDep(),students[i].getScore());
		}
	}
	
	public static void br() { // 줄바꿈 할 때마다 시스아웃 찍기 싫어서 빈 시스아웃 메소드를 하나 만들었습니다.
		System.out.println("");
	}
}

```
`main method`
```java
public class ControlFlowPractice {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in); // 스캐너 클래스에 접근하기 위한 scanner 인스턴스 생성
		StudentService service = new StudentService(); // StudentService 클래스에 접근하기 위한 service 인스턴스 생성
		menu(scanner, service); // 기타 메뉴는 리팩토링으로 축약했습니다.
	}

	private static void menu(Scanner scanner, StudentService service) { // 리팩토링 된 파트
		Student student; // 먼저 Student 형태의 student 인스턴스를 선언합니다. 아직 생성(new)은 안한 상태
		while(true) {
			System.out.println("선택하세요. [0:나가기, 1:학생입력, 2:학생수출력, 3:학과별 학점평균, 4:학생목록출력]");
			switch(scanner.nextInt()) {
			case 0 : System.out.println("시스템 종료");return;
			case 1 : 
				student = new Student(); // 먼저 자료를 저장할 인스턴스를 만들어줘야겠죠.
				System.out.println("[학생입력]");
				StudentService.br(); // 줄바꿈 메소드. static이기 때문에 인스턴스 호출 없이 클래스명으로 바로 접근 가능합니다.
				System.out.println("학번 : ");
				student.setNumber(scanner.next()); // 스캐너로 파라미터를 받아서 세터 메소드 호출해줍니다. 이하 반복
				System.out.println("이름 : ");
				student.setName(scanner.next());
				System.out.println("학과 : ");
				student.setDep(scanner.next());
				System.out.println("학점 : ");
				student.setScore(scanner.nextInt());
				service.input(student);  // input 메소드 호출, 위의 작업으로 데이터가 채워진 student를 파라미터에 넣습니다. 이러면 지금의 데이터가 students[0]이 되고 service 인스턴스의 index가 1 증가했겠네요.
				System.out.println("입력완료");
				StudentService.br();
				break;
			case 2 : 
				System.out.println("[학과수 출력]");
				StudentService.br();
				service.totAvg(); // 매개변수 리턴값 모두 없는 메소드이기에 그냥 호출만 해주면 결과가 나옵니다.
				StudentService.br();
				break;
			case 3 : 
				System.out.println("[학과별 학점평균]");
				StudentService.br();
				System.out.println("조회할 학과를 선택하세요 : 10. 수학과  20. 국어과  30. 영어과");
				service.depAvg(scanner.nextInt()); //학과별 평균 메소드 호출. 파라미터는 스캐너로 받아줍니다.
				StudentService.br();
				break;
			case 4 : 
				System.out.println("[학생목록출력]");
				StudentService.br();
				service.print();
				StudentService.br();
				break;
			default : System.out.println("정확한 메뉴를 선택하세요.");
				break;
			}
		}
	}
}
```