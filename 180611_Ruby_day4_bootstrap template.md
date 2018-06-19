#### cf. https://c9.io/djohnkang :  강동주 이사님 c9

#### cf. c9.io/kitty4089   : 내 c9  (비번은 특문2개 + 1 바로 앞 알파벳 대문자 + 끝 내 휴대폰번호 뒷자리)



---

## 1. 지난시간 복습

![1528679612712](C:\Users\student\AppData\Local\Temp\1528679612712.png)

- c9 : 우분투 리눅스Linux 쓰고 있음. 프로젝트 만들 때 blank로 하는 거. 루비가 이미 깔려 있음. 

  - 리눅스가 os의 하나인데

    리눅스 중에서도 종류가 어어어어어어어엄청 많음. 리눅스 오픈소스다 보니까.. 

    우분투, redhat계열 등등등...

  - 다른 gem들은 그 때그때 항상 깔아줘야함. 시작할 때마다 새로운 컴퓨터니까.

- 시나트라 약속 : index.erb / 그 외 여러가지 웹페이지들  -  **views폴더** 안에 넣어져 있어야 한다.

- 서버 켤 때 :  `ruby app.rb -p $PORT -o $IP`   써준다.

  : 루비야 app.rb라는 파일좀 열어줄래? 근데 열 때 저 **포트**와 저 **아이피**를 사용해서 열어줘

  -p  : 포트  :  $PORT - 지정된 포트로 열게
  -o  : 오픈(open)  : $IP - 애도 지정된 ip로 열게

  cf. -p $PORT는 안해도 사실 돌아가요.

  cf. $IP는 0.0.0.0        ( => $IP가 변수임)

- `params[내가 넣었던 해쉬 이름표]`   => 근데 이름표를 " " 스트링으로 넣는 게 아니고 :이름표

  - 내가 넣은 해쉬 불러오는 명령어
  - ex. `params[:name]`

- `puts` 명령어는 웹페이지에 출력해주는 게 아니고 **밑에 콘솔창**에 출력해 주는 명령어다.



## 2. 위 복습예제를 응용해 '방명록'을 만들어 보자

-----------------------

##### 관계있는 c9 프로젝트/파일들

1) 프로젝트 : whatyourname

-------------------------------------------

=> name 이란 변수에 저장했던 것을 name이란 배열에 저장해 보자.

1. names란 배열 만들기 :

   - `names =[]`
   - 밑에 콘솔창에 입력할 것.

2. `배열이름.push`  : 배열에 넣어주는 명령어

   cf. c의 경우에는 내가 0번째에 넣겠다고 말을 꼭 해 줘야 함... .[0] = 이런 식으로

   `names[0]` 내가 다음 값 넣을 때 몇 번째까지 넣었었는지 (index값) 까먹으면 문제. 불편.

   => 이미 넣어져 있는 배열 순서에 넣으면 오류가 안뜨고 그냥 override됨.

   - `names.push("예림")`

     :  계속 뒤로 배열에 넣어준다. 하나씩 쌓아줌. 자동으로 가장 마지막으로 넣어졌던 값 다음 순서로.



* 그냥 배열을 불러오면 계속 배열에 값이 쌓이는 게 아니고 그 때그때 새로 첫번째 숫자가 불러와짐.

  => 배열은 메모리에 저장되는 거라서

  - 입력값을 파일로 만들어서 저장한다.

    : 전에 파일 이름 한번에 바꾸고 했던 코드 응용

    0)파일File 쓸 때는 대문자로 쓴다. `File ~ `

    1) 파일을 연다 `File.open("list.txt", "a+")`

    ###### * 내가 연 메모장에 -> w : write 쓸거야, w+ : 파일에 데이터가 쌓이는 게 아니고 똑같은 파일명이 있어도 쓰기가 되는(덮어쓰기)    r : read,   a : append 수정하겠다 ,  a+ : 수정하면서 계속 같은 파일에 쓰겠다 뭐 그런 의미

    ###### * file open modes / file open ruby write 이런 식으로 구글링~

    ###### * ruby random number 구글링 :  루비에서 랜덤넘버 겟하는 방법

    - `rand(0..10)`

      맞는지 콘솔창에서 테스트 해본다.  =>` irb` -> `해당 명령어`   ---->  나올 때는` exit`

    - ![1528683999181](C:\Users\student\AppData\Local\Temp\1528683999181.png)

#### 컴퓨터에 2개의 저장공간이 있다.

1. memory  : 휘발성. 컴 끄는 순간 다 날라감
   - 매번 부를 때마다 새로 reset됨
   - 배열은 메모리에 저장되는 것
2. DISK : 저장이 됨. 반영구적 저장소.
   - 파일 형태로 저장해야함



## 3. 그대로 사랑의 큐피드 낚시 웹사이트를 만들자 

#### => 입력한 이름들을 파일로 영구저장

------------------------------

##### 관계있는 c9 프로젝트/파일들

1) 프로젝트 : whatyourname

 - 그 안에 관계있는 파일 
   - app.rb
   - index.erb
   - hello2.erb
   - admin.erb

---------------------------------------------------------------------------------------------------------------------------

- 1) File.open("lovers.txt", "r") 해서 파일을 연다.

  2) 한 줄씩 보여준다. (우리가 한 줄씩 저장했으니까)

  ​	: 구글링 '*ruby each line*'   => 메모장 파일에 저장된 내용 한 줄씩 출력해주는 명령어 검색

  - 콘솔창에서 확인

  ![1528684578949](C:\Users\student\AppData\Local\Temp\1528684578949.png)

- <% =   %> : 루비코드 넣을 수 있는. erb에서.   

  - = : puts와 같은 의미

    - 웹페이지 상에 출력해야 하는 것에는 =를 붙여줘라!!

    - 출력 필요 없는 실행 코드는 =를 붙이지 말고 <% %> 이 안에다 실행 코드만 입력

      <!DOCTYPE html>
      <html>
          <head>
              <title>낚인 놈들</title>
              <meta charset="utf-8">
          </head>
          <body>
              <div>
                  <a href="/">홈으로</a>
              </div>
              <div>
                 <h1>낚인 놈들</h1>
                 <%@file.each_line do |line| %>     <!--line변수에 저장-->
                 <%=line%> <!--line 임시변수 출력-->
                 <%end%>
              </div>
          </body>
      </html>

  

## 4. asked 같은 서비스 만들기

#### => 익명질문앱  'asked'

---

##### 관계있는 c9 프로젝트/파일들

1) 프로젝트 : asked

------





cf. html에서 input 크기 늘리기 :  input type text attribute/ height 등 구글링.

​	=> 근데 이렇게 하지 말고 그냥 bootstrap 통해서 이쁘게 할 수 있음



#### cf. 스트링 쓰는 법 2가지

1. 컨캐터네이션 :   

   - "AB" + "CD" = "ABCD"

   => 근데 `"내이름" + name + "입니다"` 가 불편하니까

   ​     "내 이름은 xx입니다"  xx부분에 루비코드를 써서 변수를 쓰면 간단할 것이다 => 인터폴레이션 방법

2. 인터폴레이션 (수술) : 

`#{루비코드}` 이렇게 쓴다

**=> 그러니까 ㅋㅋ**

1. 루비코드 안에서 특정 스트링 안에 루비코드(변수나 식같은거) 넣는 거는 `#{ }`
2. erb 문서 안에서 루비코드 쓸 때는 `<%  %>` 





## 5. 문서에서 it이 몇 개인지 알아보기 :  함수정의하기 def

https://gist.github.com/djohnkang/5d8e7001846e9ba01aa9f55e13021832

: **디킨스의 '두 도시 이야기'** - 대구법 활용된. 반페이지를 대구만 써서 해서 똑같은 글자가 엄청 많음.

- word frequency counter

- 펠링드롬 palindrome question  :   소주 만병만 주소

  앞 뒤가 똑같은 번호같은 문장

  니애미추미애니

  - 'English Palindrome'  구글링 ㄱㄱ

###### cf. 다른 언어에서는 ? 못쓰는데 루비에서는 ?써도 된다. 변수이름이나 함수이름이나 등등 ㅎㅎ`

- `.reverse` :   뒤집어 주는 명령어![1528695039994](C:\Users\student\AppData\Local\Temp\1528695039994.png)

- word1 = "asdfdsa"                 #palindrome
  word2 = "asdfghj"                   #palindrome X
  word3 = "소주만병만주소"       #palindrome

  #펠링드롬이면 True 나타내주고    :  그대로 상태 = 뒤집은 상태
          # 뒤집으려면 str.reverse 해주면 된다. 스트링을 뒤집을 수도. 배열을 뒤집을 수도

  #펠링드롬 아니면 False 나타나는 코드

  def is_pal?(str)   #입력값 -> 임의의 문자 : string
          #출력값 -> bool (palindrom?) 불리언값 T/F   : return 펠링드롬인지 아닌지
      if str == str.reverse   #str이 palingdrome이라면
          return true
      else
          return false
      end
  end

  

  puts is_pal?(word1)
  puts is_pal?(word2)
  puts is_pal?(word3)

- 실행은 밑에 콘솔창에

  `ruby pal.rb`

  cf. 현재 위치에 잘 저 파일이 있는지 확인하려면 먼저 `ls`

  ![1528695429150](C:\Users\student\AppData\Local\Temp\1528695429150.png)

- `.downcase` :  입력된 대문자를 소문자로 바꿔주는 명령어

- `!` : 원래 있던 자료 자체를 바꿔주는 명령어!!! 원본 자료를 수정할 수 있음

  #입력값은 하나의 문자열이 아니라 배열 ["A", "B", "C", "D"]

  #출력값은 ["a", "b", "c", "d"]

  words = ["A", "B", "C", "D"]

  def downcaser(arr)    #arr : array (변수다 내가 지정한)
      # 1. 배열을 하나씩 돌면서
      # 2. 각각을 .downcase를 통해 소문자로 만든다.
      arr.each do |x|
          x.downcase!
      end
      return arr #전부다 소문자로 만든 배열을 리턴
  end

  puts downcaser(words)  # ["a", "b", "c", "d"]

  

cf. `.methods`  :  .앞에 있는 애한테 쓸 수 있는 모든 .XX를 보여줌

​    `.methods.sort`   : 알파벳 순서로 보여줌

하이 예림 족발 먹으러 갈래?? 

아니 가자 그냥 따라와 

잔소리 하지 말고

알겠어??!!!!!

그럼

이만

수고



- `text.split(" ")`  text에 들어간 글자들을 빈 칸(띄어쓰기) 마다 다 분리해서 배열에 넣어주는 명령어

  text = "It was the best of times, it was the worst of times, it was the age of wisdom, it was the age of foolishness, it was the epoch of belief, it was the epoch of incredulity, it was the season of Light, it was the season of Darkness, it was the spring of hope, it was the winter of despair, we had everything before us, we had nothing before us, we were all going direct to Heaven, we were all going direct the other way--in short, the period was so far like the present period, that some of its noisiest authorities insisted on its being received, for good or for evil, in the superlative degree of comparison only."

  words = text.split(" ")
  #.split  :  문단을 빈칸(띄어쓰기) 단위로 쪼개서 배열에 담아줌

  words.each do |word|
      word.downcase!
  end

  #puts words


  count = 0
      #한 번씩 돌면서 만약 해당 요소가
      #"it"인 경우는 count를 하나 올려준다.
          
  words.each do |word|
      #만약 word가 it과 같다면 count를 하나 올려준다.
      if word == "it"
          count+=1
      end
  end

  puts count



- 콘솔창에서도 단어(파일명같은거) 어느 정도(한 두글자) 쓴 다음`tab키` 누르면 자동완성된다



## 그럼 이번엔 모든 글자에 대해 

## 어떤 단어가 몇 번씩 나오는 지 알아보자

* **배열 / 해쉬 만드는 2가지 방법**

1. arr = []   #배열을 만들 때는 [] 대괄호로

   h = {}  #해쉬를 만들 때는 {} 중괄호로

2. **method이용 방법**

   arr = Array.new   : 배열을 새로 만들겠다

   h = Hash.new  : 해쉬를 새로 만들겠다 

   cf. 출력해보면 hash만 {} 이렇게 출력되는 걸 볼 수 있다.  array를 출력하면 아무것도 안뜨는데 빈 배열은 출력이 안되기 때문.

   - arr = Array.new(10)  :   빈칸 10개(배열 크기)가 있는 배열을 만들겠다.
   - h = Hash.new(원하는 초기값)   :  초기값 - 내가 붙인 이름표 안에 넣을 초기값

* `.class` :  .앞에 것이 어떤 것인지 알려주는 method(명령어)

  ex.  h.class / arr.class :  각각 Hash / Array 가 나옴

###### cf. 해쉬는 순서가 없어요. 배열은 순서 있잖아요? ㅎㅎ





## 7. bootstrap template으로  홈페이지 예쁘게 만들기

### ; 부트스트랩 framework 사용

구글링 'bootstratp template' ->  첫번째 or 두번째 https://startbootstrap.com/template-categories/all/

https://startbootstrap.com/

-> 우리는 Agency를 골라보았다 -> 클릭으로 들어가서 Download - > 다운된 압출폴더 압축풀기 -> 파일 중에 index.html 눌러서 홈페이지 템플릿 확인

![1528702463482](C:\Users\student\AppData\Local\Temp\1528702463482.png)

https://startbootstrap.com/template-overviews/agency/



-> 압축 풀었던 폴더를 project폴더 안에 'hompage' 라고 이름 바꿔서 넣어줍니다.

-> git bash를 열어줍니다 (커맨드창, *windows키 -> git bash 검색*)

->project폴더로 디렉토리를 이동합니다

​	: `ls`를 이용해서 현재 디렉토리 확인 -> `cd 폴더이름` 이용해서 그 디렉토리로 이동

![1528703128645](C:\Users\student\AppData\Local\Temp\1528703128645.png)

빨간부분대로 친다 ㅎㅎ

->  현재 폴더를 코드 에디터(visual studio)로 열어줍니다.

​	:  현재 폴더 :  `code .` 입력  => `code`치고 `띄어쓰기` 그리고 `.`

​		(cf. `w` : 지금있는 working directory를 출력해줌)

-> 아래와 같이 visual studio가 켜지면, index.html 목록에서 선택![1528702897709](C:\Users\student\AppData\Local\Temp\1528702897709.png)



-> title부분에 *'예림이의 홈페이지'* 로 바꿔줍니다.

-> 다른 부분도 원하는대로 바꿔줍니다/////

​	:  index.html 파일 열어서 계속 **웹페이지에서 해당 부분 우클릭 -> 검사** 로 바꿔야할 부분 봐가면서 

  - 참고로 영어 추천.  한글은 쓰면 기본 폰트가 궁서체로 돼 있음..

    

##### icon아이콘 바꾸기

- https://fontawesome.com/

  : 아이콘 공짜 사이트. 

- https://www.w3schools.com/icons/fontawesome_icons_webapp.asp

  : 부트스트랩 쓰면 아이콘 다 무료로 쓸 수 있어용

  =>  visula studio에 떠 있는 index.html파일 코드에서 `fa-shopping-cart`  찾아서(검색 : ctrl + F) `fa-`뒤에 원하는 아이콘 이름으로 바꿔줍니다.

  ex. `fa-desktop`

  

##### 사진 바꾸기

* 쓰인 이미지들은 압축푼 폴더 안에 img -> portfolio 안에 들어있다.
* 웹페이지상 해당 사진 우클릭 -> 검사 ->  해당 사진의 코드상 위치와 파일명 알아둔 다음 - > portfolio 폴더에서 그 사진파일 찾아서 이름 복사(ctrl + c)->  폴더에서 원래 사진파일 삭제 -> 내가 넣을 사진 다운받아서 원래 사진 이름으로 바꿔준다.



##### 필요 없는 부분 없애기

해당 부분 웹페이지에서 우클릭 -> 검사 -> visual studio 코드에서 해당 부분 코드 다 없애기



##### **이런식으로 해당부분 아이콘/링크/사진/내용 등을 바꿔줍니다.

##### 트위터 아이콘 링크를 내 인스타그램 링크로 바꾸기

=> 'twitter' 검색으로 찾기 -> 아이콘을 instagram으로 바꾸기  (fa-instagram 하면 나오더라)

-> 이 아이콘 이미지 있던 코드 바로 윗줄 <a href> 태그의 주소를 내 인스타 주소로 바꿔준다.





#### 이제 이거 github에 올리기  => 내일 합시다.

## 7-1 우선 c9에 올립시다.

1. yerim_homepage 프로젝트 만든다 (HTML5로 만들것!)
2. ??? 이것도 쌤쪽에서 프로젝트가 더 안만들어지니 내일 합시다.





---

cf. **atlassian**  jira라는 회사가 쓰는 SW만드는 회사  10조원 규모 회사. 호주에서 제일 큰 회사

**trello**  우리 협업할 때 쓸 거. 이거 인수했대 



-----------------

*cf. Computational Thinking : 단계별 사고*

https://youtu.be/kJEHOpWZeC4

; 유투브 영상 - 스티브 잡스 "프로그래밍을 왜 배워야 할까?" (30년 전 영상)

###### *=> teach you how to think in a certain way*

- 스티브 잡스 대단한 것이  2번 시대를 열었다 : personal com / mobile

- cf. 스티브 워즈니악(짧게 woz라고 함) :   개천재 / apple 같이 만들었다

- 맨 처음 만들었던 게 **'블루박스'** : 세계 어디서든지 공짜로 통화할 수 있는 

  - 통화 **연결음** 분석해보니까 연결음 자체가 어디로 연결해 줄지 알려주는 것이더라. 

    => 통화 연결음을 속여서(해킹해서) 어디든지 공짜로 전화 걸 수 있는 걸 만듦.

  - 지금 스카이프 같은 거 만든거임

  - 첫 성공 작품

---

