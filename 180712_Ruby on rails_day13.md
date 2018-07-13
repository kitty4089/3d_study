18 .07 .12

## 관리자 페이지 만들기

- 서버에서 검사하는 거
- validation  텍스트 필트 태그 form태그에서 email태그는 email만 들어가고 그런 유효성 검사..

`validates(:title, presence: true)`

- **flash** :   메세지를 띄워주는 (rails문법)
- 글자 수도 지정해 줄 수 잇따.  validates로.

---

*c9 프로젝트  :  저번에 했던 **exhibition**에다가

* vscode 루비 코드 :  grid.html

---

![1531444476910](C:\Users\student\AppData\Local\Temp\1531444476910.png)

(3번 마지막 항목은 저번에 했던 것이므로 각자 해 볼 것!)







1.   Devise gem 설치   :   회원 관리 . 로그인, 회원 정보 변경 같은 거 해주는

   `gem 'devise'`

   `bundle`

   `rails generate devise:install`  devise 설치한다. rails에다가 설치.

   `rails g devise user`  : user 모델 만든다  devise로

   `rake db:migrate`   모델 만들었으니까 rake해준다



2. 또 gem 하나 더 배웠다.

   `gem 'devise-i18n'`  #한글로 번역해주는 애. password나 id나 등등

![1531375438566](C:\Users\student\AppData\Local\Temp\1531375438566.png)

![1531378173912](C:\Users\student\AppData\Local\Temp\1531378173912.png)

ko로 쓰겠다 바꿔준다



이제 본격 devise gem을 써보자

('gem devise i18n' 구글링 ㄱㄱ)

![1531381625592](C:\Users\student\AppData\Local\Temp\1531381625592.png)

제일 위에 웹페이지 들어가본당.

https://github.com/tigrish/devise-i18n

- 페이지 자체 아래로 스크롤 내려서 README.md  내용 보면  gem 사용법 알 수 있당

![1531385241384](C:\Users\student\AppData\Local\Temp\1531385241384.png)

저 코드 복사     `rails g devise:i18n:views`   :  view페이지들 모두 한글로 해쥼



콘솔창에 붙여넣기 . enter.

![1531378037457](C:\Users\student\AppData\Local\Temp\1531378037457.png)

애가 생김 



![1531378079728](C:\Users\student\AppData\Local\Temp\1531378079728.png)

이렇게 view페이지가 한글로 나옴



---

*cf.* 한글로 어떻게 번역되는지 알고 싶으면,

또 아까 그 깃헙  페이지 ('gem devise i18n' 구글링 ㄱㄱ)

https://github.com/tigrish/devise-i18n

==> 아래와 같이 잉여가 잘 정리해 놓았다

![1531381658164](C:\Users\student\AppData\Local\Temp\1531381658164.png)

위에 rails/lacales 클릭

![1531381675164](C:\Users\student\AppData\Local\Temp\1531381675164.png)

ko파일 보면  영어 <-> 한글 어떻게 호환되는 지 볼 수 있당

(언어마다 번역이 어떻게 되는지)

---





'gem devise' 구글링 ㄱㄱ

https://github.com/plataformatec/devise

![1531384599107](C:\Users\student\AppData\Local\Temp\1531384599107.png)

이 페이지 들어와서 쭉 스크롤 내려보면

![1531381700230](C:\Users\student\AppData\Local\Temp\1531381700230.png)

이 부분 빨간 박스 안에 첫 줄 복사한다. 아래와 같이 로그인이 되었냐? 이런 것들을 물어볼 수 있다



![1531381709587](C:\Users\student\AppData\Local\Temp\1531381709587.png)

복붙한다.  (저 첫줄 의미:  인증된 유저만 로그인 시키겠다)



![1531381738628](C:\Users\student\AppData\Local\Temp\1531381738628.png)

우리 model이름으로 바꿔준다



![1531381842190](C:\Users\student\AppData\Local\Temp\1531381842190.png)

관리자인지 확인하는 column추가

- 기본값 false라서 관리자일 때만 true



![1531381911074](C:\Users\student\AppData\Local\Temp\1531381911074.png)

db수정했으니 드랍하고 다시 마이그레이트 해준다



![1531381959179](C:\Users\student\AppData\Local\Temp\1531381959179.png)

seed에 관리자 계정 만들어 준당

(admin계정)

`rake db:seed`

![1531382052577](C:\Users\student\AppData\Local\Temp\1531382052577.png)

index페이지에 

로그인된 상태인지, 지금 유저가 관리자인지 .. ===> devise gem깔아서 가능한 부분





---

### 회원 등급 관리  - 양민으로 혹은 관리자로 

`rails g controller admin`

![1531372925928](C:\Users\student\AppData\Local\Temp\1531372925928.png)

콘트롤러가 생겼따

![1531373484061](C:\Users\student\AppData\Local\Temp\1531373484061.png)

![1531382206836](C:\Users\student\AppData\Local\Temp\1531382206836.png)

route 정의



우클릭->new  file로 view페이지 만들어 준다

![1531382243715](C:\Users\student\AppData\Local\Temp\1531382243715.png)



#### 삼항 연산자

if - else 로 길게 쓰던거를 (명아 조교님 노트 참고)

![1531382338129](C:\Users\student\AppData\Local\Temp\1531382338129.png)

이렇게 짧게 가능

`: `  앞에 것이 맞아면 : 좌측 내용 보여주고   아니면 : 우측 보여줌



양민<->관리자 코드를 넣는다

![1531373518456](C:\Users\student\AppData\Local\Temp\1531373518456.png)

```ruby
class AdminController < ApplicationController
    def users
        @users = User.all
    end
    
    def change
       # 해당하는 유저의 역할을 바꾼다.
       # 1. 만약에 관리자면 -> 양민
       # 2. 아니면 -> 관리자
       user = User.find(params[:id])
       if user.is_admin?
           user.update(
               is_admin?: false
           )
       else
           user.update(
               is_admin?: true
           )
       end
       redirect_to '/admin/users'
    end
end
```







![1531372983044](C:\Users\student\AppData\Local\Temp\1531372983044.png)

```html
<h1>회원정보</h1>

<!--회원정보(이메일, 관리자 여부)-->
<table>
    <tr>
    	<th>이메일</th>
    	<th>역할</th>
    	<th>로그인 횟수</th>
    	<th>로그인 시간</th>
    	<th>로그인 ip</th>
    </tr>
    <% @users.each do |user| %>
    <tr>
        <td><%= user.email %></td>
        <td><%= user.is_admin? ? "관리자" : "양민" %></td>
        <td><%= user.sign_in_count %></td>
        <td><%= user.last_sign_in_at %></td>
        <td><%= user.last_sign_in_ip %></td>
        <td><%= link_to "역할 바꾸기", "/admin/users/#{user.id}/change", data: {confirm: "레알?"} %></td>
    </tr>
    <% end %>
</table>
```

코드 입력

![1531373139189](C:\Users\student\AppData\Local\Temp\1531373139189.png)



근데 또 시간이 **utc 시간**으로 나옴. 세계 협정시 (표준시)

* cf.* 그리니치 천문대 시간 gmt



![1531373202900](C:\Users\student\AppData\Local\Temp\1531373202900.png)



![1531373236705](C:\Users\student\AppData\Local\Temp\1531373236705.png)

주석 풀고 내용 바꾸기

![1531373281158](C:\Users\student\AppData\Local\Temp\1531373281158.png)

rake -D time`인지 뭔지 콘솔 창에 쳐 보면 가능한 시간들 뭐 알 수 있댕..



- config 폴더 안에 내용 건드렸으면 무조건 서버 껐다 켜야 적용된닷!!!!





---

admin 컨트롤러에 check_admin 액션을 

![1531373565141](C:\Users\student\AppData\Local\Temp\1531373565141.png)

![1531373691286](C:\Users\student\AppData\Local\Temp\1531373691286.png)

일단 모든 액션 하기 전에 무조건 관리자인지 검사하도록(해당 액션부터 수행하도록) before_action을 넣어준다

![1531373730132](C:\Users\student\AppData\Local\Temp\1531373730132.png)

**==> `~~ /admin/users` 로는 관리자여야 들어갈 수 있당.**





---

![1531382988481](C:\Users\student\AppData\Local\Temp\1531382988481.png)

devise gem 깔았을 때 콘솔 창에 gem이 이런 거 알려준다

![1531383033369](C:\Users\student\AppData\Local\Temp\1531383033369.png)

이 때

flash 메시지를 보내주는 애. 메시지를 담아놓고 불러올 수 있는  :이거로 이름을 정해준다

![1531383157877](C:\Users\student\AppData\Local\Temp\1531383157877.png)

여기서 :alert 라고 정해준 이름을 

![1531383145108](C:\Users\student\AppData\Local\Temp\1531383145108.png)

여기서 %= 로 프린트 해 줘라

 

- layout 페이지에 넣어서 어디서나 실행되도록 한당





왜 집으로 가는 지 알려주자 (flash 메시지로)

![1531373845088](C:\Users\student\AppData\Local\Temp\1531373845088.png)

`flash[:alert] = "양민 꺼져!!"`



layout페이지에....

![1531373952243](C:\Users\student\AppData\Local\Temp\1531373952243.png)

![1531374122105](C:\Users\student\AppData\Local\Temp\1531374122105.png)





부트스트랩 적용하자

![1531374184069](C:\Users\student\AppData\Local\Temp\1531374184069.png)

부트스트랩 css / javascript (js)   코드 복붙







---

요새 디자인 그리드는 12column 그리드를 많이 쓴다.



ex.  아래와 같이 4개 요소가 있다 하면![1531375522845](C:\Users\student\AppData\Local\Temp\1531375522845.png)

한 요소당 3개씩 쓰는 것



![1531375602935](C:\Users\student\AppData\Local\Temp\1531375602935.png)

이렇게 3개 요소가 배열된다면 한 요소당 4개씩 쓰는 거고.  (12를 동일하게 배분)



![1531375618697](C:\Users\student\AppData\Local\Temp\1531375618697.png)

이렇게 비대칭으로 8:4 로 구성할 수도.이쁘장하게 ㅎㅎ





- 12가 약수가 제일 많은 수라서 12가 채택되엇습니다. (자유도가 높아서.. 2개도 3개도 4개도 나누어 떨어지니까)
  - rails도 12그리드를 채택하고 있습니당



git bash를 연다

project 폴더로 들어가요 `cd project`



`ls`모든 파일 보기



`code grid.html`

grid파일을 만들어요







![1531375872535](C:\Users\student\AppData\Local\Temp\1531375872535.png)

grid파일 만든 거 열어봐요



### **부트스트랩 요소는 항상 class로 가져와요**



![1531375940561](C:\Users\student\AppData\Local\Temp\1531375940561.png)

![1531376015608](C:\Users\student\AppData\Local\Temp\1531376015608.png)

페이지 검사



div 클래스 이름을 말해주자

![1531376165649](C:\Users\student\AppData\Local\Temp\1531376165649.png)

![1531376180415](C:\Users\student\AppData\Local\Temp\1531376180415.png)

자기가 알아서 배분이 된다.  (class를 row로 설정해 줬기 때문에 그 row로 )



]

(원래 css로 포지셔닝 해서 가려고 내가 양분하려고 하면 굉장히 어렵당...)

get bootstrap페이지에 Documentation에 Layout에 Grid 파트에 있다

![1531376273558](C:\Users\student\AppData\Local\Temp\1531376273558.png)









#### 우리 전시회 페이지로 쓸 것은 이것이다 ㅎㅎ (레이아웃이 좋은 듯)

![1531376314637](C:\Users\student\AppData\Local\Temp\1531376314637.png)

반응형 웹페이지로 만들어져 있기 때문에 

줄어들때도 레이아웃이 잘 유지된다.

==> 태블릿이나 핸드폰 사이즈에서도 잘 나오도록 되어 있음

![1531376421312](C:\Users\student\AppData\Local\Temp\1531376421312.png)

각 태블릿pc  모바일폰 등 크기 px 참고



![1531376555039](C:\Users\student\AppData\Local\Temp\1531376555039.png)

![1531376506416](C:\Users\student\AppData\Local\Temp\1531376506416.png)

줄여봐바 창을 .  이렇게 잘 나온당



![1531376592165](C:\Users\student\AppData\Local\Temp\1531376592165.png)

이 크기일 땐 어떻게 배치 하겠다는 뜻



![1531376645471](C:\Users\student\AppData\Local\Temp\1531376645471.png)



![1531376692918](C:\Users\student\AppData\Local\Temp\1531376692918.png)

![1531376754858](C:\Users\student\AppData\Local\Temp\1531376754858.png)

줄였을 때 반응하는 모습

![1531376768612](C:\Users\student\AppData\Local\Temp\1531376768612.png)

더 줄였을 때









(숫자를 아무것도 쓰지 않으면 자동분배를 한다 (col만 썼을 때 자동으로 3분할 한 것처럼))

![1531376723484](C:\Users\student\AppData\Local\Temp\1531376723484.png)

이 뜻은  컬럼 자체를 2개를 쓰겠다는 뜻 ( 6개씩 2개로 )

![1531376810608](C:\Users\student\AppData\Local\Temp\1531376810608.png)

이런식으로 반만 쓰게 된다





그럼 3등분한 맨 오른쪽에만 배치하고 싶으면

![1531376868559](C:\Users\student\AppData\Local\Temp\1531376868559.png)

![1531376886712](C:\Users\student\AppData\Local\Temp\1531376886712.png)

이런식으로 앞 2개 내용은 비우고 가장 마지막에만 내용 채우면 그쪽에 배치한 것이 된 것.



sm small의 약자 ==> 반응형 되도록 하는

![1531376937765](C:\Users\student\AppData\Local\Temp\1531376937765.png)

이렇게 바꿔보자

![1531376951059](C:\Users\student\AppData\Local\Temp\1531376951059.png)

클 때는 똑같은데

![1531377042967](C:\Users\student\AppData\Local\Temp\1531377042967.png)

이 정도가 되면 하나의 cloumn으로 수렴한다



- column-4라고 하면 아주 작은 창 크기일 때도 이것을 유지하겠다
- sm-4라고 하면 작게 하지 않으면 4개 컬럼을 쓰겠다. 작으면 그냥 창 하나를 다 쓰겠다

![1531377082128](C:\Users\student\AppData\Local\Temp\1531377082128.png)

더 큰 태블릿에서 작동하게 하려면 md 넣고.   (좀만 줄여도 바로 하나의 column쓰는 레이아웃으로 바뀌는.)



![1531377166453](C:\Users\student\AppData\Local\Temp\1531377166453.png)

3개씩 쓰는 4개 column을 만들겠다

![1531377199657](C:\Users\student\AppData\Local\Temp\1531377199657.png)



작아졌을 때 하나가 아니라 그래도 4개 유지는 너무 많으니 2개 컬럼을 쓰겠다고 하고플때

![1531377313785](C:\Users\student\AppData\Local\Temp\1531377313785.png)

![1531377413856](C:\Users\student\AppData\Local\Temp\1531377413856.png)



- small이 모바일 사이즈
- Medium 이 태블릿 사이즈
  	- 태블릿까지 맞춰서 잘 보이게 하고 싶다 하면 md쓰는 거고







앨범 example에서.

우클릭, 페이지 소스보기

`<body>` ~ `</footer>` 까지 복사  (위 클릭하고 shift키 누르고 밑에 footer에서 클릭하면 전체 블록 가능!)

![1531377499955](C:\Users\student\AppData\Local\Temp\1531377499955.png)

![1531377565550](C:\Users\student\AppData\Local\Temp\1531377565550.png)

![1531377573062](C:\Users\student\AppData\Local\Temp\1531377573062.png)

body에 붙여넣는다  

(붙여넣을 때 tip!!  딱 붙여넣은 순간에 tab정리가 잘 안되어 있다. 

​	==>  붙여넣고 바로 그 다음 `ctrl + z`를 눌러주면 정렬이 된당)





근데 이 상태로 페이지 띄워 보면 살짝 원래 album template 예시와 쬐금 다름,.

![1531377692379](C:\Users\student\AppData\Local\Temp\1531377692379.png)





custom setting 링크가 따로 있기 때문!!

==> 아래 클릭!

![1531377654608](C:\Users\student\AppData\Local\Temp\1531377654608.png)

![1531377719089](C:\Users\student\AppData\Local\Temp\1531377719089.png)

이 링크가 따로 지정되어 있다. 우리도 넣어줘야 한다 저 추가 코드들을!! 

==> url 복사



![1531377748196](C:\Users\student\AppData\Local\Temp\1531377748196.png)

이렇게 넣는다

![1531377798703](C:\Users\student\AppData\Local\Temp\1531377798703.png)

됐당~



---

*cf.*  즉,  부트스트랩 그냥 제공 템플릿을 봐도 **디자인 그리드 합은 다 12이당**

---



.

이제, 

이제까지  vscode로 해본 것을 **c9 exhibition 프로젝트에** 적용시켜 보자

1. 우선 `<header>` ~ `</header>`  부분을 복사해서 

![1531383434276](C:\Users\student\AppData\Local\Temp\1531383434276.png)



layouts 폴더에 `_header.html.erb`파일을 만들어서 거기에 붙여넣기

![1531383505863](C:\Users\student\AppData\Local\Temp\1531383505863.png)

![1531383614176](C:\Users\student\AppData\Local\Temp\1531383614176.png)

레이아웃 마스터 파일에다가 header _header로 따로 빼 놓은 거 렌더.





2. 그리고 이번엔 `<main>` ~ `</main>` 복사

![1531383706345](C:\Users\student\AppData\Local\Temp\1531383706345.png)

![1531383743136](C:\Users\student\AppData\Local\Temp\1531383743136.png)



복사한 거 works index페이지에 붙여넣기

![1531383576102](C:\Users\student\AppData\Local\Temp\1531383576102.png)



3. 이제 우리 페이지에 맞게 내용 바꾸고 넣고 각각 맞게 바꾼당!!!

---



---

#### flash메시지 디자인 부트스트랩 적용~

- get bootstrap에 Components -> **Alerts** 

---



---

#### **각 link에 class 지정해서 스타일 넣기**

![1531383356280](C:\Users\student\AppData\Local\Temp\1531383356280.png)

---



---

#### 메인 로고 누르면 어느 페이지에서나 홈으로 가도록 하기 (layout  _header파일에서)

![1531383341085](C:\Users\student\AppData\Local\Temp\1531383341085.png)

---





---

그리고 내가 자주 에러내는... 나쁜 습관!!   (if - end도 if 소문자인데 왜 자꾸 unless는 대문자로 쓰니 ㅠㅠ)

# unless - end 할 때 unless 소문자로 !!!! 주의!!!!!

# Unless (X)

---

