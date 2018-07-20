### html + CSS(스타일시트이용, 디자인)

##### 1. html + css 통해 이쁘장한 나의 홈페이지 만들기

##### 2. 단순히 똑같은 웹페이지를 보여주는 사이트가 아닌 다양한 요청에 부응하는 동적인 사이트 만들기

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

* 대부분의 웹페이지들은 비슷하게 생겼다. 

  ex. 네비게이션 바

* 웹서비스 :   클라이언트 <-> 서버

  

#### 웹페이지 종류

1. static page 

ex. **스포카.** 백화점 포인트 쌓아주는 사업. 굉장히 잘하고 있는 애들 중 하나인데

​	=> ico페이지 따로 있음.  initial coin offring 내 코인 발행. 토큰을 만들어서 팜. 홍보하는 페이지.

* 누가 접속해도 똑같은 페이지가 보여짐. 기능이 없다. 정적인 웹사이트. 누구든 아메리카노 서비스만 하는 페이지

2. dynamic website 페북, 트위터

​    :  개인별로 다른 페이지들을 보여주는 사이트. 다양한 유저 요청에 따라



#### html 요소

1.  <div> : 디바이드. 섹션을 나눌 때 쓰는 태그 =>  **구역화, 구조화 할 때**

   * p태그보다 훨씬 많이 쓸 것. 

   1) <p>보다 일반적인 개념으로 콘텐츠를 넣을 수 있는 요소

   2) 한 division은 보통 그 안의 내용을 들여쓰기 해서 섹션을 한눈에 구분할 수 있게 코드를 짠다.

   - 웹페이지상 결과물은 똑같다. 개발자가 보기 편하기 위해 쓰는 것

   3) 각각의 division마다 각기 다른 스타일링이 가능 =>  css와 함께

2. <table>  :  표를 넣을 수 있다

   1) customizing이 힘들어서 잘 안쓰는 추세

   2) 게시판 쓰는 곳에 거의 table 쓴다고 보면된다

3. 선택자. 



#### CSS 스타일을 입히는 방법 3가지

##### 1) 태그tag 단위로. 태그의 속성 지정 => 실제로 태그 단위로 넣어 쓰지는 않음

- ex. <p style="color: red">   :    <p>태그에 스타일을 넣은 예시

- 각각 지정해 줘야 해서 불편함. 보기 힘들고 코드가 복잡해짐.

  

##### 2) CSS <style> </style> 태그 따로 이용해서

- head 안에 넣어줌. 

- ex.   <style>
              p {
                  color: pink; font-style : italic; font-size:15px ; font-weight : bold
              }
          </style>

  => 모든 p에 다 먹고 각각 커스텀이 안되는 불편함.

- 위 코드 p부분에 *을 쓰면 모오든 글씨에 먹음. 모든 글씨를 다 똑같은 스타일로 하진 않기 때문에 거의 쓰진 않음.

- **id (단일 태그에 각각 naming시 이용) / class (여러 태그 클래스 이름 하나로 그룹핑) 이용하기**

  => body에서 해당 태그에 id / class = " " 이름 지정해 준 후 아래 스타일 코드는 head에 넣는다

  ```css
  <style>
  	#welcome {			  (#붙이는 게 id)
      		color: PALEVIOLETRED; font-style : italic; font-size:15px ; font-weight : bold
  	}
      .search{color : CADETBLUE ; font-weight :bold}    	 (.을 붙이는 게 class)
  </style>
  ```

  (id/class이름 항상 " " 안에 스트링으로 해야함 유의)

  - class로 같은 속성 가진 애들을 묶어주도록 하라

    => **DRY 코딩 ;  do not repeat yourself  항상 간편하게, 반복되는 것을 없애야한다**

- body에 보더 주려면 body 안 내용을 하나의 div로 감싸서 <div id=" "> 해서 

  위 헤드에 id속성을 넣어준다.

  

##### 3) css 파일을 따로 만들어서 

- 새폴더 - > style.css 이름으로 저장 -> 옆에 새폴더 'public'만들고 그 안에 style.css넣을 것 -> 

  -> html파일 헤드에  <link rel = "stylesheet" type="text/css" href ="style.css"> 넣는다 -> 

  

- default 서버가 public을 먼저 어쩌구 한대.. public이란 폴더 안에 넣어야 됨..
  - 경로폴더 : 아무것도 명시 x경우 현재 폴더

  - 외부에 있는 파일을 가져와서 스타일링 할 수도. 

    ex. 부트스트랩 (bootstrap)



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

- sinatra => 경량형 웹 프레임워크   : 루비 엄청 간단함. 

  - express(javascript 기반)도 sinatra보고 만듦. 

  - flask도 sinatra 보고 만들었다 (파이썬 기반=> sinatra의 파이썬 버전)

- html colors name : https://htmlcolorcodes.com/color-names/



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

*css  <link rel = "stylesheet" type="text/css" href ="style.css"> 링크에서

시나트라라는 앱이 public이 home directory로 설정 되어 있음.

href 에서 아무것도 안쓰면 home directory안에 있는 거임.

- sinatra erb ?  => erb : 임베디드 루비



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

### opgg 프로젝트 새로 시작

- http://www.op.gg/summoner/userName=heart :  롤 전적 아이디별로 다 보여주는 사이트
- 강사님 아이디 :  지수야쏘리

*우리 opgg_clone 프로젝트

:  이거 할 줄 알면 크롤링해서 검색하는 사이트는 웬만한 거 다 만들 수 있다

cf. 메이커스페이스도 뭐 op.gg있대..???



1. 새 프로젝트 만들고

2. 콘솔에 `gem install sinatra`입력해서 sinatra깔고

3. `gem install httparty`

4. `gem install nokogiri`

5. 위 창에 app.rb 새파일 만들어주고

   위 3개 다  불러줌

   `require 'sinatra'`

   `require 'httparty'`

   `require 'nokogiri'`

6. 스크랩할 사이트 접속

   ex. http://www.op.gg/summoner/userName=heart   (방문자 월3억찍는대)

   내가 필요한 정보 위에 마우스커서 놓고 우클릭 -> 검사 -> 해당하이라이트된 코드에서 우클릭 -> copy -> copy selector

7. 다시 프로젝트창에서 app.rb에서

   get '/' do

       @res = HTTParty.get("http://www.op.gg/summoner/userName=heart")
       @win = Nokogiri::HTML(@res).css('#SummonerLayoutContent > div.tabItem.Content.SummonerLayoutContent.summonerLayout-summary > div.SideContent > div.TierBox.Box > div.SummonerRatingMedium > div.TierRankInfo > div.TierInfo > span.WinLose > span.wins')
       @lose = Nokogiri::HTML(@res).css('#SummonerLayoutContent > div.tabItem.Content.SummonerLayoutContent.summonerLayout-summary > div.SideContent > div.TierBox.Box > div.SummonerRatingMedium > div.TierRankInfo > div.TierInfo > span.WinLose > span.losses')
       erb :index
   end

   : 이런식으로 `변수 = Nokogiri::HTML(@res(받아온페이지 변수)).css('카피한 셀렉터 주소')`

8. index.erb (=루트파일)파일에서 아래와 같이 html 코드를 짜준다. 루비코드를 임베디드 해서

   <!DOCTYPE html>
   <html>
       <head>
           <title>롤 전적 검색</title>
           <meta charset="utf-8">
       </head>
       <body>
           <h1>롤 전적 검색</h1>
           <p><%=@win%></p>
           <p><%=@lose%></p>
       </body>
   </html>



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

cf. 남친추적기 만들기

=> 인스타에 팔로워 늘었을 때 이상한페이지 팔로잉하는가 감시

추가되는 사람이 카톡으로 보내지도록



ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

- ctrl + /  :  c9에서 주석다는 단축키

ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ

### 깃헙 모내기

* repository 하나는 폴더 하나의 개념

https://github.com/kitty4089

https://github.com/kitty4089/3d_study   :   써야하는 코드들 나와있음

```
echo "# 3d_study" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/kitty4089/3d_study.git
git push -u origin master
```

###### *사전작업 :   1) git bash 깔았던 거 띄워     2) 올릴 파일이 든 폴더 위치 확인

1. 올릴 (마크다운)파일이 든 위치로 이동 **(ex. 나는 project폴더 하위에 study폴더를 만들었다)**

   :  cd project -> cd study -> cd       (cf. dir치면 현재위치에 있는 파일 목록들 볼 수 있다.)

   . git bash 콘솔에 git init을 친다     	

   => init : initialize/  깃아~ 내가 현재 있는 폴더에서 관리를 시작할게.

   -> 치면  "initialized empty Git repository in C:// 어쩌구~~ /.git/" 문구가 나옴

   => git폴더가 숨김폴더로 만들어진다. (하고 나면 숨김폴더로 git폴더가 생김. 해당 위치에)

   - git숨김폴더가 잘 만들어졌나 확인 => 숨김파일 보이게 하기

     => study 폴더로 가서  -> alt키 -> 도구 탭메뉴 -> 폴더옵션 -> 보기 탭 -> '숨김 파일, 폴더 및 드라이브 표시' 체크 -> 확인 -> 폴더 새로고침

   => 폴더 안에 숨김폴더 확인은 그냥 dir로 안보여진다. 아래 2가지 중 하나를 택해 해본다.

   ​	1) ll       => 엘엘

   ​	2) ls -al   =>엘에스 대시 에이엘            :  들어있는 파일들 목록 보기

   

2. git status    => 깃아 지금 내 상태가 어떻니 :  처음에는 아직 commit할 파일이 아무것도 없고. 추적할 파일이 2개가 있어요 (그 폴)

   => 빨간색으로 파일 목록들 뜰 것이야. 저장이 안돼있어서 그런거 => git add를 해준다

3. git add .       (=> 한 칸 띄고 .찍어)

   쳤을 때 아무일도 안일어나면 잘된 것  => 이게 git 숨김폴더 생겼던 거에 저장을 한 것. => 이제 잘 저장됐는지 봐야겠죠

4. 그 다음 다시 git status치면 이젠 있던 파일들이 초록색으로 바뀜 => 잘 저장됐네

   이제까지 숨김폴더 내 컴 폴더 (로컬)에 저장된 거고. 이제 온라인에 올려야겠지.

5. git commit -m "first commit"        => " "안에는 원하는 이름.   (애네는 save를 commit으로 씀 ==)

6. git config  --global user.email  "내 이메일 주소"      => configuration : 내 이메일과 이름을 써줘야 함

   또 enter치고 아무말 안나오면 잘된 것.

7. git config --global user.name "내 아이디"

8. 다시 `git commit -m "내가 저장하려는 제목이름"`

   enter누르면 또 아무것도 안나오면 잘 저장이 됐음

   => 첫번째 save 포인트를 지정한 것

9. git log 치면 내가 저장한 시간 등과 함께 first commit이란 문구가 나옴 => 히스토리 확인

10. 원격저장소(=깃헙)에 저장

```
git remote add origin https://github.com/kitty4089/3d_study.git
```

: git 아, 원격저장소(=깃헙)에 저장할 건데 그 주소는 이거야.

enter누르면 또 아무것도 안나오면 잘 된 것

11. 이제 push 우리 저장한 걸 밀어넣어줄 거

    ```
    git push -u origin master
    ```

12. git add .

13. git commit -m "first commit"

14. git push -u origin master

15. 로그인하라고 함

    kitty4089 / 특문 두개 + 끝에 숫자 하나도

**모내기 끝**

16. (선택) git log  => 한 번 더 눌러서 저장 잘 됐는지 확인

![1528450755343](C:\Users\student\AppData\Local\Temp\1528450755343.png)

![1528450785498](C:\Users\student\AppData\Local\Temp\1528450785498.png)