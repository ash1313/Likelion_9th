# Django

## MTV패턴

### 가상환경

+ python -m venv [가상환경명] //가상환경을 만드는 명령어
+ + source [가상환경명]/bin/activate    //mac 실행
  + source [가상환경명]/Script/activate  //windows 실행

+ pip install django //장고를 다운로드
+ django-admin startproject [프로젝트 이름]  //장고로 프로젝트를 만듬
+ python manage.py runserver //server를 기동

### MTV패턴

MTV(Model Template View)

+ Front End: Template
+ Back End: Model, View

Template :

+ 사용자가 보이는 영역
+  HTML
+ CSS
+ 템플릿 언어

Model:

+ DataBase(DB)

View:

+ 데이터를 처리하는 곳
+ MTV중에서 핵심

## Django 실습[1]

### App

Django 프로젝트를 이루는 작은 단위

### 웹 사이트 구동 순서

1. 사용자가 서버에 요청
2. 서버의 view 는 model에게 요청에 필요한 데이터를 받음
3. view는 받은 데이터를 적절하게 처리해서 template으로 넘김
4. template은 받은 정보를 사용자에게 보여줌

### 정리

1. App을 생성
2. Template 제작
3. View 제작
4. URL연결

![image-20210605151206388](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605151206388.png)

![image-20210605151215507](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605151215507.png)

## Django 실습[2]

### 템플릿 언어

html에서 파이썬 변수와 문법을 사용하게 해주는 언어

``{%for(if)~~~~%}

  ...

  {%endfor(if)%}
``
+ {{변수명}}
+ ![image-20210605161852588](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605161852588.png)
+ ![image-20210605161906425](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605161906425.png)


## git 사용법

### 명령어

+ echo "#firstproject">>README.md
+ git init : 현재 디렉토리를 새로운 깃 저장소로 초기화한다.
+ git add README :Staging area로 더함
  + gitignore.io
  + gitignore 폴더

+ git commit -m "message" 파일들을 저장
+ git branch "브랜치 이름": 브랜치를 만듬
+ git checkout 옮길 branch: 옮김

+ git remote [ remote 이름] [깃주소]: 깃주소에 연결

+ git push [remote이름] [branch이름]: 깃허브에 업로드

  

##  Django와 데이터베이스

ORM(Object Relation Mapping)

models.py

클래스: 붕어빵 틀

객체: 붕어빵

+ class Blog:
  + ID=숫자
  + 제목=문자
  +  본문=문자
  + 생성날짜=날짜
  + 글쓴이=문자

  

## Model 실습

![image-20210605175350009](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605175350009.png)

![image-20210605175427434](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210605175427434.png)

### python manage.py makemigrations

:앱 내의 migration 폴더를 만들어서 models.py의 변경사항 저장

### python manage.py migrate

:Migration폴더를 실행시켜 데이터베이스에 적용

### python manage.py createsuperuser

:슈퍼 권한 유저 생성



## CRUD

### CRUD-READ

:Create Read Update Delete

데이터 베이스를 CRUD한다.

def summary(self):

​	return self.body[:100]// 파이썬 슬라이싱

get_object_or_404 : 404 오류

![image-20210606141712159](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210606141712159.png)

![image-20210606141722449](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210606141722449.png)

![image-20210606141742309](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210606141742309.png)

### CURD-CREATE

new: new.html 보여줌

create: 데이터베이스에 저장

get vs post

get 

+ 데이터를 얻기 위한 요청
+ 데이터가 url에 보임

post

+ 데이터를 생성하기 위한 요청
+ 데이터 url 안보임
+ csrf 공격 방지

![image-20210607003912093](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210607003912093.png)

![image-20210607003940290](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210607003940290.png)

## CRUD-UPDATE

edit: edit.html 보여줌

update: 데이터베이스에 적용

수정할 데이터의 id값을 받아야함

![image-20210611122428694](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210611122428694.png)

![image-20210611122439383](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210611122439383.png)

## CRUD-DELETE

![image-20210611123036305](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210611123036305.png)

![image-20210611123043898](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210611123043898.png)

![image-20210611123054896](C:\Users\안효준\AppData\Roaming\Typora\typora-user-images\image-20210611123054896.png)
