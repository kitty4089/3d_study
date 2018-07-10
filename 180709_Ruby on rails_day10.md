18 .07 .09

***c9프로젝트;  'sunshine'**

(졸음 참사가 났던 저번시간에는.. devise/carrierwave gem 을 써서 scaffolding을 해보았다)





### model 만드는 것과 비슷한 scaffold

:  `rails g scaffold Post tilte content`

<=>  비슷! `rails g model 모델명 cloumn명 cloumn명`

- rake를 반드시 해 줘야 반영되는 것도 비슷!



![1531096044062](C:\Users\student\AppData\Local\Temp\1531096044062.png)

얘는 route에서 어떻게 한 줄로만 끝났을까?



model처럼 

`rake db:migrate` 해줘야 한당







**partial render** 

![1531096098698](C:\Users\student\AppData\Local\Temp\1531096098698.png)

(layout페이지의 yield처럼 써 있다)





cf.

![1531096523099](C:\Users\student\AppData\Local\Temp\1531096523099.png)

이 기본 홈페이지 루트페이지는 어디있냐면.... 아래 사진 참고.. Public에 있다

![1531096475133](C:\Users\student\AppData\Local\Temp\1531096475133.png)

![1531096494740](C:\Users\student\AppData\Local\Temp\1531096494740.png)

굳이 index.html 파일 내가 만들면 처음 나오는 디폴트 파일 바뀌긴 함.

full html이 아니라 한글은 안됨

![1531096600944](C:\Users\student\AppData\Local\Temp\1531096600944.png)

![1531096614506](C:\Users\student\AppData\Local\Temp\1531096614506.png)



그러나 이렇게 코딩 절대 안하므로 저 public안에 만들었던 html index파일은 삭제한당

---

얌전히 우리가 만든 페이지를 루트페이지로 routes.rb에 적어준당

![1531096653625](C:\Users\student\AppData\Local\Temp\1531096653625.png)





layout폴더 안에 `_nav.erb`파일 만들어 준다

![1531096723049](C:\Users\student\AppData\Local\Temp\1531096723049.png)

![1531096769281](C:\Users\student\AppData\Local\Temp\1531096769281.png)

그 파일 안에 부트스트랩 navbar 코드를 다 붙여 넣는다



**partial rendering** 불러올 때는 _를 쓰지 않고. 원본파일 이름에는 _를 쓴다

![1531096961824](C:\Users\student\AppData\Local\Temp\1531096961824.png)

- 기본으로 페이지는 app/view에 있는 애를 찾으므로 layouts 폴더에서 찾아줘라는 뜻으로 써줘야함



**Partial rendering**

![1531097039735](C:\Users\student\AppData\Local\Temp\1531097039735.png)





**루비온레일즈 교재 115p.**

링크 관련 뷰 헬퍼

![1531099178661](C:\Users\student\AppData\Local\Temp\1531099178661.png)

실제 페이지 '검사' 해보면

![1531099208956](C:\Users\student\AppData\Local\Temp\1531099208956.png)



/posts/new 페이지로 연결해 줘라 라는.. 링크 걸려 있다

`<a heref="/posts/new>New Post</a>`  와 같은 것!



==> 우리도 해보쟝!

![1531099297556](C:\Users\student\AppData\Local\Temp\1531099297556.png)

![1531099402000](C:\Users\student\AppData\Local\Temp\1531099402000.png)



링크가 생긴닷!!



![1531099435465](C:\Users\student\AppData\Local\Temp\1531099435465.png)

`rake routes`치면 모든 route에 정의된 페이지들을 볼 수 잇땅

ex. root 페이지(/)의 prefix는 root이다.



==> prefix에 정의된 이름_path 로 입력한다.

![1531099567189](C:\Users\student\AppData\Local\Temp\1531099567189.png)

이런식으로



결과 확인

![1531099589426](C:\Users\student\AppData\Local\Temp\1531099589426.png)

링크된 주소는 같은 '홈으로'링크 버튼을 만들었다







---

### 이제 더 scaffolding스럽게 만들어 보는 것을 해 보자



`rails g model Blog title content`

model 을 만들어보자



컨트롤러도 만들어 준다

`rails g controller blogs`

- 이제까지 게시판 있는 기능 페이지 만들었던 페이지들 목록 (7가지)

  index

  new

  create

  edit

  update

  destroy

  show



==>  `rails g controller blogs index new create show edit update destroy`

이대로는 pending migrate db에러가 나므로

`rake db:migrate`로 실제 db에 적용시키겠다고 rake해줄것!



![1531099891498](C:\Users\student\AppData\Local\Temp\1531099891498.png)

루트를 posts에서 blogs로 바꿔준당









![1531100196258](C:\Users\student\AppData\Local\Temp\1531100196258.png)

route들 다 지우고

![1531100226986](C:\Users\student\AppData\Local\Temp\1531100226986.png)

![1531100260915](C:\Users\student\AppData\Local\Temp\1531100260915.png)

![1531100321295](C:\Users\student\AppData\Local\Temp\1531100321295.png)

![1531100352091](C:\Users\student\AppData\Local\Temp\1531100352091.png)

![1531100382350](C:\Users\student\AppData\Local\Temp\1531100382350.png)

링크 달림

==> `<a href=""></a>`  이제 이 a태그를 쓰지 않고 **link 뷰 헬퍼**를 쓸 거에요 **:  link_to**





원래 스캐폴드에서도

![1531100461366](C:\Users\student\AppData\Local\Temp\1531100461366.png)

얘도 뷰헬퍼를 통해 만들었다는 것을 알 수 있당





![1531100670662](C:\Users\student\AppData\Local\Temp\1531100670662.png)

create로 넘겼는데

실제로 /blogs/new에다가 글 써서 제출 눌러보면 show페이지를 보여준다

**>>  일단 /blogs/create는 없으니까 get방식으로 보내는 /blogs/ 인 다른 url을 찾는데 그게**

**>>  /blogs/:id 니까 create가 id인 것으로 인식해서 show페이지로 보여준 것**





![1531100700243](C:\Users\student\AppData\Local\Temp\1531100700243.png)

![1531100802141](C:\Users\student\AppData\Local\Temp\1531100802141.png)



post방식으로 날려줘야 하므로

![1531100830089](C:\Users\student\AppData\Local\Temp\1531100830089.png)

method post를 추가해 준다





---

우리 지금 'restful' 하고 있습니다.

-

posts/create

create/posts

url을 지맘대로 만들기 시작하다 보니까 인터넷 환경이 너무 지저분해짐.

url통일되게 만들자고 어떤 컴공 교수가 제안함.

동사 활용해서 만들자. (동사 - 목적어 형태로 활용 가능하도록  규칙 순서 정착시킴)

​        **<u>verb</u>**(method/verb)    +    **<u>url</u>**

ex.  		    get			/posts			index

​		   post			/posts			create



![1531101037718](C:\Users\student\AppData\Local\Temp\1531101037718.png)

즉 그냥 /blogs로만 보낸당



다시 글을 넣어보니

![1531101087025](C:\Users\student\AppData\Local\Temp\1531101087025.png)

이 에러



![1531101114599](C:\Users\student\AppData\Local\Temp\1531101114599.png)

이부분 주석처리!   (authenticity 어쩌구 보안 처리를 하면 다른 곳에서 자기 맘대로 글 등록하지 못하게 할 수 있는 거였지. url로 그냥 parameter 채워서 보내면 글도 등록 가능하고 계정도 새로 만들 수 잇고. 그래서 get방식으로 url만들면 안되고 **(사용자 정보를 받을 때는 get 방식이 아니라 post방식으로 해야 하고. 토큰도 같이 보내야 한다.)**)



다시 하면 제대로 될 것

![1531101150263](C:\Users\student\AppData\Local\Temp\1531101150263.png)



