- 수업 마지막에 한 **c9** 프로젝트 이름 :   '**asked2**'

  

### bundler로 필요한 gem들 한번에 깔기

1. c9에 Gemfile을 만든다
2. Gemfile에 밑에 코드 쓴다

```Ruby
source 'https://rubygems.org'   #항상 똑같은 줄. 루비 gem들을 다 모아놓은 사이트. 루비gem들 관리하는 사이트
#들어가보면 다운한 사람 수. STATUS이런 데에
#Gems에 알파벳 order로 나와있음

gem 'sinatra'
gem 'sinatra-contrib'

#datamapper 관련 Gem들
gem 'json', '~> 1.6'
gem 'data_mapper'
gem 'bcrypt'
gem 'dm-sqlite-adapter'
```

3. 콘솔창에 `gem install bundler`

4. 다 깔리고 나면 또 콘솔창에 `bundle`  ==> 파일 안에 있는 gem들이 깔린다.

   ( #다 깔리고 나면 `Gemfile.lock`이란 파일이 새로 생긴다.  이 파일 열어보면 깔린 gem들이 나온다 )



##### 서버 열 때 !!!! bundler썼으면!!!!!  `bundler exec ruby app.rb -o $IP`   라고 써야함 !!!!

*exec => execute : 실행하다



### db 쓸 때 필요한 코드

(`require 'data_mapper'` 밑에 써줍니당.)

```Ruby
DataMapper::setup(:default, "sqlite3://#{Dir.pwd}/blog.db")

class Post
  include DataMapper::Resource
  property :id, Serial
  property :title, String
  property :body, Text
  property :created_at, DateTime
end

# Perform basic sanity checks and initialize all relationships
# Call this when you've defined all your models
DataMapper.finalize

# automatically create the post table
Post.auto_upgrade!
```



##### ex.   DataMapper로 데이터베이스 표 만들기!!

```Ruby
require 'sinatra'
require 'sinatra/reloader'
require 'data_mapper'

DataMapper::setup(:default, "sqlite3://#{Dir.pwd}/question.db")     #db 이름을 question으로 바꿔줬음

class Question      #엑셀 파일 하나 안에서 Sheet에 해당. Sheet 이름을 Question으로 해주었다. 첫 글자 대문자로 해야함 유의
  include DataMapper::Resource      #column이 3열인 표를 만듦
  property :id, Serial
  property :name, String        #스트링과 text는 거의 같음. text가 더 많은 글자를 저장할 수 있는 것이 차이
  property :question, Text
  #property :created_at, DateTime       #그냥 안만들 거에요
end

# Perform basic sanity checks and initialize all relationships
# Call this when you've defined all your models
DataMapper.finalize

# automatically create the post table
Question.auto_upgrade!      #계속 자동으로 업데이트 해주겠음. 이 코드 덕분에 id값 (순서 1,2,3,...)은 자동생성됨


get '/' do
    @questions = Question.all      #다 프린트하겟다
    
    erb :index  #페이지를 렌더하겠다. 이 줄 없어도 layout.erb 페이지가 먼저 실행되겠징.
end

get '/ask' do
    @name = params[:name]       # : 이 붙은 거는 Symbol이라고 함. String과 유사하지만 다르다
    @question = params[:question]
    
    Question.create(        #Question 표에 한 줄 한 줄 추가하겠다 :  .create
            name: @name,        #name column에는 @name을 넣겠다. (내용으로)   #,  콤마 주의!!!
            question: @question        #question column(열, 항목)에는 @question을 넣겠다. (내용으로)
    )
    redirect '/'
    #erb :ask
end

# 데이터베이스를 새로 만들었으면 서버 한 번 껐다 켜주는 것이 좋음
# 데이터 추가될 때마다 . 한 줄 한 줄 각각이 배열로 들어온다. [name, question]
```



---

##### 다음주는 CRUD(크루드)의 주입니다  ===> 데이터베이스 모든 서비스는 크루드에요.

C Create	

R Read

U Update

D Destroy







### 아래는 어떤 날 했는지 헷갈리는 메모 옮김 (csv한 날 한 건 맞음)

---

* foreach :   csv.foreach File.foreach

  한줄씩 '읽는거' read
  { }

* `File.open("파일명","할 것")`

#### <다음에 할 것들 예고>

- Block / 환경변수(비번을 환경변수에 저장해서 몰래 우리만 쓰는 법) / 파일이 없을 때 처리 (이건 안할 수도 있음) / String 글자 조작
  합체 수술 .method 정도 했었는데 이제 더 여러가지 해볼거야. 
  cf. 수술은 (스트링 안에 변수넣기) #{ } 로
  / Symbol (params로 갖고올 때 : 하고 썼던 것)
  / 배열 조작. 해쉬도. 배열이랑 해쉬 자료구조는 전문적으로 상세하게 잘 알아야함!

`.push`  =  `<<`  (같은 거다) 
shift
pop?

select / reject



/ **범위** (우리 로또할 때 1~45했던 것) 범위 안에서 반복도 할 수 있고 자료를 돌릴 수 있다.

/ 가장 많이 쓸 것이 **해쉬**
해쉬와 닮은 파일자료구조 **json**

---

