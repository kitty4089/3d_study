### 26일 화 / 아침과제

**Morning Assignment :** Codecademy 9, 10장 마무리

if (9, 10장 다 한 사람)
    8장도 추가로 하기(좀 어려움)
end



---

#### 수업시작

---

**오늘 쓴 파일들**

block.rb

yield.rb

---



git bash를 열어 -> `ls` -> `code block.rb`

:  vscode로 block.rb란 이름으로 새 파일을 저장하면서 연다



- block : 블록.  **중괄호{ } 혹은 do-end로 묶인 코드의 묶음**

  1. { } 중괄호를 써서 하는 방법
  2. do.. end 로 싸는 방법

  ​	

  - ex. each라는 method가 do-end로 둘러싸인 block을 보냄
  - 1. 로 표현한 애는 모두 2.로 표현 가능. (vise versa)
    2. 

- **map** :  각 배열 값들을 바꾸려면 배열 하나 새로 만들어서  넣었어야 했는데.

  `.map!` method 를 써서 간단히 가능.

  (`.each`다음으로 자주 사용할 method. 아예 배열 내 값을 바꿔줌)

  

- 블록에 대하여 :  'yield.rb' 파일 코드 볼 것!!

  => 함수 뒤에 { } 중괄호(블록)가 붙었다는 것은 그 함수 정의한 내용 안에 yield가 무조건 있다는 것!!! 









---

# 루비온레일즈 day2 시작  

### :  c9에 새로운 프로젝트 'final-board'

##### (blank템플릿 말고 ruby on rails템플릿으로 만들었다)

---



- 레일즈는 MVC패턴으로 전체 구조가 되어 잇다



1. 일단 컨트롤러를 만들어 준다.

   콘솔창에 `rails g controller posts index new show`

   ==> 그럼 아래와 같이 컨트롤러가 생성되자. index / new / show 페이지 코드랑 같이 ㅎㅎ

   ==> index.html.erb / new.html.erb 등등 이 views폴더 안에 다같이 생성된다

   ![1529979520091](C:\Users\student\AppData\Local\Temp\1529979520091.png)

   

2. config -> routes.rb 에 아래 3번 사진의 코드를 써 준다.

   

3. 서버 켜자

   ![1529979258069](C:\Users\student\AppData\Local\Temp\1529979258069.png)

   - 이제 서버 돌릴 때는 그냥 저 run project버튼 눌러주면 된다

   

4. 루트 페이지(index.html.erb) 코드를 써 준다

   ![1529979413492](C:\Users\student\AppData\Local\Temp\1529979413492.png)

- 레일즈는 이름을 서로 잘 맞춰줘야 한당!!!!

- 딱 /posts url요청이 오면 routes(문지기 파일)을 살펴본다. 이 요청을 받아도 되는 건지. 그러면 컨트롤하는 애한테 넘겨줌. /posts/new 이런 걸 알아볼 수 잇다고 판단되면. (posts 컨트롤러 안에 있는 new라는 액션을 불러옴) 

  -> posts컨트롤러 안에 있는 

  ```Ruby
  def new 	#액션들
  	#항상 이 부분에 렌더 코드
      #render 'posts/new' 
      #코드가 숨어있다고 생각하면 된다 (이름이 같다면 자동으로 렌더해줌)
  end 
  ```

  가 실행될 것

  -> 액션과 렌더할 파일 이름이 같다면 자동으로 렌더를 해줌!

- 문지기 파일 (routes.rb) 에 get방식으로 정의를 해 줘야 한다.

  ![1529980040490](C:\Users\student\AppData\Local\Temp\1529980040490.png)

  

- -> 그 다음 2. 컨트롤러에도 액션을 정의해 줘야 한다

  ![1529980075542](C:\Users\student\AppData\Local\Temp\1529980075542.png)

  

- -> 그 다음 3. views 폴더 안에도 html.erb페이지 만들어 줘야 한다 (같은 이름으로 맞춰줄 것)

  (error :  missing template / 에러메시지가 이와 같이 난다면 이 단계를 안해준것!!)

  ![1529980166744](C:\Users\student\AppData\Local\Temp\1529980166744.png)





---

### 이제 그 다음 db 테이블을 만든다

==> model

1. `rails g medel Post title content`   --> 옆에 내가 생성할 column도 같이 말해주면 같이 생성된다

   - cf. `content: string` 이런식으로 자료형을 말해줄 수도 있지만.  디폴트값이 스트링이기 때문에 스트릴일 경우엔 생략.

   ![1529980426087](C:\Users\student\AppData\Local\Temp\1529980426087.png)

   - 아래 빨간네모가 db 설계도가 생성된 파일 위치

   

2. 실제로 db 테이블을 만들어 주는 명령어 ==> rake

   - 우리는 rails 4.x 버전을 쓰고 있음. 4점대.   ==> 명령어  model 과 rake 가 나뉘어 있다.

   `rake db:migrate`

   - -> schema.rb 가 생기며 db에 넣는 코드가 생성됨 (sql)

   ![1529980622335](C:\Users\student\AppData\Local\Temp\1529980622335.png)

   

3. create 액션에 가서 

   ![1529980675603](C:\Users\student\AppData\Local\Temp\1529980675603.png)

   db에 넣을 코드를 정의해 준다

   

4. 데이터를 넣어보자

   ![1529980778107](C:\Users\student\AppData\Local\Temp\1529980778107.png)



5. 콘솔에서 확인 가능 ( SQL 글자 확인)

   ![1529980846744](C:\Users\student\AppData\Local\Temp\1529980846744.png)

   

+ 더 예쁘게 보기 위해 rails db gem 을 깔 수 있당 ㅎㅎ
+ 혹은, 레일즈는 콘솔을 통해 모든 것이 확인 가능

`rails console`

![1529981025621](C:\Users\student\AppData\Local\Temp\1529981025621.png)





- cf. `.methods.sort` 하면 알파벳순으로 정렬됨

  ![1529986293726](C:\Users\student\AppData\Local\Temp\1529986293726.png)

  ![1529986313784](C:\Users\student\AppData\Local\Temp\1529986313784.png)



- 게시글 제목으로 찾을 수도 있다 (Post 테이블에서 title  column  항목)

![1529986410998](C:\Users\student\AppData\Local\Temp\1529986410998.png)

그 외 ex. 

app 에 우리 어플리케이션이 들어가 잇음.

`app.get 어쩌구 `하면 어쩌구  페이지 요청을 보내줌 ==> 해당 페이지가 잘 작동하는 지 볼 때 사용

ex 2.

`app. response.remote_ip`

사람들의 아이피를 가져와서 어떤 아이피가 썼는지 추적도 할 수 있다.



---

### 게시판 글 수정하기 버튼/기능 추가하기 



##### cf. 링크 걸려있는 요소 위에 마우스 커서 올려 놓으면 (hover) 웹브라우저 창 하단에 그 연결된 링크 url이 나옴

![1529987504043](C:\Users\student\AppData\Local\Temp\1529987504043.png)



1. routes.rb파일에서

![1529988811476](C:\Users\student\AppData\Local\Temp\1529988811476.png)



2. 컨트롤러에서. 

![1529988734548](C:\Users\student\AppData\Local\Temp\1529988734548.png)



3. views폴더에서

![1529988972393](C:\Users\student\AppData\Local\Temp\1529988972393.png)





---

### 삭제하기 기능 만들기

![1529990446146](C:\Users\student\AppData\Local\Temp\1529990446146.png)

![1529990428734](C:\Users\student\AppData\Local\Temp\1529990428734.png)



---

### 회원가입 기능도 붙이기 ㅋㅋ

- 컨트롤러 C는 M모델에 따라감. (한 쌍으로)
- 이제까지 posts 컨트롤러로 했는데. 이제 user컨트롤러 따로 만든 상황을 가정해서 users  url로 다시 만들어 주자

(url에 /posts/edit 이런식으로 햇던 것들을 users로 해보자. 복수형으로 쓰는 것은 관례.)

![1529990774210](C:\Users\student\AppData\Local\Temp\1529990774210.png)

-> users 컨트롤러 만들어 준다   (필요한 액션은 회원가입/로그인/로그아웃/회원탈퇴 4가지로)

`rails g controller users signup login logout getout`

![1529991341049](C:\Users\student\AppData\Local\Temp\1529991341049.png)





-> model로 우리 db의 설계도를 만들어 준다

`rails g model User username password`



-> `rake db:migrate`



-> view폴더 페이지 파일들 코드 써준다

![1529991393242](C:\Users\student\AppData\Local\Temp\1529991393242.png)





* 회원가입에서 아이디 이미 존재하는지 여부 체킹 ==> 

  `User.find_by(username: "김루비")`

(안 찾아질 경우 nil이 뜬다. ==>  nil == false 이다)

![1529993367411](C:\Users\student\AppData\Local\Temp\1529993367411.png)



*cf. `unless`는 그냥` if not`으로 해도 된다

unless 나 if는 앞에 대문자로 하지 않도록 유의 ( 나 자꾸 오타냄 ㅠㅠ 주의)

*cf. <!--컨트롤러는 무조건 복수로 쓰는 게 관례-->

- **레일즈에서 session쓰기!!  (enable sessions 이런 거 썼던 거 안써도 된당)**

  ![1529994414839](C:\Users\student\AppData\Local\Temp\1529994414839.png)







![1529994716243](C:\Users\student\AppData\Local\Temp\1529994716243.png)

![1529994879001](C:\Users\student\AppData\Local\Temp\1529994879001.png)

로그인 돼있을 때만 나오도록 함. (로그아웃 눌렀을 때 에러가 뜬다면 저 조건문을 추가해줘봐바











---

---

### 에러,  단계별 3가지

1. 루트 문지기 페이지가 없다

![1529988033976](C:\Users\student\AppData\Local\Temp\1529988033976.png)



![1529988082895](C:\Users\student\AppData\Local\Temp\1529988082895.png)



2. 컨트롤러에 액션이 없다

![1529988114356](C:\Users\student\AppData\Local\Temp\1529988114356.png)

![1529988132576](C:\Users\student\AppData\Local\Temp\1529988132576.png)



3. 템플릿이 없다

   ==> views 폴더 안에 해당 .html.erb 파일을 만들어 준다

---







---

### ORM 이 다름. 시나트라는 datamapper / 루비온레일즈는  Active Record

but. 문법이 비슷해서 get으로 하던거 find로 하고 그런 조금의 차이만 있을 뿌니당

##### 1. `.find`      vs.     `.find_by`

​	1) `User.find(고유한 id값)`

​		ex. `User.find(1)`

​		ex. `User.find(200)`



​	2) `User.find_by(찾고자 하는 필드: 값)`

​		ex. `User.find_by(username: "김루비")`

​		ex. `User.find_by(password: "1234")`



​	** 중복되는 친구가 있으면 어떻게 돼요?



---

### <과제>

1. 회원정보수정

   users/edit/

   users/update/

2. 오늘 한 거 처음부터 해보기

---

