18 .07 .13

## facebook login 기능 구현

*c9프로젝트 :    '**devise_review**' (강사님은  'bloggg')

![1531444449306](C:\Users\student\AppData\Local\Temp\1531444449306.png)





---

1.  Gemfile에 gem 2개 깔아준다

![1531447141689](C:\Users\student\AppData\Local\Temp\1531447141689.png)

carrierwave(로컬파일 이미지 웹에 업로드 해주는 gem) / devise 

-> `bundle`



2. devise gem을 사용하기 위해 install 해준다

`rails generate devise:install`



3. devise gem 이 install 되었으니 user db를 만들어 준다

` rails g devise user`

![1531447506046](C:\Users\student\AppData\Local\Temp\1531447506046.png)

(devise로 user 만든 모습)



4. scaffold로 블로그 db만들어 준다. (model같은 거)

`rails g scaffold Blog title content image`

![1531447264708](C:\Users\student\AppData\Local\Temp\1531447264708.png)

그럼 이렇게 생긴다



이제 db관련된 것들 다 완성되었으니 rake 해 준다

->  `rake db:migrate`



5. carrierwave gem 이 깔린 상태이니,  uploader를 만들어 준다 (업로더 이름: Photo)

`rails g uploader Photo`

![1531447555154](C:\Users\student\AppData\Local\Temp\1531447555154.png)

이렇게 uploader가 생긴다. 



6. 우리 블로그 모델(db)의 image항목에 이 업로더를 이용해서 파일을 웹에 올리겠다고 mount해준다

`mount_uploader :image, PhotoUploader`

![1531447598243](C:\Users\student\AppData\Local\Temp\1531447598243.png)



==> (업로더 이름을 내가 만들었던 업로더 이름으로 맞춰 줘야 한다)

![1531446403849](C:\Users\student\AppData\Local\Temp\1531446403849.png)

: 바꾸기 전 default 코드의 모습

![1531446416181](C:\Users\student\AppData\Local\Temp\1531446416181.png)

: 내가 만든 업로더 이름이 Photo 업로더이니   photouploader로 바꿔준 모습



**이제 블로그 준비가 다 끝났다**

---

블로그 새 글을 올리는 new 페이지를 확인해 본다

![1531447752782](C:\Users\student\AppData\Local\Temp\1531447752782.png)

form 을 render 하게 되어 있으니 `_form`페이지를 찾아 본다



![1531447802680](C:\Users\student\AppData\Local\Temp\1531447802680.png)

내용을 보고 이미지 항목은 로컬 파일에서 찾아서 올리게 되므로 `file_field`로 바꿔준다



![1531447879060](C:\Users\student\AppData\Local\Temp\1531447879060.png)

이렇게 선택하도록 나온다 ㅎㅎ

(cf. 파일 선택 부분은 구글 크롬에서 보여주는 것이기 때문에 (내가 한글 크롬을 쓰므로) 얘만 한글로 나온당)



목록에서 이미지 주소가 아니라 이미지가 바로 보이도록 `<img src>`태그로 바꿔 준다.

![1531447958904](C:\Users\student\AppData\Local\Temp\1531447958904.png)





![1531447996756](C:\Users\student\AppData\Local\Temp\1531447996756.png)

글들을 등록해 본 모습.



부트스트랩 css / js 코드 layout에 복붙

![1531448072428](C:\Users\student\AppData\Local\Temp\1531448072428.png)







![1531448199094](C:\Users\student\AppData\Local\Temp\1531448199094.png)

![1531448226571](C:\Users\student\AppData\Local\Temp\1531448226571.png)

![1531448235715](C:\Users\student\AppData\Local\Temp\1531448235715.png)

![1531448255909](C:\Users\student\AppData\Local\Temp\1531448255909.png)

![1531448262715](C:\Users\student\AppData\Local\Temp\1531448262715.png)



![1531448183306](C:\Users\student\AppData\Local\Temp\1531448183306.png)





![1531448372304](C:\Users\student\AppData\Local\Temp\1531448372304.png)

![1531448384614](C:\Users\student\AppData\Local\Temp\1531448384614.png)

![1531448365654](C:\Users\student\AppData\Local\Temp\1531448365654.png)





![1531448443088](C:\Users\student\AppData\Local\Temp\1531448443088.png)

![1531448469793](C:\Users\student\AppData\Local\Temp\1531448469793.png)

![1531448489544](C:\Users\student\AppData\Local\Temp\1531448489544.png)

![1531448521264](C:\Users\student\AppData\Local\Temp\1531448521264.png)



![1531448573531](C:\Users\student\AppData\Local\Temp\1531448573531.png)

근데 container가 없어진 탓에 양쪽 padding 사라짐 ㅠㅠ



아래 코드 추가

![1531448619698](C:\Users\student\AppData\Local\Temp\1531448619698.png)

![1531448637757](C:\Users\student\AppData\Local\Temp\1531448637757.png)

아름답게 맞춰진 모습 ㅎㅎ



![1531448663625](C:\Users\student\AppData\Local\Temp\1531448663625.png)

너무 다양한 이 메뉴들 없애주자..



![1531448712279](C:\Users\student\AppData\Local\Temp\1531448712279.png)

우클릭 -> 검사



지운다

![1531448776907](C:\Users\student\AppData\Local\Temp\1531448776907.png)

![1531448787802](C:\Users\student\AppData\Local\Temp\1531448787802.png)



![1531448879486](C:\Users\student\AppData\Local\Temp\1531448879486.png)



index페이지에

![1531448907346](C:\Users\student\AppData\Local\Temp\1531448907346.png)

![1531448926395](C:\Users\student\AppData\Local\Temp\1531448926395.png)

![1531449023777](C:\Users\student\AppData\Local\Temp\1531449023777.png)



![1531449043197](C:\Users\student\AppData\Local\Temp\1531449043197.png)

![1531449050964](C:\Users\student\AppData\Local\Temp\1531449050964.png)



![1531449093689](C:\Users\student\AppData\Local\Temp\1531449165644.png)





---

![1531449295569](C:\Users\student\AppData\Local\Temp\1531449295569.png)

![1531449326601](C:\Users\student\AppData\Local\Temp\1531449326601.png)





----

![1531449436240](C:\Users\student\AppData\Local\Temp\1531449436240.png)

#### 패딩과 마진을 class로 조절 가능.

*ex.*   p-3  : padding   : 패딩을 3을 준다

​	m-5   : margin   :  마진을 5를 준다

![1531449479715](C:\Users\student\AppData\Local\Temp\1531449479715.png)



- ex.  0으로 바꿔 보자

![1531449540966](C:\Users\student\AppData\Local\Temp\1531449540966.png)

![1531449558832](C:\Users\student\AppData\Local\Temp\1531449558832.png)





![1531449608576](C:\Users\student\AppData\Local\Temp\1531449608576.png)

![1531449629709](C:\Users\student\AppData\Local\Temp\1531449629709.png)

![1531449688762](C:\Users\student\AppData\Local\Temp\1531449688762.png)



![1531449664613](C:\Users\student\AppData\Local\Temp\1531449664613.png)





![1531449704975](C:\Users\student\AppData\Local\Temp\1531449704975.png)

: 배경색



> 태그 안에서 그냥 fontcolor 이런식으로 다 지정해 주던 것들을 
>
> 부트스트랩에서는 class로 관리한다.



```
x :  x축  ( 가로축 )

y :  y축  ( 세로축 )

t :  top

b : bottom

l  :  left

r  : right



=> p(padding)  / m (margin)  의 각각을 조절
	p-숫자, m-숫자  :  숫자는 0~5
	md는 device size를 의미 (p-3이고 p-md-5 :  작아질 경우(md) padding이 더 생기도록 하는 부분)
```

![1531449997935](C:\Users\student\AppData\Local\Temp\1531449997935.png)

ex. grid 에서 확인해 보면,   **md** :  medium





![1531450058193](C:\Users\student\AppData\Local\Temp\1531450078659.png)

![1531450667706](C:\Users\student\AppData\Local\Temp\1531450667706.png)

![1531450677341](C:\Users\student\AppData\Local\Temp\1531450677341.png)

이미지 사이즈 비율 정해주는 코드

**25/50/75/100**  로만 지정 가능





---

![1531456304222](C:\Users\student\AppData\Local\Temp\1531456304222.png)

전부 주석 처리

(파일 자체를 지워도 되지만 혹시 몰라서 주석 처리)



![1531456326687](C:\Users\student\AppData\Local\Temp\1531456326687.png)



![1531456339403](C:\Users\student\AppData\Local\Temp\1531456339403.png)

지금까지 scaffold css랑 섞여서 좀 이상하게 보였는데

이제 제대로 보이는 것 (원래 템플릿대로)



---

![1531456648263](C:\Users\student\AppData\Local\Temp\1531456648263.png)

![1531456657489](C:\Users\student\AppData\Local\Temp\1531456657489.png)

link_to와 a태그로 만든 두 줄 둘이 똑같다. ==> rails에서 제공하는 link_to 를 쓰도록 할 것!  (a태그 보다!)





![1531456683904](C:\Users\student\AppData\Local\Temp\1531456683904.png)



![1531456766636](C:\Users\student\AppData\Local\Temp\1531456786526.png)

위에 버튼도 link_to 로 바꿔 주자



원래 있던 class 적용하자

![1531456840679](C:\Users\student\AppData\Local\Temp\1531456840679.png)

태그 안에서는 `class=" "`  등호로

link_to 에서는 `class:" "`  :로



---

![1531457019886](C:\Users\student\AppData\Local\Temp\1531457019886.png)

홈 로고 수정

![1531457031434](C:\Users\student\AppData\Local\Temp\1531457031434.png)

누르면 루트(홈)으로 이동

---



![1531457140150](C:\Users\student\AppData\Local\Temp\1531457202925.png)

회원가입도 링크 걸어준다



![1531457233880](C:\Users\student\AppData\Local\Temp\1531457233880.png)

딱 붙어 있는 거 수정하자

![1531457615257](C:\Users\student\AppData\Local\Temp\1531457615257.png)

`ml-숫자`   :   ml  은 left   (왼쪽 마진)



*cf.*

ml  px  pb   부트 스트랩에서 정해 놓은 마진 같은 거 정할 수 있는.

0~5 만 가능

---

***rem 단위**

​	r은 루트

​	html문서를 작성했을 때 가장 최상위에 정의된 폰트사이즈.  

​	최상위에 정의된 폰트사이즈에 비례한 단위. 

​	ex. 폰트 사이즈가 원래 처음에 16px로 정의되어 있다면 1rem = 16px

0 :  0

1:   0.25rem

2:   0.5rem

3:   1rem

4:   1.5rem      

5:   3rem



구글 크롬 설정 -> 글꼴 크기 (디폴트 : 중간)  이런 데서 브라우저 자체 글씨 크기 설정 가능하다. 사용자가 



rem 단위 안쓰고 막 px 쓰고 그러면 이 브라우저 폰트 설정에 따라서 비례해서 늘어나는 게 아니라 레이아웃 이상해짐..막 깨지고 글자 사이 여백 등등. 설정에 따라 조정이 되야 하니까.



아직도 많은 웹사이트들이 rem단위를 써주고 있지 않음. 특히 정부 사이트 같은.. 나중에  모바일에서도 되게 하는 사이트 만들 때는 rem단위를 써야 한당 ㅎㅎ 예쁘게 사이트 다 잘 보이게 하려면..

---





Gemfile에 i18n 깔고 bundle

![1531459075822](C:\Users\student\AppData\Local\Temp\1531459075822.png)

![1531459042508](C:\Users\student\AppData\Local\Temp\1531459042508.png)

한글로 바뀜



![1531459169761](C:\Users\student\AppData\Local\Temp\1531459169761.png)

`rails g devise:i18n:views`

view를 다 뽑아주세요 라는 명령어

원래 이게 숨어있기 때문에 나오게 해서 (뽑아 줘서)  우리가 수정 가능하도록 해 주는 애



그럼 뿅 devise폴더가 생김

![1531459184831](C:\Users\student\AppData\Local\Temp\1531459184831.png)



ex. 

![1531459205456](C:\Users\student\AppData\Local\Temp\1531459205456.png)

이 부분이 한글로 변경시키겠다는 부분  (sign_in을 '로그인' 한글로)

![1531459387889](C:\Users\student\AppData\Local\Temp\1531459387889.png)

이렇게



![1531459409980](C:\Users\student\AppData\Local\Temp\1531459409980.png)

class를 먹이면 

![1531459425764](C:\Users\student\AppData\Local\Temp\1531459425764.png)





![1531459496645](C:\Users\student\AppData\Local\Temp\1531459496645.png)

![1531459538502](C:\Users\student\AppData\Local\Temp\1531459538502.png)

![1531459689425](C:\Users\student\AppData\Local\Temp\1531459689425.png)



![1531459674903](C:\Users\student\AppData\Local\Temp\1531459674903.png)





반응형으로 만들자

![1531459740024](C:\Users\student\AppData\Local\Temp\1531459740024.png)

-md  추가 (col들에다가)

![1531459827972](C:\Users\student\AppData\Local\Temp\1531459827972.png)



![1531459863482](C:\Users\student\AppData\Local\Temp\1531459863482.png)

![1531459887871](C:\Users\student\AppData\Local\Temp\1531459887871.png)

줄여도 레이아웃이 잘 되도록





![1531459930259](C:\Users\student\AppData\Local\Temp\1531459930259.png)

![1531459943859](C:\Users\student\AppData\Local\Temp\1531459943859.png)



색도 바꿔보자

![1531459965680](C:\Users\student\AppData\Local\Temp\1531459965680.png)

![1531459994218](C:\Users\student\AppData\Local\Temp\1531459994218.png)





뭐 조건들 있는 파일이래

![1531460116729](C:\Users\student\AppData\Local\Temp\1531460116729.png)



![1531460353389](C:\Users\student\AppData\Local\Temp\1531460353389.png)

![1531460374155](C:\Users\student\AppData\Local\Temp\1531460374155.png)

![1531460387753](C:\Users\student\AppData\Local\Temp\1531460387753.png)

버튼화



![1531460447741](C:\Users\student\AppData\Local\Temp\1531460447741.png)

![1531460461772](C:\Users\student\AppData\Local\Temp\1531460461772.png)

![1531460473628](C:\Users\student\AppData\Local\Temp\1531460473628.png)

![1531460486089](C:\Users\student\AppData\Local\Temp\1531460486089.png)

![1531460498005](C:\Users\student\AppData\Local\Temp\1531460498005.png)

![1531460504270](C:\Users\student\AppData\Local\Temp\1531460504270.png)







---

*cf.*  **flexbox froggy**   :  game을 통해 flex를 가르쳐 주는 귀요미 배치 연습하는 사이트.

 부트스트랩은 기본적으로 flex가 다 먹여져 있어서. 

ex. `flex-end;`

(front-end 개발자가 되면 해보자)



![1531460810235](C:\Users\student\AppData\Local\Temp\1531460810235.png)

![1531461129339](C:\Users\student\AppData\Local\Temp\1531461129339.png)

- vh :  view height



![1531461143134](C:\Users\student\AppData\Local\Temp\1531461156942.png)

80이라는 숫자는 보이는 웹페이지 화면 맨 위 ~ 맨 끝에서 비율이다.

:  navbar 염두에 두면서 간격 조정하면 된다. 수치 조절해서 (ex. 100이면 너무 많이 떨어진다 네브바랑.)

80정도로 했더니 적당한듯.







---

### 블로그 새 글쓰기 페이지 글 쓰는 부분 에디터로 예쁘게 만들기

에디터 summernote

- 에디터 하나 설치해서 쓸 거에요

https://summernote.org/

![1531462618692](C:\Users\student\AppData\Local\Temp\1531462618692.png)

![1531462738508](C:\Users\student\AppData\Local\Temp\1531462738508.png)

![1531462817710](C:\Users\student\AppData\Local\Temp\1531462817710.png)





(form for rails textarea  구글링 ㄱㄱ)

-> blogs view페이지에서 `_form.html.erb` 파일 에다가!

![1531462866011](C:\Users\student\AppData\Local\Temp\1531462866011.png)

![1531462937111](C:\Users\student\AppData\Local\Temp\1531462937111.png)



![1531462925628](C:\Users\student\AppData\Local\Temp\1531462925628.png)

텍스트 area 로 일단 바뀐다



이어서 써머노트 자바스크립트 코드를 아래에 넣어줄 것이다.

![1531462969142](C:\Users\student\AppData\Local\Temp\1531462969142.png)



![1531462985502](C:\Users\student\AppData\Local\Temp\1531462985502.png)

복붙



