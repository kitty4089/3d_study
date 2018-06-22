## 아침 과제

회원가입 & 로그인

'/' -> index.erb
  1. '홈(/)', '회원가입(/signup)', '로그인(/login)' 링크만들기

'/signup' -> signup.erb
  1. <form>으로 email, password 받아서,
  2. '/register'로 보내기

'/register' -> X
  1. User.create로 새로운 User를 만들고,
  2. '/'로 redirect     

'/admin' -> admin.erb
 1. 모든 User를 불러와 보여주기

    

'/login' -> login.erb
  1. <form>으로 email, password 받아서,
  2. '/session_new'로 보내기

'/session_new' -> X
  1. 로그인 로직 구현(유저 검증 == DB에 저장된 유저인지 확인)
  2. 만약 유효한 유저라면
    session[:email]에 유저 저장
    redirect '/'
    아니면
    redirect '/login'

---





cf. **텔레그램**... 카톡같은. 보안이 뛰어남

- 러시아 존잘남이 만듦. 얼굴도 코딩도 짱짱맨

- 보안적으로 완벽한 메신저 앱을 만들 거다 해서 만든것

  telegram.org

- 프로그래머 입장에서 봤을 때 진!짜 잘 만든 앱. 아름다운 앱

- 러시아 석유재벌한테 1조원받고 팔아서 20대에 1조원 가짐

- 보통 멀티디바이스 지원이 안되는데 (모바일?) 얘는 됨. 

- 메신저에서 갑오브 갑이래

- telegram ico 가장 성공적인 ico래. 거의 1조원 모았대. 몇 억 인구가 쓰는 엄청난 앱.

- 경찰이나 정부가 보지 않았으면 좋겠는 것들은 다 텔레그램으로 써요.

- 웹버전도 있어요. 프로그램 설치 필요 x

- 시스템을 잘 만들어 놔서 챗봇 만들기가 정말 쉬워요



## 텔레그램 챗봇

BotFather 와 대화창  start -> /newbot 입력 -> 이름 정하기

![1529460779187](C:\Users\student\AppData\Local\Temp\1529460779187.png)



이름 정해지면 아래와 같은 메시지가 나옴

![1529460962430](C:\Users\student\AppData\Local\Temp\1529460962430.png)

메시지에서 맨 아래 파란 링크로 들어가 (새 창에서 열어)



-> https://core.telegram.org/bots/api   텔레그램 봇 api 주소로 들어가서

-> Making requests 내용에서 가이드를 본다

![1529461079244](C:\Users\student\AppData\Local\Temp\1529461079244.png)

-> 새 창에 위 표시해놓은 곳 같은 주소를 써 줄 건데

- <token> 부분에 아까 봇파더가 봇이름 정해지고 보내준 메시지에 링크 위 빨간 글씨들 복붙해준다.
  - 열쇠같은 거래
- METHOD_NAME 부분에는 내가 할 것들을 정해주면 된다

![1529461179574](C:\Users\student\AppData\Local\Temp\1529461179574.png)

##### MEHOD_NAME에 쓰는 하려는 것들 ex.

- **getMe** ==> Json형태로 **내 정보**가 나온다

* **getUpdates** :  내 봇의 상태 업데이트

![1529467412285](C:\Users\student\AppData\Local\Temp\1529467412285.png)

*api에서 **sendMessage** 부분 참고

- 특히. id에 내 챗봇의 id번호를 입력하면  '챗봇이 챗봇한테는 메시지 못보낸다'는 에러메시지가 나옴





![1529462207308](C:\Users\student\AppData\Local\Temp\1529462207308.png)

위에 클릭하면 내 챗봇과 대화 가능

![1529542343032](C:\Users\student\AppData\Local\Temp\1529542343032.png)

/getMe화면!!



![1529467292273](C:\Users\student\AppData\Local\Temp\1529467292273.png)

getUpdates에서, 빨간 사각형 표시 중에 밑에 표시한 것이 내 아이디인 것.

==> **sendMessage**할 때 url에 *id 부분에 저 아이디 쓰고 & text=나에게 보낼 메세지* 쓰면 됩니당

아래와 같이 쓰면 'wow it's working' 이라는 메시지가 내 텔레그램으로 보내진당

ex.

https://api.telegram.org/bot397628463:AAEC4uGnenoBkFna1a3FLbXTdqW-yqCgS2U/sendMessage?chat_id=573960813&text=wow it's working



![1529540845742](C:\Users\student\AppData\Local\Temp\1529540845742.png)

보내진 모습



- url로 치면 아래와 같은 페이지가 나오고 텔레그램 메신저에 메시지가 와있당

![1529542025266](C:\Users\student\AppData\Local\Temp\1529542025266.png)









### 메시지 보내는 코딩 vscode에서 .rb로 저장. 

#### -> 코드 실행은 git bash에서.

​     :  해당 디렉토리로 이동 `cd`로 -> `ruby telegram.rb` 루비야 ~~.rb 파일 좀 열어줘.

![1529541352047](C:\Users\student\AppData\Local\Temp\1529541352047.png)

```Ruby
require 'httparty'  #우리(나)를 대신해 (url)요청보내주는 애
require 'uri'  #한글 쓰기 위해서 uri로 인코딩 해 줘야 한다. 

url = "https://api.telegram.org/bot"    #반복되는 부분을 url이라는 변수 안에 넣었다

# +bot+token(봇파더에 있다)+/sendMessage?chat_id=XXX&text=hello"

token = "  "

id = " "     #챗봇 아이디 말고 내 아이디 넣어야 함 메시지 보낼 때는
msg = URI.encode("와우 행복한 점심시간")
url + token + "/sendMessage?chat_id=#{id}&text=#{msg}"

#res = HTTParty.get(url+token+"/getMe")    #임시변수 res(response)에 받아온 결과물을 받아온다
#json :  parsing 해서 해쉬처럼 정보를 쓸 수 있다

#hash = JSON.parse(res.body)     #받아온 정보를 해쉬에 담자

HTTParty.get(
    url + token + 
    "/sendMessage?chat_id=#{id}&text=#{msg}"
)

#puts hash
```

==> 루비 코드 짠 모습



![1529541195643](C:\Users\student\AppData\Local\Temp\1529541195643.png)

==> git bash에서 코드 실행





- 메시지를 보낼 때마다 아래와 같이 **getUpdates**에서 보내진 내역을 볼 수 있다.

  ![1529541852876](C:\Users\student\AppData\Local\Temp\1529541852876.png)