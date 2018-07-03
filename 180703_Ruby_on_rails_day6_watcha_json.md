18 . 07 .03   화

##### 오전 /  db 연결짓기 (복습)  -  나는 지각을 해서 하지 못함 ㅠㅠ 홍식오빠가 들음 하하

![1530595328614](C:\Users\student\AppData\Local\Temp\1530595328614.png)



#### Data Collection  ->  Data Exhibition

1. API					> 1) 'movie' data table 만듦 (column ;  tilte, genre, rate, director,....)

   Scrapping			> 'data base를 populate 한다'는 표현을 쓴다

   Crawling  			> 2) 'review' 댓글 기능 (movie db표와 1대 N의 관계) :  content, **movie_id** **중요

   > data  					==> N쪽이 1의 정보를 가진다. 
   >
   > page







----

## 오후 /  왓챠에서 제이슨 파일 가져와서 가지고 놀기

왓챠에서 제이슨 파일 가져와서 VS code에서 내가 필요한 영화 정보만 추출하는 과정

***왓챠 : 영화 평점 서비스 사이트**

https://watcha.net/

![1530594347631](C:\Users\student\AppData\Local\Temp\1530594347631.png)

![1530594361048](C:\Users\student\AppData\Local\Temp\1530594361048.png)



url 끝에 .json을 붙여서 enter

![1530594377533](C:\Users\student\AppData\Local\Temp\1530594377533.png)



우상단 raw버튼(아래 그림아이콘)  눌러준다

![1530594401353](C:\Users\student\AppData\Local\Temp\1530594401353.png)

-> raw상태가 나오면, 페이지 우클릭 -> 다른이름으로 저장 -> (project 폴더에 저장했음)





**그 다음 vscode에서 루비코드를 짜보자**

git bash를 연다

`cd project`로 저장할 폴더에 들어간다

`code movie.rb`로 vscode에서 저장할 파일이름을 적어준다 -> vscode에서 해당 파일이름으로 저장된 새 파일이 열린다.

## *오늘 코드 파일 :   project폴더 안에 'movie.rb'

![1530597072390](C:\Users\student\AppData\Local\Temp\1530597072390.png)

정리된 형태로 프린트 찍히게 하기 위해 awesome_print gem 을 깔아주자

`gem install awesome_print`



vscode에 루비코드를 치자

```ruby
# boxoffice.json 파일에 있는 내용을 불러와서
# 가지고 놀아보기
# (JSON 알아보기~)

require 'json'
require 'awesome_print'     #깔끔하게 찍어주는(프린트해주는) 거.. 그냥 puts로 찍으면 막 더럽게 나옴.. ap로 찍으면 좀 더 정리돼서 나온다.
#gem 설치 먼저 :  git bash에서  gem install awesome_print


file = File.read('boxoffice.json')  # ( ) 안에 JSON 파일 이름
data = JSON.parse(file) 
#(json 파일)json처럼 돼있는 거를 해쉬로 바꿔주는 코드.(parse)

# 우리가 필요한 데이터
# : 제목, 장르, 관람가능 연령, 감독, 포스터 사진 URL

# data = {
#     "cards"=> [{}, {}, {}, {}],
#     "load_more"=> XXXX,
#     "total"=> YYYY
# }




title = data["cards"][1]["items"][0]["item"]["title"]
# ap data["cards"][0]["items"][0]["item"]

#------------------------------------------------------------------------------
# 1번 과제(장르, 관람연령, 감독, 포스터 URL)
genre = data["cards"][1]["items"][0]["item"]["main_genre"]
rate = data["cards"][1]["items"][0]["item"]["filmrate"] #관람 가능연령
director = data["cards"][1]["items"][0]["item"]["directors"][0]["name"]
poster = data["cards"][1]["items"][0]["item"]["poster"]["original"]

puts title, genre, rate, director, poster


#------------------------------------------------------------------------------
# 2번 과제
# json 파일 안에는 몇 개의 영화가 들어가 있을까?
list = data["cards"]
ap list.size

#------------------------------------------------------------------------------
# 3번 과제 ; json 파일 안에 있는 모든 영화를 각각 title, genre, 등등 각 항목들 따로 뽑아라
# ==> 반복문을 쓰면 된다  # 1. movies 라는 새로운 배열을 만들어서. 
# movies = [
#     {
#         "title" => ,
#         "genre" => ,
        

#     }
# ]


list.each do |elem|  #elements
    elem["items"][0]["item"]["title"]
end

movies = []
list.each do |elem|  #elements
    movies.push({
        "title" => elem["items"][0]["item"]["title"],
        "genre" => elem["items"][0]["item"]["main_genre"],
        "director" => elem["items"][0]["item"]["filmrate"],
        "rate" => elem["items"][0]["item"]["directors"][0]["name"],
        "poster" => elem["items"][0]["item"]["poster"]["original"]
    })
end

puts movies
```

*실행은 git bash에서!   `ruby movie.rb`   (루비야 movie.rb  파일 열어줘)

​					- (rb파일이니 그대로 실행되어서 bash창에 나옴))



![1530597157772](C:\Users\student\AppData\Local\Temp\1530597157772.png)

==> 배열에 들어간 모습 결과.   (인코딩이 안돼서 한글로 나오진 않음..)

cf. 유니코드 ;   위에 나온 것들이 즉, **각 한글에 해당하는 유니코드**임.







#### 오늘 강사님이 앞에서 적으신 코드 (강사님 올려주신)

http://bit.ly/2KIjZzB

(== https://gist.github.com/djohnkang/49224d820d3993530d6d9683b11ef54e)





---

c9 에서 rails로 프로젝트 :  '**watcha**'



5개의 column을 가진 Movie db table을 만들어 준다

`rails g model Movie title genre rate director poster`

-> db폴더에 migrate파일이 잘 만들어졌는지 확인.  (db설계도 만들어져 있따)

![1530598836337](C:\Users\student\AppData\Local\Temp\1530598836337.png)

-> 실제로 db표를 만들기 위해  `rake db:migrate` 해준다.



컨트롤러도 만들어 준다

`rails g controller movies index new create`

==> 컨트롤러와 index 뒤에  해당하는  루트와 view페이지들도 같이 생성된다



![1530598925272](C:\Users\student\AppData\Local\Temp\1530598925272.png)





루트페이지 지정

![1530599523320](C:\Users\student\AppData\Local\Temp\1530599523320.png)



**get bootstrap**  (구글링)

-> get started ->  **css** / **js** 코드를 복사해서 layout파일 안에 붙여 넣어준다.

![1530605750579](C:\Users\student\AppData\Local\Temp\1530605750579.png)

![1530605760235](C:\Users\student\AppData\Local\Temp\1530605760235.png)

![1530605777227](C:\Users\student\AppData\Local\Temp\1530605777227.png)



*css는 <head>태그 안에 넣고 / js는 <body>태그 끝나기 바로 전에 (body 맨 끝에) 넣는 것이 관례.

(js도 head안에 넣어도 되긴 하다)

![1530605820230](C:\Users\student\AppData\Local\Temp\1530605820230.png)





**부트 스트랩에서 적절한 components들을 가져와서 적절히 복붙해준당**

*ex.* 

**navbar** - layout 페이지에 복붙

**card** - view파일들에 복붙

**jumbotron** - view 파일들에 복붙

![1530605963828](C:\Users\student\AppData\Local\Temp\1530605963828.png)

![1530605982751](C:\Users\student\AppData\Local\Temp\1530605982751.png)









**이제 왓챠 제이슨 파일 불러온다**

![530599767043](C:\Users\student\AppData\Local\Temp\1530599767043.png)

로컬 json파일을 드래그앤드랍으로 끌고와서 넣어준다



db 씨드에 데이터를 넣어준다

![1530600083989](C:\Users\student\AppData\Local\Temp\1530600083989.png)



`rake db:seed`  로 씨드 rake를 해준다

==> 아무 말도 안나오면 잘된 것

![1530600183783](C:\Users\student\AppData\Local\Temp\1530600183783.png)



*확인해 보고 싶으면 콘솔창에

`rails c`

`Movie.all`

해본당

![1530600245298](C:\Users\student\AppData\Local\Temp\1530600245298.png)





index 페이지에 넣어준다

컨트롤러에 먼저 db데이터를 모두 불러와 주고,

![1530600694313](C:\Users\student\AppData\Local\Temp\1530600694313.png)

views index파일에서 db table 데이터 하나씩 도는 반복문으로 보여준당

![1530600456683](C:\Users\student\AppData\Local\Temp\1530600456683.png)







그럼 씨드에 하나의 데이터를 넣어봐서 해봤으니 

**이제 15개 카드를 모두 보여주자**

*db데이터 날릴려면 `db :drop`  -> `db :migrate` (-> `db :seed`  씨드도 migrate 넣어줘야 한다) 

![1530606118453](C:\Users\student\AppData\Local\Temp\1530606118453.png)







---

#### show 페이지를 만들어서 '평가하기' 기능 / 평점 & 후기 등록 기능을 만들어 주자



![1530602921971](C:\Users\student\AppData\Local\Temp\1530602921971.png)

**평가하기 버튼 누르면 show페이지로 넘어가게 만들었다**

![1530606173274](C:\Users\student\AppData\Local\Temp\1530606173274.png)





**Review db파일을 만들어서 score로(Review의 column 요소)  별점주기 기능을 넣어보자**
*필요한 column들 (자료형) ;  **score (int)** / **content (string)** / **movie_id (int)**

`rails g model Review content score:integer movie_id:integer`



- 평가는 라디오 버튼을 이용해보자 (5점 만점)

  ('radio html' 구글링 ㄱㄱ ㅎㅎ)

  ```html
  <form>
      평점 <input type="radio" name="score" value="1">1
      <input type="radio" name="score" value="2">2
      <input type="radio" name="score" value="3">3
      <input type="radio" name="score" value="4">4
      <input type="radio" name="score" value="5">5 <br>
      리뷰 <input type="text" name="content">
      <input type="submit">
  </form>
  ```

![1530603111665](C:\Users\student\AppData\Local\Temp\1530603111665.png)





**db표들 관계 (1:N)  설정**해주지 않고 (rails에게 알려주지 않고) 그냥 show페이지에 출력하려고 하면

![1530603873975](C:\Users\student\AppData\Local\Temp\1530603873975.png)

![1530603844141](C:\Users\student\AppData\Local\Temp\1530603844141.png)

이런 에러가 나온다 ㅋㅋ



**db끼리 관계를 말해주자 :**    (`belongs_to`  /  `has many`)

![1530604078169](C:\Users\student\AppData\Local\Temp\1530604078169.png)

![1530603974867](C:\Users\student\AppData\Local\Temp\1530603974867.png)





#### 평점 평균을 내는 코드를 추가하자.

![1530604254582](C:\Users\student\AppData\Local\Temp\1530604254582.png)

근데 이렇게 하면  평균점수 avg가 정수만 나온당...(버림되어서)

==> 하나에만 `.to_f`을 붙여주면 float로 인식한다 ==> 몫도 실수로 해준당



![1530604572785](C:\Users\student\AppData\Local\Temp\1530604572785.png)



`.round(#)` :  실수값을 소수점 #자리까지만 보여준당

![1530604544825](C:\Users\student\AppData\Local\Temp\1530604544825.png)







*cf.*

**back-end 개발자** (서버, db쪽)

**front-end 개발자** (웹페이지, 자바스크립트)