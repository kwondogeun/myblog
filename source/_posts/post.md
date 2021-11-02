---
title: temp1028
date: 2021-10-28 14:22:21
tags: python
---

2021년 10월 28일 시작.

## 개요
-블로그 만들기 

## 프로그램 설치
-node.js 설치
+ URL:https://nodejs.org/ko/

- git 설치
+ URL:https://git-scm.com/

-깃허브 회원가입
+ URL:https://github.com/

-pycharm 설치
+ URL:https://www.jetbrains.com/ko-kr/pycharm/

## 깃허브 파일생성

1. 로그인 후 your repositories 클릭
2. New
3. Repository name(파일명과 동일하게)
4. Create repository
5. Code 클릭후 https 복사
6. 바탕화면 우클릭 Git bash 실행
7. ~$git clone 붙여넣기
8. 파일생성완료

## Repo 만들기
- 블로그 운영을 위한 Repo 2개의 파일(버전관리,배포용)이 필요하다.

1. hexo 설치 ~$ npm install -g hexo-cli

- 파일 명은 버전: ex)myblog 배포용: 본인이름.github.io 두 개의 파일 깃허브생성

3. 
- ~$ hexo init myblog
- ~$ cd myblog
- ~$ npm install
- ~$ npm install hexo-server --save
- ~$ npm install hexo-deployer-git --save

5. config.yml 파일 설정

6. title: 제목을 지어주세요

7. author: YourName

8. url: https://본인이름.github.io

9. #Deployment -- _config.yml 내용 수정
  - deploy:
  - type: git
  - repo: https://github.com/kwondogeun/kwondogeun.github.io.git
  - branch: main

10. ~$ hexo generate --버전

11. ~$ hexo server를 통해 localhost:4000으로 화면확인

12. ~$ hexo deploy --배포

## 블로그 파일 만들기
-~$ hexo new 파일명

## 용어정리
- ~$ git add . 
- ~$ git commit -m "updated" 
- ~$ git push 

## 테마 변경(예시)
- ~$ npm install -S hexo-theme-icarus --이카루스테마
- _config.yml에서 theme:icarus--로 수정
- 에러생성 (?) ~$ npm install --save bulma-stylus@0.8.0 hexo-renderer-inferno@^0.1.3 을추가하라고 문구나옴
- 에러문구 메세지입력하면 적용

## 이미지 추가(예시)
- source하위 폴더에 images폴더 생성

![](/images/dog.jpg)

##배포할때 명령필수-> 헥소 제네레이트($hexo generate )
                 헥소 디플로이 ($hexo deploy)

##블로그 만들기 (참고자료)
https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/#install-npm

##블로그 세팅하기 (참고자료)
https://dschloe.github.io/settings/

##나의 깃허브 링크
https://github.com/kwondogeun/kwondogeun.github.io/

##빅데이터 공모전 링크
https://bigdata.seoul.go.kr/noti/selectNoti.do?r_id=P440&bbs_seq=429&sch_type=&sch_text=&currentPage=1

##빅데이터 자격증 관련 링크
https://dataq.or.kr/www/main.do

## 파이썬
2021-11-01 파이썬 수업

1. google colab 검색해서 이용(깃허브 연동가능)
2. 크롬 로그인해서 이용할것.

##예시

# 주석처리
- print("Hello, world!") -->(출력) Hello, world!
# 변수의 종류
- int,float,bool,none
# 사칙연산
- a = 3 b = 2
- print('a + b = ', a+b)  --> (출력) a+b = 5
- print('a - b = ', a-b)  --> (출력) a-b =1
- print('a * b = ', a*b)  --> (출력) a *b = 6
- print('a / b = ', a/b)  --> (출력) a/b= 1.5
- print('a // b = ', a//b) --> (출력) a//b=1
- print('a % b = ', a%b) --> (출력) a%b=1
- print('a ** b = ', a**b) --> (출력) a **b=9

# 논리형 연산자
- print(True and True) -->True
- print(True and False) --> False
- print(False and True) --> False
- print(False and False) --> False

# 비교 연산자
- print(4 > 3)  true
- print(4 < 3)  false
- print(4 >= 3) true
- print(4 <= 3) false
- print(4 > 4) false
- print(4 >= 4) true

# 논리형 & 비교 연산자 응용
- num1 = int(input("첫번째 숫자를 입력하세요: "))
- num2 = int(input("두번째 숫자를 입력하세요: "))
- num3 = int(input("세번째 숫자를 입력하세요: "))
- num4 = int(input("네번째 숫자를 입력하세요: "))

- var1 = num1 >= num2
- var2 = num3 < num4
- print(var1 and var2)

# 응용 출력
- 첫번째 숫자를 입력하세요: 4
- 두번째 숫자를 입력하세요: 5
- 세번째 숫자를 입력하세요: 2
- 네번째 숫자를 입력하세요: 3
- False

# Indexing
- greeting = "Hello Kaggle"
- print(greeting[6])
  - (출력) K

# Slicing
- greeting = "Hello Kaggle"
- print(greeting[:])
- print(greeting[6:])
- print(greeting[:6])
- print(greeting[3:8])
- print(greeting[0:9:2])
- (출력)
  - Hello Kaggle
  - Kaggle
  - Hello 
  - lo Ka
  - HloKg

# 리스트
- a = [] # 빈 리스트
- a_func = list() #list()함수로도 빈 리스트를 만들 수 있다.
- b = [1] # 숫자도 요소가 될 수 있다.
- c = ['apple'] # 문자열도 요소가 될 수 있다
- d = [1, 2, ['apple']] # 리스트 안에 리스트를 요소로 넣을 수 있다.

- a = [['apple','banana','cherry'], 1]
  - print(a[0]) # 리스트 내의 리스트
  - print(a[0][0]) # 리스트 내의 리스트의 첫번째 문자열
  - print(a[0][0][3]) # 리스트 내의 리스트의 첫번째 문자열 'apple' 중 첫번째 인덱스
  - print(a[0][1]) # 리스트 내의 리스트의 두번째 문자열

- (출력)
  - ['apple', 'banana', 'cherry']
  - apple
  - l
  - banana

- a = [1,2,3,4,5,6,7,8,9,10]
 - b = a[:4]  # 인덱스 0부터 3까지
 - c = a[1:4] # 인덱스 1부터 3까지
 - d = a[0:7:2] # 인덱스 0부터 6까지 인덱스 2씩 건너 띄우기
 - e = a[::-1] # 리스트 a의 역순
 - f = a[::2] # 리스트 전체구간에서 인덱스 2씩 건너띄우기

# 예시
- print("a[:4]", b)
- print("a[1:4]", c
- print("a[0:7:2]", d)
- print("a[::-1]", e)
- print("a[::2]", f)

- (출력)
  - a[:4] [1, 2, 3, 4]
  - a[1:4] [2, 3, 4]
  - a[0:7:2] [1, 3, 5, 7]
  - a[::-1] [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
  - a[::2] [1, 3, 5, 7, 9]

# 리스트값 수정하기
- [] a = [0,1,2]
- a[1] = "b"
- print(a)
  - (출력) [0,'b',2]

# 리스트값 추가
- a.append , a.extend
# 리스트값 삭제
- a.remove , del , a.pop

# 유용한 메서드
- a.clear(삭제) a.sort(값 정렬)

# 튜플
- tuple1 = (0) # 끝에 콤마(,)를 붙이지 않았을 때
- tuple2 = (0,) # 끝에 콤마(,)를 붙여줬을 때
- tuple3 = 0,1,2

- print(tuple1)
- print(tuple2)
- print(tuple3)

- print(type(tuple1)) # 콤마(,)를 붙여주지 않으면 튜플이 아닙니다.
- print(type(tuple2)) # 콤마(,)를 붙여주어야 튜플 자료형 입니다.
- print(type(tuple3)) # 여러개의 값 일경우 괄호를 없애주어도 튜플 자료형 입니다

- (출력)
  - 0
  - (0,)
  - (0, 1, 2)
  - <class 'int'>
  - <class 'tuple'>
  - <class 'tuple'>

# 딕셔너리 
- value값 넣어주는것. ex) dic = { 'teacher' : 'alice' }

# 집합 연산자

# if 조건문
- a = -5

- if a>5:
   - print('a is bigger than 5')

- elif a > 0:
   - print("a is bigger than 0 but a is smaller than 5 ")

- else:
   - print("a is negative"
- (출력)
   - a is negaive

# 반복문
- for i in range(100):
    - print("Hello World")
- 출력하면 100개의 문장 출력

- ex) 반복문과 break문
    - a = "Kaggle"
    - for x in a:
    - print(x)

    - if x == 'g':
    - break
  

# 참고용URL:https://docs.python.org/3/tutorial/datastructures.html