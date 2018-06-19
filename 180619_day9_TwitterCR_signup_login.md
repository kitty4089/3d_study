##### 오늘의 c9 프로젝트

## :  twitter_cr



- 회원가입. 로그인 서비스

---

### 트위터 만들기(아침 예제)

'/' -> index.erb
  1. <form>
    - 이름(name) & 내용(content)
    - '/create'로 보내기
  2. Database에 저장된 모든 글 보여주기

'/create' -> 없음
  1. 제목 & 내용 Database에 저장
    - Database의 이름은 Twitter.db
    - Table의 이름은 Tweet
    - Table의 column은 id(Serial), name(String), content(Text), created_at
    - 트윗 저장(Database에 저장)
  2. 모든 저장 완료 후, redirect '/'

---



### 첫 단계

Gemfile(views밖에) 만들어 준다 ==>  **bit.do/gemfile-3d*   에 올라와 있어요

-> gem install bundler

-> bundle

-> 다 깔리고 나면 좌측에 Gemfile.lock 파일 만들어짐. 우리 gem 다운된 목록들 파일인 거

---

cf. 10minutemail.org



- db를 건드렸으면 서버 껐다 켜줄 것

  

### model.rb 에 넣는 db 코드

(https://github.com/43dp/sinatra_tutorial)

```Ruby
DataMapper::setup(:default, "sqlite3://#{Dir.pwd}/twitter.db")

class Tweet
  include DataMapper::Resource
  property :id, Serial
  property :name, String
  property :body, Text
  property :created_at, DateTime
end

# Perform basic sanity checks and initialize all relationships
# Call this when you've defined all your models
DataMapper.finalize

# automatically create the post table
Tweet.auto_upgrade!
```



### 회원가입 권한주는 절차

1.  db에 있는 사람인지 확인 (id)
2. 만약 db에 있다면
3. pw가 동일한지 확인
4. 권한주기





### 아이디 / 비밀번호 암호화

=> 암호화 하지 않고 다 보이게 하면 큰일남. 감옥감. 법적으로 닷컴버블 이후!! 법이 복잡해지면서 암호화 필수!

=> 그냥 값 받으면 url에도 내가 만든 /admin 페이지에도 막 다 보임



- 유럽 입자 물리 연구소에서 CERN에서 팀 버너스리가 웹을 처음 만들었음

- cf. 모뎀; 전화선을 통해서 인터넷 연결했음. 전화통화와 동시 사용 불가능했음. 승진오빠 세대 옛날 것 고대 것

  

- http(Hypertext Transfer Protocol) :  html문서를 주고받는 인터넷 통신규약

  - Hypertext :  우리가 계속 하던 html

  - 무상태성(Stateless) :  어떤 상태를 저장하지 못함

    유저의 상태를 저장할 수 없음/ 특정 고객(유저)의 상태를 저장하지 못함

    **==> http자체만으로는 로그인 서비스를 실제로 구현할 수 없음**

    

    => (우리가 db Tweet 만들어서 했던 것처럼) 회원가입을 통해서 서버 db에는 저장이 됐을 것 

    => 그런데 고객 1번이 우리 db에 저장된 사람이 맞으니까 그 뒤로는 계속 어떤 승인을 해줘야 하는데 (상태가 저장되어야 하는데) http는 저장을 할 수 없음

    **=> session이라는 sinatra 기능 쓸 거에요** => *쿠키*

    => 저장을 못하니까 서버는 몰래 고객1에 쿠키(ex. 오레오)를 심어놔 (해당하는 중요한 정보를 고객의 컴퓨터에 심어놓는다) -> 다음 요청이 들어올 때는 계속 이 오레오를 같이 보내게 됨

    *cf. 마치 헨젤과 그레텔이 쿠키 조각들 크럼블 떨어트려놔서 집을 찾아왔듯이 그런 역할이라서 쿠키임*

    - 예전에는 쿠키를 썼는데 요새는 잘 쓰지 않음 

      => 보안의 위험. 문제가 있음 :  고객 3이 쿠키를 발급받지 못했는데 쿠키가 텍스트 파일처럼 저장돼 있기 때문에 발급받은 고객2의 쿠키파일을 그대로 가져와서 작업하면 문제없이 해킹 가능

      => 쿠키는 고객한테 저장하는 것이기 때문에 발생한 문제

    - 검색기록은 쿠키로 쓸 수 있다. 이제 그래서 로그인 서비스에는 쿠키 잘 쓰지 않음

    - 구글 같은 거는 우리의 쿠키정보를 다 읽어서 검색어 패턴 기반 맞춤형 서비스 제공하는 거임.

      ==> 내가 wconcept에서 봤던 상품들 바로 다른 뉴스 볼 때 옆에 뜨는 이유 ==> 쿠키, 검색기록 지우면 되긴 할 거야... 걔네가 또 저장해 놨을 지는 모르지만..

      ###### ==> *cf. gdpr* 외국에 까다로워진 개인정보보호정책



#### session

- session을 통해 유저 정보 저장 :  

- 고객이 어떤 정보를 통해 **로그인**을 했다 -> 어떤 특정 고객이 인증을 받았을 때, db에 있는 정보와 이 고객이 인증받은 정보가 동일하다(일치한다)면,

  -> 인증된것. session이 그 인증된 사실을 저장하는 또 하나의 저장소. 

  - 서버에 있음. 우리한테 있는 것. 

  **=> 이 사람의 인증 정보를 우리가 갖고 있을 수 있게 된 것.**

- 조건문이 2개 있다고 보면됨.

  1) id가 db에 있는 지  -> 없으면 회원가입 페이지로 돌림

  ​				     -> 있으면 패스워드 조건문으로

  2) 패스워드가 일치하는지

##### 로그인 승인한다 == session에 저장한다 (sinatra)



- 'sinatra session' 구글링 ㄱㄱ
- params는 hash와 비슷 params[:name]

![1529386493301](C:\Users\student\AppData\Local\Temp\1529386493301.png)

cf. 해쉬  key 와 value   이름표 => value

session도  session [key] = "value"

- 유저를 id값으로 인식한다. (번호, 숫자로) email 값으로 인식하는 게 아니라. 

  => 검색이 쉽고 엄청 빠름

  => 특정인 id값 1번인 사람이 들어오면 거기의 email값이 있지만(아이디) 그 email이 뭔지도 모른다. 그분은 1분일 뿐.

  **=> session의 key가 id가 됨 / value가 해당 id값 번호로 들어가고**



### ==> session도 서버 껐다 켜야 저장돼요

: 제대로된 id와 비밀번호로 로그인 햇다면 계속 모든 페이지에 아이디가 뜬다 (우리 프로젝트)

==> 사용자 로그인 기억하는 것



#### layout에 넣어야 할 조건문

![1529389201150](C:\Users\student\AppData\Local\Temp\1529389201150.png)



#### cf. 루비에서는 거짓말만 아니면 다 True



`.nil?`   :   Array나 Hash에 비어있니? 물어보는 method

**`[].nil?`  / `{}.nil?` 도 True가 아니고 False다 ==> '없다'라는 요소가 있는 거로 인식.







#### cf. 페이지 소스보기 주석에 장난 많이 쳐놓는다. 

ex. Khan Academy

https://www.khanacademy.org/

![1529391169536](C:\Users\student\AppData\Local\Temp\1529391169536.png)