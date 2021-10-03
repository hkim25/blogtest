---
layout: post
title: mdPractice
date: 2021-10-03
author: Hongjoong Kim
categories: markdown
tags: [markdown, practice]
---

# 마크다운 연습

`개행`  
띄어쓰기를 두 번 입력하면 줄이 바뀐다.  
이렇게  
  
`목록`   
요소를 나열할 때  

1. 첫번째  
2. 두번째  
3. 세번째  

+ 순서없음
  - 홍길동
    * 중대장
        + 프로실망러

`강조`   
문장 내 강조하고 싶은 단어를 눈에 띄게  
__볼드(진하게)__  
_이탤릭(기울이기)_  
~~취소선~~  
<u>밑줄(왜 갑자기 태그임ㅋㅋ)</u>  
  
`인용구`  
인용할 경우 또는 분위기 전환시에도 사용  
  
>위키백과
>>중대장은 실망했다.
>>>프로 실망러

`링크`  
[그냥 에이태그 쓰면 안됨?](https://www.github.com/hkim25)  
<https://www.github.com/hkim25>  
[동일 파일 내 문단 이동](#마크다운-연습)  
  
>__문단 매칭 방법__  
>제목(header)를 복사 붙여넣기 후  
> 1) `특수문자` 제거 
> 2) 스페이스 갯수만큼 `-`로 변경  
> 3) 대문자 -> `소문자`로 변경  
> 4) 예) "#Markdown! 장점" -> "#markdown-장점"  
  
<br>  
<br>
  
`이미지` 삽입  

    
유형 1 : 단순 이미지 삽입  

![이미지](https://hkim25.github.io/assets/swh.jpg)
  
    
유형 2 : 크기 조절을 위해선 img 태그 사용 <br>  

<img src = "https://hkim25.github.io/assets/swh.jpg" height="100" width="150">  
  
<br>
유형 3 : 이미지에 링크 걸기  
  
[![이미지](https://hkim25.github.io/assets/swh.jpg)](https://hkim25.github.io)  
  
    
      
  
`코드 블록`  
```java  
public String sampleMethod(){
    String result = "returnValue";
    return result;
}
```  

__어렵다 어려워__

