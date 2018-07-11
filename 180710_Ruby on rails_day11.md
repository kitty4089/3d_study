18 .07 .10  (수업 다 잘 들었당 ㅎㅎ 다행. 노트도 잘 한 듯)

####  c9 프로젝트 ;   exhibition



![1531182617326](C:\Users\student\AppData\Local\Temp\1531182617326.png)

## HTTP - REST API, RESTful Architecture

---







*url :  주문서

주문서(url)의 양식이 통일이 안되어 있었다. 개발자들이 자기 마음대로 썼었다. 서로 통신하는데 불편. miscommunication. (routing을 자기 마음대로 한 것. 일정한 규약 없이)

ex.  /posts/create  로 쓰는 사람도, create/posts 로 쓰는 사람도 있당..

**w3c** : 인터넷 규약을 모여서 정하는 곳. 브라우저를 만드는 회사들이 모여 있음.  ex. microsoft,  구글 크롬

- 어떤 컴공 교수님이 논문에 쓴 것을 w3c가 차용한 것
- ==> REST하게 만들자. API 이런 거 명세서 보지 않고도 다 통일되어 알아들을 수 있게.
- **공통규약**  / 주문서를 통일되게 만드는 방법
- 개발자 웹서비스 만드는데 있어서 엄청 중요하다. 취업시도. 안지키면 개발자들로부터 욕 먹는다



http  이런 부분  https는 조금 암호화된 형태,  ftp : 파일 주고 받을 때    sntp : 메일을 주고 받을 때 .

**; 표준적인. 프로토콜. 통신규약** 





**ex. naver페이지**

naver.com 들어가 -> 우클릭, 검사 -> Network탭 -> F5 새로고침 -> 문서들 중 www.naver.com 선택 -> (창을 세로 점 세 개 있는 아이콘 눌러서 왼쪽붙임으로 바꿔서 편하게 보자) -> Remote Address 에 있는 숫자들이 ip주소

![1531183158869](C:\Users\student\AppData\Local\Temp\1531183158869.png)

네이버 서버 있는 IP주소.  이런 숫자로 다 주소로 쓰도록 하는게 규약 

`.`으로 구분된 4가지 숫자의 조합으로 사이트 다 찾아가게 됐었는데 옛날에는. 그래서 url이 전화번호 외우듯이 번호를 외웠어야 하는데.  지금은 건물이름 붙여놓듯이 편하게  http~~ 이런 url (도메인)으로 편하게 바뀜.





### HTTP 기본 속성

HTTP쿠키를 만들고 ,상태가 있는 세션을 활용할 수 있도록 보안 ==> stateless하다





### **URI 통합자 자원 식별자.**   == **url**  (l은 locator 얘도 찾는 친구)

**Uniform**(공통적으로) **Resource**(데이터를) **Identifier**(찾는 친구, 검색어와 비슷하다고 생각하면 된당)

(resource == 데이터)



### REST API 

##### :   동사는 넣지 말고 (뭘 하겠다는) 목적어만 넣도록 하는 규약

*REST :  Representational safe transfer 이지만 이것을 봐서는 아무것도 알 수 없다 의미를 ㅋㅋ

- CRUD 를 아래 동사를 사용해서 표현. 

  *데이터 보내는 방식

  ​	- 수정  PUT

  ​	- 삭제  DELETE

- url에는 간편화 해서 목적어만 쓰겠다.

![1531185049608](C:\Users\student\AppData\Local\Temp\1531185049608.png)





- restful하게 짜여있는 url을 쓰겠다고 하는 것이

![1531183878640](C:\Users\student\AppData\Local\Temp\1531183878640.png)

이 한 줄이다. ==> `resources(:내가 정하는 이름)`



`rake routes`로 (생성된 routing들 다 보고 싶을 때)

찍어 보면.. restful하게 짜여진 url 들을 확인할 수 있다



- 위 한 줄로 끝났던 것의 편리함을 느끼기 위해

  전에 이제까지 했던 코드로 번거롭게 만들어 보자.

`get '/works' => 'works#index', as: :works`

![1531184003241](C:\Users\student\AppData\Local\Temp\1531184003241.png)

이제까지 했듯이 get방식으로 저기에 routing 해주고. works라는  prefix(별명)을 달아줘!



차례대로 만들어 보자.

![1531185150563](C:\Users\student\AppData\Local\Temp\1531185150563.png)

![1531185351092](C:\Users\student\AppData\Local\Temp\1531185351092.png)

원래 이런식으로 한 줄 한 줄 다 정의해 줘야 한다 (되게 귀찮음)



cf. 단 몇 개 다른 부분이 있음..

​	ex. update같은 경우 put/patch 두 가지가 있음. (둘이 거의 같고 큰 차이는 없음, 둘 중 아무거나 쓰면 된다)

​		(우리는 put 방식을 썼다)

​		1. **put** :  전체를 수정할 때

​		2. **patch** : 한 부분을 수정할 때





근데 뭐 이 여러 routing 다 아래 한 줄이면 된당

`resources(:works)`





---

#### 본격적으로 exhibition 전시회를 위한 웹페이지를 만들어 보자

(아카이브 같은 역할 하게 될 거시다 ㅎㅎ)



모델을 만들장 (N대 M)

Work	N  (N쪽이 자기가 속한 정보를 갖고 있다. (많은 쪽))

Maker	M



근데 N : M 은 어려우니까 일단 N : 1로 만들쟝 ㅎㅎ

`rails g model Work title desc image maker_id:integer`

작품은 제목, 설명, 사진을 가지고 있고 자기가 속한 '메이커'의 정보를 가지고 있다. (많은 쪽이니까 ㅎ)



`rails g model Maker name phone_number email`



여기까지 migrate폴더에 각 테이블이 생성됐음을 (설계도가) 알 수 있다

![1531185733557](C:\Users\student\AppData\Local\Temp\1531185733557.png)



이 모델 간의 관계 정의해 주자

`has_many :works`

![1531185775301](C:\Users\student\AppData\Local\Temp\1531185775301.png)

`belongs_to :maker`

![1531185803557](C:\Users\student\AppData\Local\Temp\1531185803557.png)



rake해주자

`rake db:migrate`

![1531185844228](C:\Users\student\AppData\Local\Temp\1531185844228.png)



컨트롤러를 만들어 주자 (복수형으로)

`rails g controller works index new create show edit update destroy`



![1531185938719](C:\Users\student\AppData\Local\Temp\1531185938719.png)

그리고 routes파일에 가서 get으로 만들어진 쓸데없는 애들 다 지워준다.



![1531185973083](C:\Users\student\AppData\Local\Temp\1531185973083.png)

애만 남기면 되니까



루트만 지정해 주자

![1531185996500](C:\Users\student\AppData\Local\Temp\1531185996500.png)

`root 'works#index'`



*cf.* 아래 authenticity  error가 난다면! app -> controllers -> application control 어쩌구 가서 주석처리

![1531186596220](C:\Users\student\AppData\Local\Temp\1531186596220.png)

![1531186587899](C:\Users\student\AppData\Local\Temp\1531186587899.png)



views페이지에 **new**

```html
<h1>새 작품 업로드</h1>
<!-- 기존 form 태그 :  애는 default가 get방식이라 따로 method지정 post로 해 줘야 된다.-->
<!--<p><form action="/works" method="post">-->
<!--    제목 :  <input type="text" name="title"><br>-->
<!--    설명 : <input type="text" name="desc"><br>-->
<!--    이미지_url :  <input type="text" name="image"><br>-->
<!--    메이커_id : <input type="text" name="maker_id"><br>-->
<!--    <input type="submit" value="등록">-->
<!--</form></p>-->

<!--rails form 태그로 form 만들기 :  애는 default가 post방식이라 따로 method지정 안해줘도 된다. -->
<%= form_tag("/works") do %>
<!--form 내용물 : input 등등 -->
    제목 : <%= text_field_tag(:title) %><br>
    설명 : <%= text_field_tag(:desc) %><br>
    이미지url : <%= text_field_tag(:image) %><br>
    메이커_id : <%= text_field_tag(:maker_id) %><br>
    <br>
    <%= submit_tag("작품 올리기") %>
<% end %>
```







이제 새 글 쓰면 create로 잘 넘어 온다

![1531186692158](C:\Users\student\AppData\Local\Temp\1531186692158.png)

![1531186683269](C:\Users\student\AppData\Local\Temp\1531186683269.png)



이제 입력하는 새 글을 db에 저장하기 위해 컨트롤러에서 create를 정의해 주자

![1531187002195](C:\Users\student\AppData\Local\Temp\1531187002195.png)



새 글 넣어보자

![1531187147310](C:\Users\student\AppData\Local\Temp\1531187147310.png)

![1531187166854](C:\Users\student\AppData\Local\Temp\1531187166854.png)

(결과는 콘솔 창에서 확인 가능)

![1531187196614](C:\Users\student\AppData\Local\Temp\1531187196614.png)



그러나 더 정확한 확인을 위해서는 bash창에서

`rails c`

`Work.all`

로 db를 찍어보면 더 정확하게 db상황 확인 가능하겠지.

(그 다음 다른 코드 작성하려면 `exit`해야 함 유의~~!! )







---

### `<form>` tag도 편하게 만들어 보자 이제

![1531187248297](C:\Users\student\AppData\Local\Temp\1531187248297.png)

`<%= form_tag %>`  :   `<form>  </form>`  form태그를 열고 닫고 해주는 것과 같은 코드



즉, 확인해 보자.

![1531187348807](C:\Users\student\AppData\Local\Temp\1531187348807.png)

위는 내가 여러 줄로 직접 쓴 코드

/ 밑은 `form_tag` 로 **'form 헬퍼'** 로 열어준 form 태그



![1531187604391](C:\Users\student\AppData\Local\Temp\1531187604391.png)

![1531187613652](C:\Users\student\AppData\Local\Temp\1531187613652.png)

'페이지 소스 보기' 해보면

![1531187668378](C:\Users\student\AppData\Local\Temp\1531187668378.png)

자동으로 form 이 생성됐음을 알 수 있다



![1531189344353](C:\Users\student\AppData\Local\Temp\1531189344353.png)

이런 식으로 완성해 준다.

```html
<!--rails form 태그로 form 만들기 :  애는 default가 post방식이라 따로 method지정 안해줘도 된다. -->
<%= form_tag do %>
<!--form 내용물 : input 등등 -->
    제목 : <%= text_field_tag(:title) %><br>
    설명 : <%= text_field_tag(:desc) %><br>
    이미지url : <%= text_field_tag(:image) %><br>
    메이커_id : <%= text_field_tag(:maker_id) %><br>
    <br>
    <%= submit_tag("작품 올리기") %>
<% end %>
```

##### cf. 나도 검사창 예쁘게 보고 싶다!!





컨트롤러 정의

![1531189449194](C:\Users\student\AppData\Local\Temp\1531189449194.png)





#### form 헬퍼 구글링 ㄱㄱ





---

퍼펙트 루비 온 레일즈 171 쪽 ~





---

### Makers 모델로도 똑같이 만들어줘 보자

`rails g controller makers index new create show edit update destroy`

CRUD를 위한 7가지 액션 만들어줌.



routes.rb가서 쓸데없는 것들 없애줌

![1531196914409](C:\Users\student\AppData\Local\Temp\1531196914409.png)





![1531202956737](C:\Users\student\AppData\Local\Temp\1531202956737.png)

우리 프로필 csv 파일을 다운받는당



![1531203329523](C:\Users\student\AppData\Local\Temp\1531203329523.png)

다운받은 파일을 c9 db폴더로 드래그앤 드랍

![1531203377264](C:\Users\student\AppData\Local\Temp\1531203377264.png)

![1531203396582](C:\Users\student\AppData\Local\Temp\1531203396582.png)



![1531203410733](C:\Users\student\AppData\Local\Temp\1531203410733.png)

주석 다 지우고



![1531203539393](C:\Users\student\AppData\Local\Temp\1531203539393.png)

`require 'csv'`

csv파일 쓰기 위해서 위와 같이 require 해 줘야.



`file = File.read('43dp.csv')`

![1531203840567](C:\Users\student\AppData\Local\Temp\1531203840567.png)

근데 no such file 하면서 경로 못찾으니까

파일 위치를 맨 바깥으로 끌자



![1531203883837](C:\Users\student\AppData\Local\Temp\1531203883837.png)



seed파일에다 데이터를 넣자

---

![1531208042207](C:\Users\student\AppData\Local\Temp\1531208042207.png)

`headers: true`  이 부분 :  

![1531208130205](C:\Users\student\AppData\Local\Temp\1531208130205.png)

다운받은 프로필 csv파일을 보면. 여기 첫 번째 줄이 있잖쓰. 이 부분이 header니까 여기는 안읽겠다는 뜻

---









---

#### seed에서 puts결과 보는 법

:   콘솔창에  `rake db:seed`로

![1531204785352](C:\Users\student\AppData\Local\Temp\1531204785352.png)

![1531204808629](C:\Users\student\AppData\Local\Temp\1531204808629.png)







---

#### 작품 등록할 때 작가를 드롭다운 메뉴로 16명 중에 선택하도록 만들어 보자

- select box html

  cf. 'rails select tag'  구글링 ㄱㄱ  :   링크 헬퍼 알고 싶을 때 ㅎㅎ

  ![1531204686780](C:\Users\student\AppData\Local\Temp\1531204686780.png)

  저 부분을 

  select_tag로 바꾼다

  

  ![1531204708715](C:\Users\student\AppData\Local\Temp\1531204708715.png)

  

  ![1531204729007](C:\Users\student\AppData\Local\Temp\1531204729007.png)

  바뀐 모습 확인

  

  

  엥 근데 정작 옵션 넣는 방법이 까다로우니

  다시 원래대로 text_field로 바꾸고

  `<select>` 태그를 쓰자

  - work 콘트롤러에서 db 데이터 변수에 담아두고

  ![1531205057731](C:\Users\student\AppData\Local\Temp\1531205057731.png)

  -  new view페이지에 가서 select 태그 안에 입력

  ![1531205197451](C:\Users\student\AppData\Local\Temp\1531205197451.png)

  

  ![1531205208611](C:\Users\student\AppData\Local\Temp\1531205208611.png)

  

  확인.

  

  

  

  ---

  #### gem carrier wave  :   이미지 업로드 하는 애 (온라인 주소 말고 로컬에 저장된 이미지)

  

  ![1531206659314](C:\Users\student\AppData\Local\Temp\1531206659314.png)

  

  ![1531206691029](C:\Users\student\AppData\Local\Temp\1531206691029.png)

  **bundle 했으니 서버 껐다 켜야 함**

  

  `rails g uploader Image`

  ![1531206726747](C:\Users\student\AppData\Local\Temp\1531206726747.png)

  ![1531206834289](C:\Users\student\AppData\Local\Temp\1531206834289.png)

  uploader가 생겼다

  ![1531206932460](C:\Users\student\AppData\Local\Temp\1531206932460.png)

  저 이름을 복붙

  

  이제 mount를 해 줘야 한다

  ![1531206892740](C:\Users\student\AppData\Local\Temp\1531206892740.png)

  ==> work.rb에다가!!

  

  ![1531206963698](C:\Users\student\AppData\Local\Temp\1531206963698.png)

  여기에 아까 복사한 이름 붙여넣기

  

  - Image 들을 쭉 upload한다

  

  

  new페이지에 온다

  ![1531207033663](C:\Users\student\AppData\Local\Temp\1531207033663.png)

  

![1531207058790](C:\Users\student\AppData\Local\Temp\1531207058790.png)

file_field_tag로 바꿔준다

![1531207110952](C:\Users\student\AppData\Local\Temp\1531207110952.png)

이렇게 바뀜



![1531207121669](C:\Users\student\AppData\Local\Temp\1531207121669.png)

누르면 이렇게 파일 올릴 수 있게 로컬이 열림



파일을 선택해 올려보쟈

![1531207159065](C:\Users\student\AppData\Local\Temp\1531207159065.png)

![1531207185684](C:\Users\student\AppData\Local\Temp\1531207185684.png)

이미지값이 들어가지 않은 것이 보임.. 어! 뭐가 문제징 ㅠㅠㅠ



![1531207372341](C:\Users\student\AppData\Local\Temp\1531207372341.png)

반드시 이 코드를 추가해 줘야 한다 .`<form>`태그에 ~~~

==> html에서 텍스트가 아니라 파일을 받을 때. 이미지나 단순 텍스트 뿐 아니라 여러 가지 형태의 파일 포맷을 받겠다고 하는 것



이제 된당 ㅎㅎ



![1531207705681](C:\Users\student\AppData\Local\Temp\1531207705681.png)

db 데이터 넣을 때 .create로 만들면 이 redirect 때 id 값 받아올 수 있는 방법이 없다  ㅠㅠ

그러니 .new 한다음 .save로 넣는 방법으로 하자

![1531207817422](C:\Users\student\AppData\Local\Temp\1531207817422.png)



---

![1531208619601](C:\Users\student\AppData\Local\Temp\1531208619601.png)

- **maker.name으로 이름을 불러올 수 있는 이유 :**

  아래와 같이 db끼리 관계가 설정되었기 때문 >_<    (이 belongs_to :maker 에 썼던 maker를 쓴 것. Maker db를 검색할 수 있게 되엇다. Work 모델이 maker_id 를 품고 있기 때문에. 그 id값 가지고 있는 Maker데이터를 불러오는 것.)

![1531208671034](C:\Users\student\AppData\Local\Temp\1531208671034.png)

![1531208643513](C:\Users\student\AppData\Local\Temp\1531208643513.png)







- _path 이런 거 우리 한 것 :   (prefix 이런 거) - url간단히 하기 위해 별명 지은 것



#### **뷰 헬퍼**

- **link_to** :  애는 루비에서 html코드를 자동으로 생성해쥼
  - 실제로 검사 해보면 <a>태그 로 나오잖아. 자동으로 만들어주는 애.