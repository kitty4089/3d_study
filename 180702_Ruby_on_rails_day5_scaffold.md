# Scaffolding

*(퍼펙트 루비온레일즈 **책 74쪽~**)



c9 프로젝트를 만들어준 후, (프로젝트 이름 :   '**scaffold**'  - 7월 2일 생성)

bash창에..

`rails g scaffold`

1. `rails g scaffold Post title content`  라고 치자

   cf. `rails g model Post title content`   (원래 모델 만들었듯이 한 것이다)

2. `rake db:migrate`를 또 치자

   cf.  migrate, db/post.rb   

3. 여기까지 해준 상태에서 서버를 켜서 창을 열어본다

4. url끝에 /posts 를 붙여본다

   - 오옷 이제까지 손으로 다 노가다했던 게시판 기능들이 다 구현돼 있다!!!

---



- https://scaffold-kitty4089.c9users.io/rails/info/routes

  scaffold가 routes 컨트롤 어떻게 하는지 보기

  ![1530495662105](C:\Users\student\AppData\Local\Temp\1530495662105.png)

- 실제 routes.rb파일 상태

  ![1530495692891](C:\Users\student\AppData\Local\Temp\1530495692891.png)

  한 줄뿐. 이 한 줄이 실제로는 route컨트롤 액션 8개 정의해주는 중..



- 인덱스 페이지를 루트페이지로 하쟝

  ![1530495756755](C:\Users\student\AppData\Local\Temp\1530495756755.png)

  컨트롤러에서 액션 확인

![1530495825829](C:\Users\student\AppData\Local\Temp\1530495825829.png)

코드 추가 (루트 페이지에)



![1530495864912](C:\Users\student\AppData\Local\Temp\1530495864912.png)

추가된 것 확인.





---

### 컨트롤러 코드에서 각 액션들에서 중복됐던.. 

#### 해당 id 글 찾아 보여주는 find코드 처리

`@post = Post.find(params[:id])`





![1530496060429](C:\Users\student\AppData\Local\Temp\1530496060429.png)

액션들 수행하기 전에 무조건 set_post 함수를 실행하라. only (show/edit/등의 액션에만)



![1530496105864](C:\Users\student\AppData\Local\Temp\1530496105864.png)

set_post 함수는 하단에 정의되어 있음



---







### 전에 했던 board_change 2 프로젝트를 scaffold로 바꿔보자

![1530497254117](C:\Users\student\AppData\Local\Temp\1530497254117.png)



해당 프로젝트에 들어가서 컨트롤러 밑에 액션 추가  (함수 만들어준다)

![1530497396780](C:\Users\student\AppData\Local\Temp\1530497396780.png)

```ruby
def set_post
    @post=Post.find(params[:id])
    #return @post     #루비는 똑똑해서 이런 return없으면 제일 마지막 있었던 애를 리턴해주므로
    #자동으로 @post가 리턴된다
end
```



show / edit / post  에 해당하는 코드를 내가 만든 함수로 대체.

![1530497418139](C:\Users\student\AppData\Local\Temp\1530497418139.png)





`before_action(:set_post)    `

- 함수를 : 심벌로 표현해주기만 하면. 모든 액션이 일어나기 전에 해당 함수 실행하도록 하는 코드가 된다.

![1530497541412](C:\Users\student\AppData\Local\Temp\1530497541412.png)



정말 그런지 테스트 해보자  >> hello를 출력해주는 함수 정의 ( 콘솔 창에 찍힘 )

![1530497814861](C:\Users\student\AppData\Local\Temp\1530497814861.png)

![1530497827905](C:\Users\student\AppData\Local\Temp\1530497827905.png)



서버 켜서 웹페이지들 동작시킬 때마다

콘솔창에 hello가 찍힘을 확인할 수 있다

![1530497875086](C:\Users\student\AppData\Local\Temp\1530497875086.png)





그럼 이제 진짜 set_post함수가 실행되도록 해보자

![1530497901805](C:\Users\student\AppData\Local\Temp\1530497901805.png)



웹페이지 실행해보자

![1530497951977](C:\Users\student\AppData\Local\Temp\1530497951977.png)

- 아닛!!! 에러가 떴당!

  ==> params로 넘어온 url id 가 없당 ㅇㄷ

  

==> 모든 액션에 대해서가 아니라 

params 로 넘어오는 id가 없는 페이지 액션에서는 함수 실행 안되도록 해야한다.

==> `,except: [:index, :new, :create]` 추가

![1530498138400](C:\Users\student\AppData\Local\Temp\1530498138400.png)



==> 이제 에러가 나지 않는당. 

---





## 어떤 유저가 어떤 글을 썼는지 model (db table) 간 연결하기

#### User   모델 (회원들)    /    Post  모델 (게시판 글) 

> 두 모델을 1대 다로 연결해야 한당
>
> 즉, 어떤 글을 - 어떤 회원(유저)가 썼는지 표시



#### 일단 사용자가 로그인하고 나서야 모든 것을 볼 수 있게 만들자



- before_action(사용자가 로그인 되어있는지 체크하라)   를 구현해야 한다 

  (페이지 요청이 왔을 때 set_post함수 실행 전에 

  사용자가 로그인이 되어있는지부터 체크하는 메쏘드(액션)가 있어야 함)

- 모든 포스트 관련 페이지 액션 하기 전에 체크하게 할 것이다

![1530498721874](C:\Users\student\AppData\Local\Temp\1530498721874.png)

```ruby
def check_login
    #사용자가 로그인을 안했으면 -> /users/login으로 보내기
    #로그인이 안돼있으면 session이 비어있다
  	if session[:id].nil?  #비어있니? 하고 물어본당
    	redirect_to '/users/login'
	end
end     
```



![1530498765047](C:\Users\student\AppData\Local\Temp\1530498765047.png)



**...근데 하하 내가 이 프로젝트에 회원가입/로그인 기능을 안 만들었었넹;...;;**  

기능을 만들고 테스트 하도록. 지금은 실제로 실행시키면 페이지 없다고 에러 뜬당.



그러니... 여기부터는 강사님이 하는 거 메모

![1530498936523](C:\Users\student\AppData\Local\Temp\1530498936523.png)

로그인 안한 상태라도 홈페이지 들어와서 인덱스(홈페이지) 까지는 보여주고 (게시글 목록은 보이고)

게시글 클릭해서 보려고 하면 (로그인 안한 상태라면)로그인하라고 하도록 하는 부분이당..



- 작성자 같이 보여주기

Post 게시판 db table (모델) column에 **'writer' column 추가**해야.

db구조 설계는 db -> migrate 폴더 안에 해당 모델에 관련된 파일에 들어있당!



(먼저 서버를 꺼주고)

-> `t.string :writer`  를 다른 column 항목들과 똑같은 포맷으로 써준당

![1530499420410](C:\Users\student\AppData\Local\Temp\1530499420410.png)

![1530499554308](C:\Users\student\AppData\Local\Temp\1530499554308.png)



-> `rake db:drop` 으로 기존 db 설계도 날린다

-> `rake db:migrate` 로 다시 수정된 설계도를 올려준당

![1530499607050](C:\Users\student\AppData\Local\Temp\1530499607050.png)



writer 항목이 db에 추가되도록 수정.

![1530499637157](C:\Users\student\AppData\Local\Temp\1530499637157.png)



보여질 표에 '작성자' column 추가

![1530500043278](C:\Users\student\AppData\Local\Temp\1530500043278.png)

![1530500060482](C:\Users\student\AppData\Local\Temp\1530500060482.png)





---

## 데이터베이스 관계 연관

*(퍼펙트 루비온 레일즈 **책 294쪽**)



많은 것이 적은것에 포함된다고 표현하는 것이 대부분.

ex. '학생들'이 각 '학급'에 속하는 것이 더 간편. 

​	==> 학생들에게 학급을 나타내는 (또는 학년) 명찰을 다 달아놓으면 바로바로 알 수 있다

**많은 쪽이 자기가 속한 쪽의 정보를 반드시 품고 있다.**



- primary key
- foreign key



db를 바꿔준다

![1530505444539](C:\Users\student\AppData\Local\Temp\1530505444539.png)



바꿨으니

`rake db:drop`

`rake db:migrate`



컨트롤러에도 user id로 바꿔준다

![1530505544958](C:\Users\student\AppData\Local\Temp\1530505544958.png)



![1530505581888](C:\Users\student\AppData\Local\Temp\1530505581888.png)





**<가장 핵심! 부분>**

**모델**파일을 건드려야 한당!!!!!   <u>두 db 테이블을 연결 시켜준다!!!!</u>

![1530505973006](C:\Users\student\AppData\Local\Temp\1530505973006.png)

![1530505947460](C:\Users\student\AppData\Local\Temp\1530505947460.png)



#### **==> 게시글이 많고 그에 대응하는 user는 하나다. 어떤 user가 쓴 모든 글을 볼 수 있다.**





show페이지 작성자를 바꿔준다

![1530506133165](C:\Users\student\AppData\Local\Temp\1530506133165.png)



근데 이대로 하면 아래와 같이 나올 것이다

![1530506170797](C:\Users\student\AppData\Local\Temp\1530506170797.png)



==> 다시 아래와 같이 수정해준다

![1530506207954](C:\Users\student\AppData\Local\Temp\1530506207954.png)





---

### 댓글기능

:  하나의 글은 여러개의 댓글을 가진다

글과 댓글  ==> 1대 N의 관계



show페이지에 댓글 다는 곳을 만들어 준다

![1530508325005](C:\Users\student\AppData\Local\Temp\1530508325005.png)



날릴 곳을 form action으로 정의 해준다

![1530508373387](C:\Users\student\AppData\Local\Temp\1530508373387.png)



라우트 정의

![1530508410072](C:\Users\student\AppData\Local\Temp\1530508410072.png)



컨트롤러에 액션 정의



![1530508499943](C:\Users\student\AppData\Local\Temp\1530508499943.png)

private ;  외부에서 접근 못하게 하는 코드 

url정의해서 가는 걸 못함. 안전하게 앱을 만들 때.



반드시 private위에!! 해야 한다고?? >> 뭔소리징..



![1530508622294](C:\Users\student\AppData\Local\Temp\1530508622294.png)

위에 write_reply도 추가 시킨당



view페이지는 만들지 않고 redirect시킬거당



#### reply 테이블을 만들쟝 (db / model)

`rails g model Reply`   : **모델명은 대문자로 쓰는 것이 관례!!!**

댓글은 반드시 어떤 글에 속해 있어야 한다.

post와 1대 n의 관계

==> post와 reply를 관계맺게 하자.

- 댓글이 데이터가 많은 쪽이다.
- 댓글이 자기가 속한 포스트의 정보를 갖고 있어야 한다.
- reply가 속한 포스트에 포스트 아이디(몇 번 글에 속하는 건지)를 가져올 것이다



![1530509147474](C:\Users\student\AppData\Local\Temp\1530509147474.png)

cf. **루비환경에서 exit 하고 내 아이디 workspace 어쩌구 나온 상태에서 코드 입력해야함을 유의!!!!!!!**



![1530509264311](C:\Users\student\AppData\Local\Temp\1530509264311.png)

포스트 테이블에 데이터 넣도록 코드 입력 (.create)



라우트에 id를 포함하도록 추가해준다.

![1530509314872](C:\Users\student\AppData\Local\Temp\1530509314872.png)



근데 끝에 안쓰고 보통 개발자들 사이에서  해당 id글에 댓글을 쓰겠다는 의미로 (ex. 100번글에 달린 댓글)

가운데 아이디를 넣는다

![1530509376729](C:\Users\student\AppData\Local\Temp\1530509376729.png)



근데 또 이제는 앞뒤가 이름이 다르니까 해쉬 명시적으로 써 줘야 한당

![1530509445037](C:\Users\student\AppData\Local\Temp\1530509445037.png)



url 액션도 바꿔준다

![1530509537353](C:\Users\student\AppData\Local\Temp\1530509537353.png)



컨트롤러에서

1) id받도록 수정

2) 이전 페이지로 redirect

![1530509617097](C:\Users\student\AppData\Local\Temp\1530509617097.png)



확인해보자

![1530509725046](C:\Users\student\AppData\Local\Temp\1530509725046.png)



`rails c`

`Reply.all`

![1530510129764](C:\Users\student\AppData\Local\Temp\1530510129764.png)

name지정이 안돼있어서 db에 내용이 들어가지 않았다.

(name지정이 돼있어야 컨트롤러 .create에서 params로 reply내용을 Reply 테이블의 content column에 넣을 수 있겠지)







잘 db에 들어가는 것이 확인이 되었으니 

이젠 보여주기 위해 db 두 개를 연결하자 **(많은 쪽이 적은쪽의 정보를 가지고 있다)**

![1530509983020](C:\Users\student\AppData\Local\Temp\1530509983020.png)

![1530509940365](C:\Users\student\AppData\Local\Temp\1530509940365.png)





출력해주자 이제

show페이지에. (`.reverse`로  최신 댓글이 위로 올라오도록)

![1530512479081](C:\Users\student\AppData\Local\Temp\1530512479081.png)



댓글의 주인이 나오도록 수정해주자 (댓글 쓴 사람의 아이디)

![1530512568616](C:\Users\student\AppData\Local\Temp\1530512568616.png)



db를 건드렸으니 다시 db를 날리자

`rake db:drop`

`rake db:migrate`





계속 회원가입 다시 하고 로그인 하고 귀찮으니 시드를 생성해준다

![1530512676884](C:\Users\student\AppData\Local\Temp\1530512676884.png)

![1530512913523](C:\Users\student\AppData\Local\Temp\1530512913523.png)

배열 안에 해시를 넣어 주었다

*모두 스트링으로 해야함 유의!!!! " " 안에 감싸줄 것!!!



데이터를 다 써주고 나서 콘솔창에 (명령어창에)

`rake db:seed`

-> enter치고 별 말 없으면 잘 된 것

-> db건드렸으니 또 서버 껐다 켜줘요



컨트롤러에서 db에 넣도록 정의

![1530513199347](C:\Users\student\AppData\Local\Temp\1530513199347.png)





두 db연결 (레일즈에게 두 db가 연관되어 있다고 알려줘야 한다)

댓글과 유저를 연결해야 한다.

한 유저는 여러 개의 댓글을 가지고 있다



==> reply.rb 에서, **댓글은 어떤 유저에게 속해있다**

![1530513258296](C:\Users\student\AppData\Local\Temp\1530513258296.png)

==> **유저는 많은 댓글을 가지고 있다**

![1530513307951](C:\Users\student\AppData\Local\Temp\1530513307951.png)



show페이지에서 보이게 하자

![1530513563148](C:\Users\student\AppData\Local\Temp\1530513563148.png)

이러면 번호만 보인다



두 db를 연결했으므로

![1530513594608](C:\Users\student\AppData\Local\Temp\1530513594608.png)

![1530513609671](C:\Users\student\AppData\Local\Temp\1530513609671.png)

이 상태에서는 이런 코드만 보인당



![1530513645141](C:\Users\student\AppData\Local\Temp\1530513645141.png)

이렇게 바꿔주면 유저 이름이 잘 보인당





---

### 마이페이지 만들기

루트 정의

![1530506375932](C:\Users\student\AppData\Local\Temp\1530506375932.png)



컨트롤러에서 액션정의  (users 컨트롤러)

![1530506671065](C:\Users\student\AppData\Local\Temp\1530506671065.png)



==> 콘솔에서 바로 확인해보자

`rails console`

-> `User.find(1).posts`

![1530506754751](C:\Users\student\AppData\Local\Temp\1530506754751.png)

나오는 거 보니 배열 맞다. ( [ ] 대괄호로 나오는 거 보니.)



마이페이지 view파일을 적어준다

![1530507137716](C:\Users\student\AppData\Local\Temp\1530507137716.png)









---

### 지금 로그인된 유저가 쓴 모든 글들/댓글들 보여주기

https://board-change2-kitty4089.c9users.io/users/mypage

현재 모든 글들은 보이게 구현되어 있다. 



**이제 모든 '댓글들'도 보이게 하자.**

![1530513755268](C:\Users\student\AppData\Local\Temp\1530513755268.png)



마이페이지 view페이지로 갑니당 ㅎㅎ

![1530513838062](C:\Users\student\AppData\Local\Temp\1530513838062.png)



코드를 복붙해 줍니당 ㅎㅎ

![1530513980024](C:\Users\student\AppData\Local\Temp\1530513980024.png)

users 컨트롤러에 가줍니다  

==> 해당 유저가 쓴 모든 댓글들의 배열을 만든 후(`.find`) -> @replies 변수에 넣습니다

![1530515502773](C:\Users\student\AppData\Local\Temp\1530515502773.png)



다시 마이페이지에 갑니다

![1530515464218](C:\Users\student\AppData\Local\Temp\1530515464218.png)

해당 유저가 쓴 **댓글 개수**(<u>배열 @replies 의 크기를 알려주는 `.size `이용</u>) /

**댓글들** (<u>배열을 하나씩 돌면서 내용들을 print해줍니다</u>) 을 써줍니다



*cf. seed에 넣은 데이터는 기존에 있는 아이디랑 패스워드라도 상관 없이 그냥 내가 입력한대로 무조건 db에 들어가게 된닷!!!  (새로운 id넘버로)



아이디는 한 번만 보여주면 되므로 아래와같이 해보자

![1530516120305](C:\Users\student\AppData\Local\Temp\1530516120305.png)



로그인을 해준 후 웹페이지에 가서 확인한다

![1530516136934](C:\Users\student\AppData\Local\Temp\1530516136934.png)