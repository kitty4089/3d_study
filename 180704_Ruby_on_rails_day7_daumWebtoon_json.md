18. 07 .04

#### ***오늘 한 모든 vscode 파일과 / c9 프로젝트**

**1) vscode**

- webtoon.rb
- webtoon2.rb

   ---------------------

- boxoffice.rb

​    ---------------------

- css.rb
- 'tryCSS폴더 안에'
  - scrap.html
  - style.css  (css 스타일시트)



**2) c9 프로젝트**

- webtoon

---





## 다음 웹툰 json으로 어제 복습



![1530664564884](C:\Users\student\AppData\Local\Temp\1530664564884.png)





### 다음웹툰 json파일을 가져오자

http://webtoon.daum.net/data/pc/webtoon/list_serialized/mon

- 이런 json페이지는 개발자들을 위해서만 공개되어 있다

  막 아무 페이지에서나 뒤에 .json 붙인다고 그렇게 보이는게 아니다

  ==>  '**~~ api**' 이런 식으로 검색해서 json페이지를 제공하는 지 검색해 봐야 하는 것이당

  ​	*ex*. 다음웹툰의 경우 `다음웹툰 api`이런식으로 검색어를 찾아보라는 것. 

- (위 실제 다음웹툰 json url은 강사님이 그냥 알려준 거)



![1530665079472](C:\Users\student\AppData\Local\Temp\1530665079472.png)







---

# 오늘의 코드파일

### (깃헙 - lecture_code 폴더 안에) 

#### 1. webtoon.rb

#### 2. webtoon2.rb

---



git bash열어 -> `cd project` -> `code webtoon.rb`

![1530664693168](C:\Users\student\AppData\Local\Temp\1530664693168.png)

![1530664706900](C:\Users\student\AppData\Local\Temp\1530664706900.png)

vscode로 열린다.





![1530664844806](C:\Users\student\AppData\Local\Temp\1530664844806.png)



httparty gem 을 require로 불러온당

`require 'httparty'`

![1530664943235](C:\Users\student\AppData\Local\Temp\1530664943235.png)

코드 실행해 본다



![1530664991155](C:\Users\student\AppData\Local\Temp\1530664991155.png)

json파일이 그대로 나오게 된당



근데 좀 너무 안이쁘니까 어제는 awesome어쩌구 gem 썼지만 너무 어썸하게 하려다 보니 윈도우에서는 잘 안되니

다른 젬을 깔자

`gem install pp`

![1530665064488](C:\Users\student\AppData\Local\Temp\1530665064488.png)



`pp response`로 다시 찍어보자

![1530665176967](C:\Users\student\AppData\Local\Temp\1530665176967.png)

![1530665224030](C:\Users\student\AppData\Local\Temp\1530665224030.png)

한층 깔끔하게 나오는 것을 알 수 있다 (pp :  pretty 어쩌구임)



![1530665631366](C:\Users\student\AppData\Local\Temp\1530665631366.png)

```ruby
#---------------------#
# 다음 웹툰 json ------#
# 가지고 놀기!! -------#
#---------------------#


require 'httparty'
require 'pp'
require 'json'

url = "http://webtoon.daum.net/data/pc/webtoon/list_serialized/mon"
response = HTTParty.get(url)        #요청을 보내고 그것을 response에 담겠다
                                    #file = File.read(boxoffice.json)
#puts response
# pp response


data = JSON.parse(response.body) #response 안에 들어있는 json을 루비 해시로 바꾸는 것
#pp data   #json형태가 해시로 바뀐 것을 알 수 있다


#json페이지에서 뽑을 정보들을 뽑아보자 - 작품 한 단위 안에 있는 것들을 찬찬히 보면서 유용한 것들 뽑아본다
#title, appthumnailimage(사진), introduction(소개글), genre(장르 ex. 스릴러 등등), averageScore(평점인듯)
webtoon = {
    title: ,
    appThumnailImage: ,
    introduction: ,
    genre: ,
    averageScore:
}

pp webtoon
```

webtoon 해시를 뽑아보자

![1530666365537](C:\Users\student\AppData\Local\Temp\1530666365537.png)

실제 실행시켜보면 해시가 ':이 앞에 찍혀있는 심볼 - => 로켓 표시' 짝으로 돼어 나온다



![1530666505065](C:\Users\student\AppData\Local\Temp\1530666505065.png)

data가 웹툰들이 들어있는 배열인듯



![1530666658315](C:\Users\student\AppData\Local\Temp\1530666658315.png)









![1530667530702](C:\Users\student\AppData\Local\Temp\1530667530702.png)

![1530667594614](C:\Users\student\AppData\Local\Temp\1530667594614.png)

모든 웹툰 목록이 담긴 가장 상위 배열 data ==> each로 각 배열 요소 반복문 돌면서

각 웹툰    '제목 / 그 소개' 쌍들이 나온다.



#### *오늘은 webtoon.rb에 수업flow 따라서 메모했다

```ruby
#---------------------#
# 다음 웹툰 json ------#
# 가지고 놀기!! -------#
# + 여기는 월요일 웹툰 +#
# + 만 하는 코드에용 +--#
#----------------------#


require 'httparty'
require 'pp'
require 'json'

url = "http://webtoon.daum.net/data/pc/webtoon/list_serialized/mon"
response = HTTParty.get(url)        #요청을 보내고 그것을 response에 담겠다
                                    #file = File.read(boxoffice.json)
#puts response
# pp response


data = JSON.parse(response.body) #response 안에 들어있는 json을 루비 해시로 바꾸는 것
#pp data   #json형태가 해시로 바뀐 것을 알 수 있다



#json페이지에서 뽑을 정보들을 뽑아보자 - 작품 한 단위 안에 있는 것들을 찬찬히 보면서 유용한 것들 뽑아본다
#title, appthumnailimage(사진), introduction(소개글), genre(장르 ex. 스릴러 등등), averageScore(평점인듯)

#--------------------------------------------------------------------------------------------------------------#
#각 정보들이 어떻게 들어가면 나오는 지 해보면서 확인해 본당!!

# pp data["data"][0]      #각 웹툰들이 들어있는 가장 상위 배열이 data인 듯하다. [0] 뽑으면 첫 번째 웹툰이 나오겠지
#pp는 한글 인코딩 안되므로 한글이 필요할 땐 puts로 찍어준다
# puts data["data"][0]["title"]
# puts data["data"][0]["appTumbnailImage"] #뽑아보면 또 해쉬가 나옴 -> 더 들어가야 이미지 url 얻을 수 있음을 알 수 있음
# puts data["data"][0]["appTumbnailImage"]["url"]
# puts data["data"][0]["cartoon"]["genres"][0]["name"]    #장르는 한 작품당 한 개 이상일 수도 있으니 genres (.class확인해보니 배열임) 배열로 돼있음
#--------------------------------------------------------------------------------------------------------------#

# webtoon = {         # Hash를 만들어 준다
#     title: data["data"][0]["title"],
#     appThumnailImage: data["data"][0]["appThumbnailImage"]["url"],
#     introduction: data["data"][0]["introduction"],
#     genre: data["data"][0]["cartoon"]["genres"][0]["name"],
#     averageScore: data["data"][0]["averageScore"]
# }

# #pp webtoon.class    # ==>해쉬
# puts webtoon


# 이제 웹툰 한 개뿐 아니라 모든 웹툰을 뽑기 위해 반복문으로 만들어주자
# all_webtoons = [] #웹툰들 다 넣을 배열을 만들어 준당        #[{웹툰1}, {웹툰2}, {웾툰3}]
# data["data"].each do |webtoon|
#     #all_webtoons안에 모든 웹툰 정보를 해시형태로 push하겠다
#     # puts webtoon.push
#     puts webtoon["title"]
#     puts webtoon["introduction"]
# end

all_webtoons = [] #웹툰들 다 넣을 배열을 만들어 준당        #[{웹툰1}, {웹툰2}, {웾툰3}]
data["data"].each do |webtoon|
    #all_webtoons안에 모든 웹툰 정보를 해시형태로 push하겠다
    all_webtoons.push({
        "title"=>webtoon["title"], 
        "introduction"=>webtoon["introduction"]
    })
end
# puts all_webtoons    #puts가 한글을 보여지게 해주는데 (pp는 한글 인코딩 안됨) 
                       #지금은 배열들 데이터들 한 번에 보여주는 거라 한글 아닌데
                       #한 요소씩 뽑으면 한글로 잘 보여줄 것이당.
#ex.
# puts all_webtoons[0]["title"]
```

지금까지 **월요**웹툰에 대해서만 했으므로!



---

### 이제 모든 요일의 모든 웹툰을 불러와 보자

```ruby
#---------------------#
# 다음 웹툰 json ------#
# 가지고 놀기!! -------#
# + 이제 모든 요일!! +--#
#----------------------#


require 'httparty'
require 'pp'
require 'json'

days = ["mon","tue","wed","thu","fri","sat","sun"]
all_webtoons = [] # mon~sun 월~일까지 모든 웹툰들을 다 넣을 배열 만든다

days.each do |day|
    url = "http://webtoon.daum.net/data/pc/webtoon/list_serialized/#{day}"
    response = HTTParty.get(url)    #각 요일 url을 httparty로 요청. 그리고 그 요청한 페이지 내용들을 response에 담는다
    data = JSON.parse(response.body)    #response에 담긴 json형태 코드들을 해시로 바꿔서(parse) data변수에 담는다
    data["data"].each do |webtoon|
        all_webtoons.push({
        "title"=> webtoon["title"], 
        "introduction"=> webtoon["introduction"]
    })
    end
end

puts all_webtoons.size

all_webtoons.each do |w|
    puts w["title"]
    puts w["introduction"]
end
```





---

## c9프로젝트를 만들장

#### : webtoon

---

##### 지금까지 모든 웹툰을 다 모아올 수 있는 것을 보았다

이제 db에 넣어서 유저에게 보여쥬쟝!!



**webtoon db 테이블 (model)**

- title
- introduction
- thumbnail
- genre
- score

등의 요소를 가진 db를 만들쟝

`rails g model Webtoon title intro image genre score`

![1530670584915](C:\Users\student\AppData\Local\Temp\1530670584915.png)

근데 score는 string (디폴트값) 이 아니라 float값이므로 고쳐준다



![1530670625556](C:\Users\student\AppData\Local\Temp\1530670625556.png)



rake 해준당 ==> schema.rb / seed.rb 파일이 생성된당!

![1530670659716](C:\Users\student\AppData\Local\Temp\1530670659716.png)





httparty gem 써야 하니 Gemfile 수정해준다

![1530670749260](C:\Users\student\AppData\Local\Temp\1530670749260.png)

저장 후



`bundle`

![1530670776592](C:\Users\student\AppData\Local\Temp\1530670776592.png)

#### * rails는 똑똑해서 Gemfile에만 gem 있으면 따로 require 해주지 않아도 된다!!



seeds.rb 에 시드데이터 넣어준다

![1530670885004](C:\Users\student\AppData\Local\Temp\1530670885004.png)

vscode 파일 코드 복붙



근데 이제 배열은 필요 없으므로 (대신 db 에 넣어줄 거니까)

코드를 수정해준다

![1530671158812](C:\Users\student\AppData\Local\Temp\1530671158812.png)



저장 후, 넣은 씨드를 rake 해준당       `rake db:seed`

==> 아무말 나오지 않으면 잘된 것.

==> 그래도 잘됐는 지 확인하고 싶으면 

`rails c`

`Webtoon.all`

##### *새로운 명령어 쓰기 전에 `exit`해주는 것 유의~~~~!!!



webtoons 컨트롤러를 만들어준다

`rails g controller webtoons index`

![1530671428823](C:\Users\student\AppData\Local\Temp\1530671428823.png)

![1530671460194](C:\Users\student\AppData\Local\Temp\1530671460194.png)

컨트롤러가 만들어진 모습 (webtoons)



db 모든 데이터들 배열로 가져와 변수에 담아준다

![1530671542335](C:\Users\student\AppData\Local\Temp\1530671542335.png)



**index페이지에서 보여주자**

get bootstrap 구글링 -> 페이지 들어가서 get started -> css / js 코드 복붙 (layout 파일에다가)

![1530671712393](C:\Users\student\AppData\Local\Temp\1530671712393.png)

Navbar도 필요하면 layout 페이지에 넣어준다

![1530671908931](C:\Users\student\AppData\Local\Temp\1530671908931.png)

![1530671888108](C:\Users\student\AppData\Local\Temp\1530671888108.png)









---

## #Chapter2 /  api 라고 명시된 데이터를 가져오기

***오픈 api**  ;    다 공개해서 깔끔하게 데이터 갖고 올 수 있도록 오픈해 놓은 데이터



*ex.* **공공데이터포털**

www.data.go.kr

- 기상청 정보 등등 별의별 것이 다 있어... 범죄 관련도.



'영진위 오픈 api'  구글링 ;   영화진흥위원회

http://www.kobis.or.kr/kobisopenapi/homepg/main/main.do

- *cf.* 왓챠 조차도 자기네가 하는 게 아니라 영진위 정보를 가져와서 보여주는 것.



![1530677364099](C:\Users\student\AppData\Local\Temp\1530677364099.png)

박스오피스를 보자



api를 활용하기 위해서는 (워낙 공개되어 있는 정보니, 개발자들이 막 가서 마음대로 장난쳐 놓을 수 있으니)

정보제공자가 제공하는 key를 발급받아야 한다

![1530677406860](C:\Users\student\AppData\Local\Temp\1530677406860.png)



그 전에 일단 회원가입을 하자



로그인 하고 다시 키 발급/관리

![1530677606002](C:\Users\student\AppData\Local\Temp\1530677606002.png)

![1530677637200](C:\Users\student\AppData\Local\Temp\1530677637200.png)

![1530677672301](C:\Users\student\AppData\Local\Temp\1530677672301.png)

![1530677696712](C:\Users\student\AppData\Local\Temp\1530677696712.png)





이제 다시 api 매뉴얼을 본다

![1530677741004](C:\Users\student\AppData\Local\Temp\1530677741004.png)

![1530677751276](C:\Users\student\AppData\Local\Temp\1530677751276.png)

json을 지원한다(요청방식)



![1530677771133](C:\Users\student\AppData\Local\Temp\1530677771133.png)

url을 json으로 바꿔서 열어보자



![1530677797586](C:\Users\student\AppData\Local\Temp\1530677797586.png)



키를 넣자

==> 키라는 요청 변수가 있다

![1530677822893](C:\Users\student\AppData\Local\Temp\1530677822893.png)



아까 json 열었던 url 뒤에 ? 를 붙이고 해당 파라미터 key= 뒤에 발급받은 키를 입력해보자 (url 칸에)

![1530677924330](C:\Users\student\AppData\Local\Temp\1530677924330.png)



이번엔 날짜가 필수항목이라네

날짜 파라미터는 뭐로 쓰는지 확인해보자

![1530678027508](C:\Users\student\AppData\Local\Temp\1530678027508.png)



아직 오늘 박스오피스는 나오지 않을 것이니 어제 날짜로 적는다

파라미터 추가는 &을 붙이고 쓴다 (?가 아니라)

![1530678004728](C:\Users\student\AppData\Local\Temp\1530678004728.png)



git bash에서 boxoffice.rb를 vscode로 만들면서 열자

`code boxoffice.rb`

![1530678692259](C:\Users\student\AppData\Local\Temp\1530678692259.png)

```ruby
require 'httparty'  #url 요청해야 하므로 httparty필요

base = "http://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?"   #?가 있어야 뒤의 parameter들을 넘겨줌
key = " 받은 키 입력 "
targetDt = "20180704"

response = HTTParty.get(base + "key=" + key + "&" + "targetDt=" + targetDt)

puts response.body  #.body가 뭐징?
```





아래 있는 parameter들이 다 url에 &&& 로 요청할 수 있는 파라미터들

- 여러 parameter들 이용해 여러 정보를 조회할 수 있다!!

![1530678679391](C:\Users\student\AppData\Local\Temp\1530678679391.png)



ex.

![1530678784029](C:\Users\student\AppData\Local\Temp\1530678784029.png)

- itemPerPage = 1  :  박스오피스 결과를 1개만 보여준다 



![1530678837846](C:\Users\student\AppData\Local\Temp\1530678837846.png)

이 부분은 json 페이지에 보여지는 것들이 어떤 의미인지 설명해 주는 것



![1530678862153](C:\Users\student\AppData\Local\Temp\1530678862153.png)

뭐 이런 것들



이 응답구조들에서 필요한 정보들(뽑을 정보들)을 골라보자

> 순위 정보인 rank
>
> 제목;  title
>
> 누적매출액; salesAcc
>
> 누적관객수; audiAcc

이 4가지로 정했다







### 스트링을 바꾸기

##### ex. 2018-07-02  를  api구조에 맞는 20180702로 바꾸기

`"2018-07-02".gsub("찾을 놈(이미 있는 것중에 없앨 것)","대체할 아이")`

여기서는 하이픈 - 을 없앨 거니까/

`"2018-07-02".gsub("-", "")`

![1530681990288](C:\Users\student\AppData\Local\Temp\1530681990288.png)



ex.  F word를 *로 가리기

`"Fuck you".gsub("F", "\*")`

- 스트링 중에 이미 뜻이 있는 것이 있으므로. ( 점 . 같은 거) 다른 의미로 쓸 수 있도록(그냥 스트링 문자로만 보도록)  본래 의미에서 탈출해서 쓰겠다는 의미로 백슬래쉬 해줘야 함. escape문자. 

![1530682242788](C:\Users\student\AppData\Local\Temp\1530682242788.png)



- 그냥 없애기만 할 경우 (대체할 다른 것이 없을 경우)  `.delete("-") `도 가능

  ==> `"2018-07-02".delete("-")`



( 이후 수업은 

1. boxoffice.rb  (vscode파일) /  
2. c9 프로젝트 webtoon (박스오피스도 같은 프로젝트에 그대로 썼음)

이 두 가지 참고! 따로 마크다운에는 메모하지 않는다)





---

## 다음 주식 페이지에서 정보 뽑기

(이제까지처럼 json에서 말고 페이지에서 원하는 정보 뽑기)

웹페이지 -> 원하는 정보 위에서 우클릭 -> 검사 -> 하이라이트된 코드 우클릭 -> 

copy -> copy selector -> vscode에서 복붙

![1530686099536](C:\Users\student\AppData\Local\Temp\1530686099536.png)

![1530686113636](C:\Users\student\AppData\Local\Temp\1530686113636.png)

![1530686135872](C:\Users\student\AppData\Local\Temp\1530686135872.png)

![1530686151667](C:\Users\student\AppData\Local\Temp\1530686151667.png)

![1530691091301](C:\Users\student\AppData\Local\Temp\1530691091301.png)







---

## 노코기리에 대하여 Nokogiri gem

### * html문서는 나무같은 구조를 가지고 있다

==> **DOM tree**

'DOM 조작'

![1530690587448](C:\Users\student\AppData\Local\Temp\1530690587448.png)

==> **노코기리 Nokogiri gem**  ;  html문서를 **검색**하기 쉽게 해주는 애다.

-  html문서를 구조화 시켜준다 
  - html문서가 노코기리를 거쳐 가공되면 검색하기 좋게 만들어진다 ==> tag를 기준으로
  - 노코기리로 이렇게 가공이 되면 **검색/조작**이 쉬워진다

`Nokogiri::HTML`   (노코기리는 HTML의 메쏘드를 가짐 (`::`  ==> 모듈표시))



(더 궁금하면 nokogiri gem 구글링 ㄱㄱ)



vscode로  css.rb   /  scrap.html    이름으로 새 파일들을 만들어 준다

![1530686994611](C:\Users\student\AppData\Local\Temp\1530686994611.png)



scrap.html에 코드를 입력해 준다

(gamja를 찾아보자)

![1530687049646](C:\Users\student\AppData\Local\Temp\1530687049646.png)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>테스트 문서</title>
    </head>
    <body>
        <h1>숨지 않은 요소 찾기</h1>
        <div>
            <p>gamja</p>

        </div>
    </body>
</html>
```



css.rb 에서 노코기리 gem을 불러주고 코드를 입력

```ruby
require 'nokogiri'

file = File.open('scrap.html')

html = Nokogiri::HTML(file)
puts html.css("p")      #태그로 찾아준다 (p태그를 찾아주는 코드)

puts html.css("h1")
```

![1530687213148](C:\Users\student\AppData\Local\Temp\1530687213148.png)



#### 그럼 p태그가 여러개면?

ex. 

![1530687239002](C:\Users\student\AppData\Local\Temp\1530687239002.png)

![1530687272211](C:\Users\student\AppData\Local\Temp\1530687272211.png)

==> 그냥 다 나온다



하나씩 나오게 하고 싶으면 indexing을 한다 (배열처럼)

![1530687377371](C:\Users\student\AppData\Local\Temp\1530687377371.png)

![1530687525118](C:\Users\student\AppData\Local\Temp\1530687525118.png)

이렇게  그 해당 태그의  '#번째' 요소만 출력된다









---

## css 파일 연결 (스타일시트)



#### cf. vscode에서 작성한 html페이지 코드 실행은 그냥 그 파일을 웹브라우저로 연결프로그램으로 해서 열면 된당

![1530693584537](C:\Users\student\AppData\Local\Temp\1530693584537.png)

더블클릭하면 웹페이지 미리보기를 볼 수 있다. (로컬파일이 웹브라우저로 실행되어 보이는 것뿐이라서 온라인에 올라가 있고 그런 건 아니당..)



`F12`를 눌러서 검사를 해볼 때 css도 확인 할 수 있다.

![1530693930074](C:\Users\student\AppData\Local\Temp\1530693930074.png)

위와 같이 해당 요소 영역 찍으면 

![1530692451064](C:\Users\student\AppData\Local\Temp\1530692451064.png)

이렇게 나옴. 빨간 네모친 부분에서 가장 위에 실제 적용된 서열 대빵인 스타일을 확인할 수 있고

그 밑은 서열이 낮은 적용되지 못한 스타일들이다 (태그 순위에 따라 - 아래 **cascading 서열 순위** 참조)



하지만 저 color 등의 스타일 위에 커서를 올려 놓으면

![1530694032397](C:\Users\student\AppData\Local\Temp\1530694032397.png)

이렇게 체크박스가 보이게 되어 체크해제 / 설정 을 통해서 미리보기 할 수 있다

(색도 red를 blue로 바꾼다든지 웹페이지 상에서 미리보기 해볼 수 있다)

 - (하지만 새로고침을 하면 미리보기조차 바로 사라진다)







---

### 'cascading'  :  css에서, == 우선순위 규칙

(모르겠으면 검색 구글링 ㄱㄱ)

:  가장 하위단계에 적용된 css 스타일이 해당태그에 적용된다는 것 (아래 **서열 순서** 참조)

---

### * 서열 순서

0. 타고타고 들어가는 애가 대빵 (더 specific하게 끝까지 먹인 것)

   - `>` 로 구분해서 들어간다
   - 그 태그에 있는 id나 class는 바로 붙여 써준다.
   - 해당 위치에서 같은 태그가 여러 개 있을 때 #번째 태그를 지칭할 때는 `:nth-child(#)`로 표현한다

   ex. `body > div.my-user-info > p:nth-child(1)#name {color: red;} `

1. id가 대빵  ==> `#`으로 표현  (해당 id이름 앞에 #붙임  ex. `#name`)
   - id는 하나만 있어야 함.
2. 그 다음 class ==> `.`으로 표현 (해당 class 앞에 .붙임  ex. `.important`)
   - 여러 개를 묶어서 하나의 class로 만든다 ( 즉, 같은 class이름을 가진 애가 여러개인 거 )
3. 그 다음 아무 표현이 없는 그냥 태그 ==> ex. p   ==> `<p> </p>` 모든 p태그에 스타일을 먹일 때

---







- **css파일 예쁘게 보여지게 해주는 거**

: www.cleancss.com/css-beautify/

부트스트랩 css파일 같은 거 넣어서 봐 보자.

![1530690672140](C:\Users\student\AppData\Local\Temp\1530690672140.png)







---

#### cf. vscode에서 폴더단위로 한 번에 여는 것도 가능

파일 -> 폴더 열기 -> 폴더 선택 -> 

![1530692620818](C:\Users\student\AppData\Local\Temp\1530692620818.png)

![1530692672482](C:\Users\student\AppData\Local\Temp\1530692672482.png)

-> 그럼 그 폴더 안의 파일들이 한 번에 다 vscode 새 창으로 열린다

![1530692708673](C:\Users\student\AppData\Local\Temp\1530692708673.png)







---

cf. **우리 야호 idea**

웹페이지에서 원하는 정보 있는 부분을 우클릭 -> 검사해서 우리 데이터베이스에 저장합니다 

(10억개든 몇 십억개든)

거기서 강남구 있는애들 걸러

