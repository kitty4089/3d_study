https://github.com/5chang2

https://github.com/5chang2/kakao_bot_sample :  밑에 README.md 에 카카오톡 api 플러스 친구에 대한 설명



######  웹페이지 예쁘게 꾸미는 이유 :

구조화. 시각적으로 더 보기 편하게 보이도록



스캣폴딩?

스캐폴드  뭐 어제 했대.. 나 인사이드 3d 킨텍스 간 날.



### 카톡 챗봇 ex.

ex. **알려줘전북대** - 나름 자연어 처리 돼있는건가아아아  자연어 처리



ex. 오창희 강사님도 어느정도 자연어 처리된 서비스를 해봤었다 (이건 페북인듯..? 카톡아닌듯?)

**fluenty** :  챗봇에서 자연어처리 쉽게 연동시켜 주는 서비스(스타트업). 지금은 삼성전자에 이 스타트업이 인수된 상태라서 서비스 쓸 수 없음. 

**=> 차선책 : IBM  Watson** .   이 정도는 자연어 처리를 해 줘야 사람들이 좀 쓸 수 있는 챗봇이 되는 것.

- 특히 좀 지나면 사람들이 욕을 쓰기 때문에 . 욕을 썼을 때도 대응할 방법도 처리 해줘야..
- 완전히 일상 대화 하듯이 구현 될 게 아니면(사용자가 이용법도 알기 힘든채로 막연한 질문/문장들을 써야 하므로) 
  - 아예 필요한 기능들, 구현된 기능들을 버튼(키워드 기반)으로 입력 가능하도록 처리하는게 맞는 것임..



ex. **라이언봇 - 개발일지**

​	사람들이 썼던 데이터들 가져와서 그에 따라 대답하도록 한 것. ai 형태는 아니고..





---

## 카카오톡 챗봇 api와 레일즈 연결하기

**(c9 프로젝트 :  'kakao_bot_yr'  (6월 29일))**



- 레일즈에서 json 렌더링을 지원함.  

  - url 뒤에  `.json` 붙이면 json 페이지를 보여준다.

  - (렌더링 방식이 여러 가지 돼 있는 경우가 있기 때문에. json만 렌더했으면 .json 안해도 json으로 보일 것)

    ex. 렌더 방식을 html도 했고 json도 했으면  .json으로 했을 경우 json형식 페이지를 보여줄 것이다.

    말하자면, 아래와 같이 쓰면 된다는 의미. 

    ![1530252309706](C:\Users\student\AppData\Local\Temp\1530252309706.png)

    json렌더된 페이지가 보이는 모습



### 이제  진짜로 카톡 챗봇 만들기 start!!

![1530234978677](C:\Users\student\AppData\Local\Temp\1530234978677.png)



![1530234990620](C:\Users\student\AppData\Local\Temp\1530234990620.png)



- 혹은. 깃헙에 카카오가 똑같이 README파일로 올려놨다

  'github 카카오 플러스 친구'  구글링 ㄱㄱ

  https://github.com/plusfriend/auto_reply

  ![1530235064574](C:\Users\student\AppData\Local\Temp\1530235064574.png)

  **Home Keyboard API** :  유일하게 꼭 필수로 가지고 있어야 할 응답 중의 하나.

![1530235124646](C:\Users\student\AppData\Local\Temp\1530235124646.png)

- get방식으로
- url은 너의 서버 url  뒤에 /keyboard 붙이면 된다



1. `rails g controller home keyboard`

2.  루비에서는 직접적으로 제이슨을 지원하진 않음

   - 해쉬로 바꾼후
   - 렌더링할 때 json으로 렌더링해서 보내는

   방법을 쓴다

![1530235367147](C:\Users\student\AppData\Local\Temp\1530235367147.png)

![1530235937449](C:\Users\student\AppData\Local\Temp\1530235937449.png)

(해쉬를 @keyboard 변수에 넣었고, json을 해쉬문법형태로만 바꿔주고.  render를 json으로 해주겠다 코드 추가.)



3. keyboard오브젝트 설명을 본다

   ![1530235633421](C:\Users\student\AppData\Local\Temp\1530235633421.png)

   ![1530235642851](C:\Users\student\AppData\Local\Temp\1530235642851.png)







### api 해석법

![1530236044550](C:\Users\student\AppData\Local\Temp\1530236044550.png)

1. 어떤 방식으로

2. url

3. 이 부분에 파라미터가 들어가는 경우가 있음

4. 가장 증요한 건 어떻게 Response(응답)해야하는가! 

   - 실제 action으로 들어갈 부분. 

   - ex. kakao api 에서 keyboard.  자료형 타입은  keyboard라는 게 없는데 keyboard라는 게 뭐지? 

     ==> 카카오가 object 정의 해놨음

     ![1530236164580](C:\Users\student\AppData\Local\Temp\1530236164580.png)

     (keyboard라고 돼있는 설명 클릭 ->  설명 보면 아는 얘기가 나옴. 모르겠으면 또 밑의 예시 보고 참고)



![1530236302234](C:\Users\student\AppData\Local\Temp\1530236302234.png)



서버 켜서 json 렌더링된 모습 확인

![1530236798006](C:\Users\student\AppData\Local\Temp\1530236798006.png)



저 url에 뒤에 /keyboard 빼고 플친 관리자센터 api형에 넣는다

![1530236364578](C:\Users\student\AppData\Local\Temp\1530236364578.png)

![1530236570617](C:\Users\student\AppData\Local\Temp\1530236570617.png)

시작하기 눌러 아래와 같이 되도록

![1530236602221](C:\Users\student\AppData\Local\Temp\1530236602221.png)



그 다음 공개를 해준다.

![1530236622553](C:\Users\student\AppData\Local\Temp\1530236622553.png)

![1530236400126](C:\Users\student\AppData\Local\Temp\1530236400126.png)



-> 그 다음 핸드폰을 들고 플친을 검색해본다

![1530244046229](C:\Users\student\AppData\Local\Temp\1530244046229.png)

![1530244055347](C:\Users\student\AppData\Local\Temp\1530244055347.png)

![1530244063565](C:\Users\student\AppData\Local\Temp\1530244063565.png)



ㅎㅎ 옵션 3가지가 뜨는 것까지 확인되면 잘 한 것이당당당













---

**여기까지 5.1 까지 완성**

![1530236695607](C:\Users\student\AppData\Local\Temp\1530236695607.png)



**5.2시작**  >>>> 



![1530236744055](C:\Users\student\AppData\Local\Temp\1530236744055.png)



액션정의

![1530236835114](C:\Users\student\AppData\Local\Temp\1530236835114.png)



-> message는 뭔지 보자 Object

![1530237719221](C:\Users\student\AppData\Local\Temp\1530237719221.png)



-> 3가지 message필드 중 필요한 것들 정의  (아래 빨간네모 안에 작은 빨간 네모 부분이 message 오브젝트의 text 필드 하나 정의해준 것)

(*keyboard나 message나 json. 즉, 각각을 해쉬처럼 쓰는 거인듯)

![1530238224576](C:\Users\student\AppData\Local\Temp\1530238224576.png)



-> 카톡 플친에서 테스트를 해보자. (에러가 뜰 것이다)

![1530238742958](C:\Users\student\AppData\Local\Temp\1530238742958.png)

> 우리는 우리의 서버가 아니라 api서버를 이용할 것이기 때문에(외부에서 요청하는 것이라서 어차피 csrf 공격같이 외부 접근임..)  해당 서비스를 주석처리 해줄 것

![1530238563116](C:\Users\student\AppData\Local\Temp\1530238563116.png)



-> 이제 다시 카톡 플친에서 작동 잘 되나 확인.

![1530238797182](C:\Users\student\AppData\Local\Temp\1530238797182.png)

- 이렇게 되면 잘된 것. 지금은 메아리치는 챗봇이당. 

  ![1530239168234](C:\Users\student\AppData\Local\Temp\1530239168234.png)

  이 코드 때문에 메아리 치는 거당 ㅎㅎㅎㅎ

##### cf. 

- 대괄호 [ ] :  배열
- 중괄호 { } :  해쉬
  - 해쉬 안에 해쉬 그 안에 해쉬  이런 다중구조 가능하당





#### thecatapi.com

랜덤으로 계속 새로고침 할 때마다 고양이 사진 나오는 api

![1530239987166](C:\Users\student\AppData\Local\Temp\1530239987166.png)

![1530240013069](C:\Users\student\AppData\Local\Temp\1530240013069.png)

![1530240042222](C:\Users\student\AppData\Local\Temp\1530240042222.png)

==> cat api의 20개 랜덤 사진 이미지에 대한 예시 코드



##### 카카오톡 api는 gif 지원 안함.

- 강제적으로 jpg만 받겠다 처리 해줘야 함

![1530240097576](C:\Users\student\AppData\Local\Temp\1530240097576.png)

===> cf.   ?전까지가 url    그 뒤는 요청할 때 parameter값들



저 url 그대로 복사해 와서 result_per_page 부분 지워 -> **type=jpg** 로 바꿀 것

(이 서비스에서 사진들은 tumblr에서 가져오는 것)

![1530240282919](C:\Users\student\AppData\Local\Temp\1530240282919.png)



-> '로또' / '점심메뉴' / '고양이'  등을 조건문으로 코드 지정해줌

![1530243411386](C:\Users\student\AppData\Local\Temp\1530243411386.png)

```Ruby
def message
    @user_msg = params[:content]     # 임베디드루비에서 (다른 파일에서)쓸 때만 @붙여 변수 쓴다
    @return_msg = "기본메세지"   #변수 초기값 설정(없어도 되긴 함)
    @url ="http://thecatapi.com/api/images/get?format=xml&type=jpg"
    
    #'로또' if문
    if @user_msg == "로또"
      @return_msg = (1..45).to_a.sample(6).sort.to_s  #array로 바꿔주고 6개 뽑아서 순서대로 정리 
                # 마지막으로 배열은 지원안하므로 스트링으로 바꿔줘야 함
     elsif @user_msg == "점심메뉴"
      @return_msg = ["20층", "만두", "김밥", "국밥", "부찌", "냉면", "메밀국수", "연어회", "치킨", "파전", "엄초시와 막걸리", "양꼬치"].sample
            #뒤에 .sample 만 붙이면 딱 배열 요소 스트링만 뽑아줌. 
            #.sample(1) 이런식으로 뽑을 개수를 같이 적어주면 한 항목을 가진 배열로 return해 주므로 
            #꼭 다시 .to_s 달아줘야함을 유의 (카톡 api가 스트링 return만 지원하기 때문)
    end
    
    @basic_keyboard = {
      :type => "buttons",       # [해쉬로 바꾸는 방법1] 심볼 + 로켓
      :buttons => ["로또", "점심메뉴", "고양이"]
    }
    
    @basic_msg = {
      :text => @return_msg
    }
    
    result = {          # hash 만들어줌/  우리 해쉬 안에 해쉬를 넣어줄 것이당
      :message => @basic_msg,
      :keyboard => @basic_keyboard    #시각적 간소화를 위해 밖에 쓸 해쉬를 만들어준 후 변수로 사용했다
    }
    
    render json: result     # result해쉬는 최종적으로 결과를 넣어줄 해쉬.
  end
```



->  'restclient' 라는 것을 쓸 것이다  (gem)

- 궁금하면 'restclient gem' 구글링 ㄱㄱ

  https://github.com/rest-client/rest-client

  - httparty와 거의 흡사. (웹페이지에 필요 정보만 id값 따서 값 따던 )크롤링할 때 썼던. 
    - 외부로 서버 요청을 보낼 때

![1530245025814](C:\Users\student\AppData\Local\Temp\1530245025814.png)

Gemfile에 추가 (사실 루비는 Gemfile로 gem들을 다 관리하고, 위에 `require 'restclient' `는 안해도 된다. =>그냥 쓰지 말고 없애)

![1530245082833](C:\Users\student\AppData\Local\Temp\1530245082833.png)

bash창에 `bundle ` 로 새로 깐 gem들도 깔아줘요 (서버 끄고 ㅎㅎ)



->  rest client gem 에 따라서 elsif 로 "고양이" 기능 정의

![1530245358685](C:\Users\student\AppData\Local\Temp\1530245358685.png)

![1530245836963](C:\Users\student\AppData\Local\Temp\1530245836963.png)

위와 같이 catapi 를 보면 xml 형태로 페이지를 받아오므로. 우리 코드를 수정해준다.

![1530245411314](C:\Users\student\AppData\Local\Temp\1530245411314.png)

![1530245592704](C:\Users\student\AppData\Local\Temp\1530245592704.png)



nokogiri도 사용법 알려면

'nokogiri gem' 구글링 ㄱㄱ

![1530245443812](C:\Users\student\AppData\Local\Temp\1530245443812.png)



![1530246887815](C:\Users\student\AppData\Local\Temp\1530246887815.png)

http://www.nokogiri.org/tutorials/searching_a_xml_html_document.html#single_results

![1530246864896](C:\Users\student\AppData\Local\Temp\1530246864896.png)

![1530246925451](C:\Users\student\AppData\Local\Temp\1530246925451.png)

우리는 xml문서에서 parsing (태그 크롤링) 할 거니까 이 부분 참고하면 됩니다

---

**cf. html / xml / json  이런 거 다 문서 형태임.    **

​	- ex. **json형태의 웹페이지 문서는 해쉬같이 생긴 구조를 보여주는 페이지인 것**

---



그럼 다시 catapi에서의 코드를 보자

![1530247008438](C:\Users\student\AppData\Local\Temp\1530247008438.png)

우리는 이 <url> 태그로 둘러 싸인 url을 가져와서 이미지를 보여줄 거잖니

이것을 nokogiri가 해준다는 것. 저 부분 parsing을 위해서는 xpath를 쓴다는 것. 그게 위에 nokogiri구글링한 부분.

![1530247098791](C:\Users\student\AppData\Local\Temp\1530247098791.png)

```Ruby
    elsif @user_msg == "고양이"
      @cat_xml = RestClient.get(@url)
      @cat_doc = Nokogiri::XML(@cat_xml)   #parsing(xml문서를 그대로 가져오는)했습니당. xml로 받은 요청을 노코기리가 쉽게 파싱할 수 있게 구조를 잡아줍니다.
      @cat_url = @cat_doc.xpath("//url").text #.text가 xml문서 원본코드에 있던 url 부분에서 좌우의 태그들은 지워주고 그 사이 text url만 가져와 준다.
```

- `.text`가 xml문서 원본코드에 있던 url 부분에서 좌우의 태그<url> </url>들은 지워주고 그 사이 text url만 가져와 준다.



포토를 보여줄 부분 해쉬(제이슨)를 정의해준다

![1530247493945](C:\Users\student\AppData\Local\Temp\1530247493945.png)

```ruby
 @photo_msg = {
      :text => "나만 고양이 없엉 :(",
      :photo => {     
        :url => @cat_url,
        :width => 720,
        :height => 630    #카톡 api 6.3 photo  부분에 3개 모두 required라고 돼있으므로 반드시 3개 다 있어야함.
        }
    }
```

- 카톡 api에 필드명 (해쉬의 key) / 우측 value에는 카톡api에(6.2) 해당 필드명 옆 타입을 지켜줘야 함(string/photo 등으로 써 있는)

  ![1530247627854](C:\Users\student\AppData\Local\Temp\1530247627854.png)

  그럼 여기서 photo 타입이라는 건 뭐지?

  밑에 스크롤을 더 내려보면!

  ![1530247686083](C:\Users\student\AppData\Local\Temp\1530247686083.png)

  이렇게 써 있다. 이 부분이

  ```ruby
  #카톡 api 6.3 photo  부분에 3개 모두 required라고 돼있으므로 반드시 3개 다 있어야함.
  ```

  이 설명이다.

  



result 보여줄 때, "고양이" 필드에서는 **사진(photo)**이 들어가므로

if 문으로 나누어 준다.

![1530247185757](C:\Users\student\AppData\Local\Temp\1530247185757.png)





---

cf. **The Power of Kawaii 실제 논문**  == >  귀여운 것을 보면 학습능력이 올라간다. 집중도가 올라간다.

---









---

## c9 에서 코드를 짰는데 카카오톡 플친에서 볼 수 있는 이유

![1530248022616](C:\Users\student\AppData\Local\Temp\1530248022616.png)

여기서 내가 지정해 준 url 덕분.



실제 구동 시나리오 시뮬래이션 과정을 보자.

1. 유저가 고양이든 로또든 text를 보낼 거야

   - 이 보낸 값은 카카오톡 서버. 즉 정확히는 관리자센터 서버로 전송된다

     ![1530248130295](C:\Users\student\AppData\Local\Temp\1530248130295.png)

   - **==> 이런 정보들이 넘어간다**

     user_key는 사용자의 암호화된 id정보일 것이고 (나의 경우 kitty4089이런 거 암호화된 거겠지.)

     type에서는 내가 c9루비코드에서 짰던 text (고양이, 로또 , 점심메뉴) 이런 사용자가 입력한 정보

2. 관리자 서버에서는 내가 url을 c9으로 지정해줬던 것을 인식한다

   ![1530248309011](C:\Users\student\AppData\Local\Temp\1530248309011.png)

   ![1530248321719](C:\Users\student\AppData\Local\Temp\1530248321719.png)

   내가 여기서 지정해줬었음 ㅎㅎ

3. 그럼 저 사용자의 정보들은 내 c9서버로 이동해서 내 코드들을 실행하고 적당한 response (응답) 정보들을 return해서 다시 카카오톡(관리자센터)서버로 보내준다.

4. 카톡 관리자센터 서버가 사용자의 카톡창에 응답내용을 보내준다. 끝.

---





## 우리의 챗봇을 서버에 올리자

https://github.com/5chang2/kakao_bot_sample

지금까지 한 것을 서버를 돌려주는 애인 HEROKU에 올릴 거에요

![1530249059616](C:\Users\student\AppData\Local\Temp\1530249059616.png)

위의 단계 그대로 할 것이니 참고!!



---

1. 제일먼저 젬파일 수정을 해주세요 

   ![1530249106156](C:\Users\student\AppData\Local\Temp\1530249106156.png)

   없애고

   ![1530249142548](C:\Users\student\AppData\Local\Temp\1530249142548.png)

   3개를 추가해 준다.

   ```
   cf. 레일즈의 큰 3단계  :  각 단계에서만 필요한 gem들이 있다  
   
   1. development  - sqlite를 쓰고
   2. test 
   3. production(배포)  - 실제 배포 단계에서는 pg를 쓸 것이다라고 해준 것.
   ```

   

->  bash 콘솔 창에 `bundle`로 바뀐 gem들을 깔아준다



2. 그리고 `/config/database.yml`파일도 수정을 해주세요 

   ![1530249295897](C:\Users\student\AppData\Local\Temp\1530249295897.png)

   각 3단계 확인 가능

   -> 가장 마지막 production 부분 삭제

   ![1530249338004](C:\Users\student\AppData\Local\Temp\1530249338004.png)

   지우고 밑에 추가



3. 헤로쿠 가입 (HEROKU)

   ![1530249362356](C:\Users\student\AppData\Local\Temp\1530249362356.png)

   ![1530249371745](C:\Users\student\AppData\Local\Temp\1530249371745.png)

   

4. 이메일 인증 후, 로그인해서 들어간다. (로그인만 하고 작업은 c9에서 해줄 것이다)

5. c9  bash 창으로 와서 git repository 를 만들어주자

`git init`

`git add .`

`git commit - m "챗봇을 만들어보앙ㅆ다"`

`heroku login` -> 로그인 아이디/비번 입력

`heroku create "이름 입력"`   ==> 배포될 때 실제 url과 연관돼 있음. 앞부분 url 이름 정해주는 것

cf. heroku명령어는. 그냥 리눅스에는 없는 명령어지만. c9 에서는 기본적으로 설치를 해준 상태라 사용 가능한 것



###### 근데 이 다음 우리는 루비버전이 안맞아서인지 뭔지 에러가 났다

**------- 수업 잠정적 종료!  -----------**



> 해결됐다고 ㅇㅋㅋㅋㅋ

