---
layout: post
title: 배열원소 이동
date: 2020-06-23
author: Hongjoong Kim
categories: 과제리뷰
tags: [java]
---

## 문제

### 실습3: 배열원소 이동

- 입력:1~10


- 출력:[2,3,4,5,6,7,1]


> Int[] irr = {1,2,3,4,5,6,7}; 

## 풀이

```java
package p20200623;

import java.util.Scanner;

class Service{  // 기능 메소드들이 들어갈 서비스라는 클래스를 따로 만들었음
	public int[] swap(int[] arr, int count) { // 이 메소드는 정수(int)로 이루어진 배열([])을 리턴값으로 받겠다. 이름은 swap이며, 
	                                         	//정수 배열과 정수를 넣어주면(파라미터 = 매개변수) 그걸로 계산하겠다는 의미
		int temp;                               //temp라는 임시로 쓸 변수를 만들어줌. 타입은 int(배열에 들어간 값들이 정수니까!)
		for(int k = 0; k<count; k++ ) {         //파라미터에서 받아온 배열과 숫자 중 숫자를 첫번쨰 for문의 횟수로 정하겠다는 의미
			temp = arr[0];                     //temp에 배열의 첫번째 값을 집어넣겠음
				for(int i=0; i<arr.length-1;i++) { // 길이 -1을 안해주면 오류가 난다!!! 배열의 길이만큼인데 i+1번째는 배열 범위를 넘어가버리기 때문. 그림으로 그려도 길이만큼 반복할 필요 x
				arr[i] = arr[i+1];               //i+1번째 배열에 들어있는 값을 i번째에 넣어라. 즉, 한칸씩 땡기는 모양이 된다. 정확히는 덮어쓰면서 떙겨지게 됨
				}
			arr[arr.length-1] = temp;           //다 땡겼으면 최초에 템프에 넣었던 값을 길이-1번째 칸에 넣어준다. 배열은 0부터 시작하기 때문에 길이-1이 마지막 칸임. 
		}
		return arr;                            //이 모든 과정이 끝난 배열을 리턴값으로 올려준다. 즉, 이 메소드가 실행되고 나면 "swap(arr,int)"라는 텍스트는 배열의 값을 가지게 된다는 것. 
	}
	
	public void pritArr(int[] arr) {          // 위와 같다. 프린트어레이라는 메소드는 정수배열을 파라미터로 받겠다. 이 메소드 실행시킬거면 정수배열을 내놔라.
		System.out.print("[ ");               // 일단 중괄호 하나 찍어주고
		for(int i=0; i<arr.length-1; i++) {   // 줄바꿈 없이 마지막 값을 제외한 값들을 좌라라락 찍어준다. 마지막까지 안한 이유는 콤마 찍히는거 짜증나서
			System.out.print(arr[i]+", ");
		}
		System.out.println(arr[arr.length-1] + " ]");  // 마지막 값 찍어준 후 중괄호로 마무리. 이 프린트아웃들이 목적이기 때문에 리턴값은 필요없다.
	}
}


public class Practice03 {
	public static void main(String[] args) { // 메인메소드
		Service service = new Service(); // 서비스 클래스의 메소드를 호출하기 위한 인스턴스 생성
		Scanner scanner = new Scanner(System.in); //스캐너를 호출하기 위한 손가락아파요
		int[] arr = {1,2,3,4,5,6,7}; // 정수 배열을 하나 만드는데, 직접 값을 입력해서 초기화하겠다~~
		System.out.println("실행 횟수를 입력하세요");
		arr = service.swap(arr, scanner.nextInt()); // 서비스 인스턴스를 사용하여 스왑 메소드를 실행. 파라미터는 위에서 선언한 정수배열과, 스캐너로 받아온 숫자.
		                                            // 그리고 아까 "swap(arr,int)"라는 텍스트가 배열의 값을 가지게 된다 했죠(리턴) 이걸 arr 배열에 대입한다!!
		service.pritArr(arr);                       // 프린트 메소드 실행
	}
}

```