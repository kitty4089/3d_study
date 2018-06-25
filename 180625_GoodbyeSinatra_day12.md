

고객 Client <---> 서버 Server

#### 웹의 2가지 (서버에) 요청 방법

1. **get**  ==> **디폴트 방법** (이제까지는 method="get"이 생략되었던 것.) 

   - 입력한 것이 url에 노출된다

2. **post**

   - 입력 내용이 url에 노출되지 않는다
   - 따라서 url로 id/password 써서 회원가입 하는 것도 불가능.
   - url에 (브라우저에) 주소를 찍어 보내면 무조건 get 요청이다.

   `<form action="/" method="post">`

   `</form>`

---







---

#  Ruby on Rails   START

지금까지는 **sinatra** 라는 프레임워크(Framework)를 썼어요.

기본적인 구조나 필요한 건 다 해줄게

넌 그냥 좋은 웹서비스를 만드는데 집중해!



우리가 사용할 프레임워크

Ruby on Rails

==> 2017년 최고 연봉을 받는 개발자들



초보자가 가장 배우기 쉽다.

가장 인기있는 풀 스택 프레임워크 (최근엔 javascript로 넘어가고 있긴 한데!)

가장 ㅃ르게 내가 원하는 걸 만들 수 있다.

ex. 게시판도 5초면 만들어요



**M V C 구조**

**M : 데이터를 관리**- database :  model.rb

**V : 사용자가 보는 화면** - 유저에게 보여주는 페이지들 : views 폴더에 모두

**C : Controller : 중간 관리자** - app.rb (요청 들어오면 app.rb에서 일단 찾는다. (받을 수 있는 요청인지 아닌지))

- 사용자로부터 요청이 오면 **M <-> C- > V** 과정을 거쳐 다시 사용자에게 보여진다.



무언가를 요청(Request)하고 받는다 (Response)

브라우저가 받은 html파일을 예쁘게 보여지도록 한다.





---

## c9에서 blank가 아니라 ruby on rails 를 선택해 프로젝트 생성

#### -> 좌측에 이미 우리가 편하도록 다 깔아져 있는 폴더/파일들 봅시다

- **'app' 폴더**를 가장 많이 쓸 거다

- 그 다음 **'config' 폴더** (그 안에 또 든 게 많은데 다는 안씀)

  - 이 중에서 가장 많이 쓸 것은 **'routes.rb'**
    - route : 길 / routing : 길잡이를 하겠다
    - '/'  --> index.erb   이런식으로 했던 것.
    - app.rb로 썼던 게 파일 단위로 쪼개지는.

- controller 먼저 만들게 될 것.

- rails에서는 절대 새 파일 만들고 하지 않음. 이미 있는 명령어들 써서.

- rails에서 일 시킬 때는 항상.

  `rails generate controller 컨트롤러 이름`

  : 레일즈야 생성해줘 ~ (콘솔창에 쓰는 거)





1. 콘솔창에 `rails generate controller home`    :  레일즈야, home이라는 컨트롤러 생성해줘

![1529893666589](C:\Users\student\AppData\Local\Temp\1529893666589.png)



폴더들 안에 아래와 같이 생김   **(config / routes.rb)**

![1529893715418](C:\Users\student\AppData\Local\Temp\1529893715418.png)



cf.  이제까지는 routing과 controller를 하나로 정의했었음

```
get 'url' do

end
```

하던 게 routing    do/end  사이에 적었던 것들이 cotroller





2. config안에 routes.rb

![1529893882715](C:\Users\student\AppData\Local\Temp\1529893882715.png)

홈 컨트롤러에 인덱스 액션으로 보내라.

home_controller 안에 index 액션을 정의한다.

```Ruby
def index
	render 'home/index'		#erb :index  하던 거랑 비슷한 거임
end
```









정리하면,

순서가

1. config 안에 routes.rb
2. '/' -> index.erb 렌더
3. controller 입력



1. get 요청은 config 안에 routes.rb에서 한다.
2. home 폴더 안에 페이지들 정의  .html.erb로 특정해 줘도 되고.  그냥 원래 하던대로 .erb 라고 해도 된다.

![1529894668496](C:\Users\student\AppData\Local\Temp\1529894668496.png)





* 강력한 레일즈의 장점 :  렌더 (erb :index 이런거 . 마지막으로 view를 생성해 내는) 안해도 된다.
  - render를 위해 render함수가 호출될 경우 -> erb 파일이 '컨트롤러/액션.erb'일 경우 생략 가능



### 즉, 이름이 똑같을 경우 생략 가능. 

## **def 메쏘드 정의하는 '액션'명 = 컨트롤러 하위의 erb의 파일명**

### 일 경우



### *레일즈 약속

![1529901004755](C:\Users\student\AppData\Local\Temp\1529901004755.png)

1. 액션의 이름과  erb의 이름을 항상 같게 해준다.
2. '컨트롤러/액션' => '컨트롤러#액션'  이 쌍의 이름이 서로 같다면  =>이후 생략 가능. 
   - 즉 '컨트롤러/액션'만 쓰면됨.

ex.

![1529901434861](C:\Users\student\AppData\Local\Temp\1529901434861.png)

즉, def로 액션 정의 할 때, 

원래 그 안에 render 'home/search'  (시나트라에서는 erb :search)라고 해줬어야 하던거.

안해줘도 되고  views 하위에 search.erb로 액션이랑 같은 이름을 가진 erb파일만 만들어주면 됨.

---





시나트라에서.				루비온레일즈

1. app.rb -> get 'url'			1. config / routes.rb  파일 건드리는 작업
   1.      					2. ​				2. get '/' 이런 컨트롤러가 컨트롤러로 따로 떼어져 있음  => 어떤 요청을 받을지
                   					1. views    		3. 뭘 보여줄지. 







cf. 단축키 : **ctrl + e  :   파일명 찾기 .  대충 입력해도 된다. fuzzy search**



---

cf. git init  하면 숨김폴더로 .git이 로컬에 생김

 `git remote add origin https://github.com/kitty4089/ruby_on_rails.git`  이거는 리포지토리 새로 만들었을 때만 처음 한 번만 필요한 명령어. 로컬 폴더 등이랑 (지금 우리는 c9서버랑 연결했지만은)  깃헙 온라인이랑 연결해주는 명령어. 

#### 깃헙에 새로 리포지토리 만들어서 c9이랑 연결하기

![1529904201842](C:\Users\student\AppData\Local\Temp\1529904201842.png)

![1529904301674](C:\Users\student\AppData\Local\Temp\1529904301674.png)





---

- 데이터 테이블마다 컨트롤러가 하나씩 일대일로 존재.

  - 컨트롤러 새로 만들기 :  `rails generate controller 컨트롤러 이름`

    cf. `rails g controller 컨트롤러 이름` 이렇게 generate을 g로 줄일 수 있다

### 포스트 crud 크루드 레일즈에서 해보기

![1529904584240](C:\Users\student\AppData\Local\Temp\1529904584240.png)



![1529904539100](C:\Users\student\AppData\Local\Temp\1529904539100.png)







---

- 모델 이름은 앞에 대문자로 쓰는 게 관례래.  소문자로 써도 애가 알아서 대문자로 인식해주긴 한대.

- Class Post

  end

  로 해서 db 테이블 만들던 과정.

  - 만들 column들. 자료형.
  - 자료형 기본 디폴트값은 stirng이라서 안써도 된다. 스트링이면  원래는 content:string 이런식으로 써줘야한대.

![1529905612843](C:\Users\student\AppData\Local\Temp\1529905612843.png)



- 여기까지 model을 쓴 거는. 실제 엑셀 '파일'을 만든 게 아니고. 앞으로 이런 엑셀파일 테이블을 만들거다 라는 설계도까지만 준 것.

- 실제 db **'파일'**을 만드려면. 

  또 `rake db:migrate` 라고 쳐줘야 함.    migrate안에 든 파일을 실제로 db에 넣겠다.

  ![1529905765118](C:\Users\student\AppData\Local\Temp\1529905765118.png)

  

  -> rake로 db에 넣어라 하면 **schema.rb** 가 생긴다 .(좌측 리스트에서 확인 가능)

  ​		==>  db넣을 코드를 생성해줌.

  ![1529905840549](C:\Users\student\AppData\Local\Temp\1529905840549.png)



이런 sql 쉽게 db 넣어주는 애들  **orm**  이라고 한다. orm 덕분에 우리가 이렇게 쉽게 코드 몇 줄로 데이타베이스를 제어 가능한 것. ㅎㅎ



![1529906633135](C:\Users\student\AppData\Local\Temp\1529906633135.png)

##### 위처럼 루비온 래일즈 콘솔창에 db 들어간 내용도 보여진다. (bash창 말고!!) 



##### ==> rails db 라는 gem을 깔면 db넣은 내용들을 시각적으로 깔끔하게 볼 수 있다~

- ![1529908112686](C:\Users\student\AppData\Local\Temp\1529908112686.png)

  Gemfile에 `gem 'rails_db' `추가



![1529908201390](C:\Users\student\AppData\Local\Temp\1529908201390.png)

똑같이 bundle이라고 쳐서 깔아준다.  ( 초록색 부분이 새로 깔린 gem들이고 검은색이 원래 잇던 애들)

여기까지 하고 나면,

- ![1529908341841](C:\Users\student\AppData\Local\Temp\1529908341841.png)
- 이런 게 생김

![1529908401704](C:\Users\student\AppData\Local\Temp\1529908401704.png)

바로 온라인으로 추가/삭제 가능 오오오오







- 전체 저장하기는  **File -> Save all**

  ![1529908714507](C:\Users\student\AppData\Local\Temp\1529908714507.png)



#### Seed data 넣기 (디폴트로 있는 데이터들)

- shema.rb :   우리 데이터 테이블의 구조
- seeds.rb  :  ex. 100번 돌면서 Post를 만든다

![1529908922027](C:\Users\student\AppData\Local\Temp\1529908922027.png)



![1529909090989](C:\Users\student\AppData\Local\Temp\1529909090989.png)

seed.rb에 코드를 써주고

배쉬 콘솔 창에는 `rake db:seed`



- 같은 내용 100번이 아니라 서로 다른 내용을 넣고 싶을 때!!
  - Gemfile에 faker 젬 추가

![1529909166506](C:\Users\student\AppData\Local\Temp\1529909166506.png)



cf. bundle 또 해 줄때도 서버 껐다 켜야 한다.  (db건드렸을 때도)



![1529909317745](C:\Users\student\AppData\Local\Temp\1529909317745.png)



일단 이전 데이터 날리기 위해 db를 날려준다

![1529909362927](C:\Users\student\AppData\Local\Temp\1529909362927.png)

함부로 쓰면 안되는 명령어!!! 이 한 줄로 그냥 db 다 날아간다!!



![1529909423416](C:\Users\student\AppData\Local\Temp\1529909423416.png)

migrate 한 번 더 해주고



그다음 seed.rb 파일에 rake



![1529909488078](C:\Users\student\AppData\Local\Temp\1529909488078.png)

이런식으로 막 이름이랑 이메일이랑 랜덤 시드 생성됨



==> 'faker gem'  구글링 ㄱㄱ

https://github.com/stympy/faker

![1529909606948](C:\Users\student\AppData\Local\Temp\1529909606948.png)

이런식으로 이용할 수 있는 Faker들이 엄청 많당

ex. Kpop 을 클릭해 보자

![1529909641075](C:\Users\student\AppData\Local\Temp\1529909641075.png)



또 아래와 같이 'seeds.rb' 에 넣어주면 된당

![1529909676987](C:\Users\student\AppData\Local\Temp\1529909676987.png)



![1529911055153](C:\Users\student\AppData\Local\Temp\1529911055153.png)

이런 식으로 ㅎㅎㅎ





#### 게시판 예쁘게 하기

![1529911619605](C:\Users\student\AppData\Local\Temp\1529911619605.png)

지금까지 적은 반복문을 테이블에 넣어준당!



![1529911806331](C:\Users\student\AppData\Local\Temp\1529911806331.png)

- created_at (생성날짜/일시)  를 짧게 만들어주기

  - 지금을 기준으로 해당 글이 언제 쓰였는지로 나타내기

    :  지금 시간 - 만들어진 시간

    ex. 25일 12:00		만들어진 시간 : 25일 11:00

    1시간 전 으로 나오게 하려면

    => time_ago_in_words  (레일즈가 제공하는 method) 를 쓰거나 / 우리가 손수 구현도 가능

    시간이 초단위까지 나온당.3600초가 나왔으면. 분으로 보여주고 싶으면 60으로 나누고 + "분 전"

![1529912324504](C:\Users\student\AppData\Local\Temp\1529912324504.png)

![1529912343791](C:\Users\student\AppData\Local\Temp\1529912343791.png)





##### 게시판 글 링크 연결하기

![1529912141645](C:\Users\student\AppData\Local\Temp\1529912141645.png)

a태그로 감싸주면

![1529912158058](C:\Users\student\AppData\Local\Temp\1529912158058.png)

이렇게 링크 연결되게 된다



![1529912219136](C:\Users\student\AppData\Local\Temp\1529912219136.png)

/:id 포함해주면 게시판 글들마다에 다 url 각각 연결이 된당   => 'variable routing'

==> params를 그대로 쓸 수 있다





- `.round`  :  뒤에 소수점 떼주는 루비 메쏘드

