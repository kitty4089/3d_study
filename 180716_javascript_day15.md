18 .07 .16

### 전태훈 강사님의 자바스크립트



: 페이지에서 동적인 모션에 쓰는 것들 

  (ex. 어떤 버튼을 누를 때마다 다시 자료를 끌어와서 계속 다른 것들을 보여주는)

![1531701879640](C:\Users\student\AppData\Local\Temp\1531701879640.png)





---

변수를 넣을 때는 그냥 해도 되긴 하지만 var을 넣고 선언하자.

`var b = "asd"`   자동으로 자료형이  스트링으로 된당



크롬창에서 `F12` 누르고 console창에 들어갈 수 있다

![1531700786585](C:\Users\student\AppData\Local\Temp\1531700786585.png)

콘솔창 클리어 :   `ctrl + L`



`var arr = [];`

가장 많이 보게 될 자료형 배열.



`typeof arr;`

자료형 뭐니?



`arr.push(2);`

`arr.push(1);`

가장 마지막 인덱스에 값이 들어감



인덱스 맨 앞에 넣고 싶으면

`arr.ushift(4);`



그냥 배열 print는 

arr  치고 enter치면 된다



`arr.pop();`

가장 마지막 요소 삭제됨

`arr.shift();`

가장 맨 앞 인덱스 요소(첫 요소) 제거(삭제)



오브젝트라는 자료형

`var obj1 = {};`

`obj1.key = "value1";`

루비에서의 해쉬와 비슷한 개념.

`var obj1 = {key1:"value"};`  이렇게 아예 해도 된다



```javascript
> arr = [1,2,3,4,5]

> for (var i=0; i<arr.length; i++){
    console.log(arr[i]);
}
---
    실행결과 >>>
VM264:2 1
VM264:2 2
VM264:2 3
VM264:2 4
VM264:2 5
```





**html / css / javascript** 

웹페이지를 구성하는 기본 3요소

탄단지처럼 ㅎㅎ





![1531702011107](C:\Users\student\AppData\Local\Temp\1531702011107.png)

- naver웹페이지 문서 가져오는 거
- 검색어 입력하게 해 주는 거

근데.. input창이 아예 저걸로 바뀌어서 그 뒤로 검색창 클릭이 안됨. ㄱ-

(실제 네이버 웹페이지가 바뀐 건 아니고 문서 가져와서 우리가 보기에만 바뀐 것.)





----

### 이벤트 추가

: 어느 특정 버튼에  동작을 추가해 주고 싶을 때





먼저 함수 하나 만들어요

```javascript
function sayHi() {

	alert('안녕 오랜만이야!')

}
```

그 다음 함수 호출하면

`sayHi()`

![1531702220428](C:\Users\student\AppData\Local\Temp\1531702220428.png)



![1531702283593](C:\Users\student\AppData\Local\Temp\1531702283593.png)

문서의 모든 a태그들을 불러오는 함수







![1531703790345](C:\Users\student\AppData\Local\Temp\1531703790345.png)

`document.getElementById('query');`

검색창에 접근. 검색창의 id는 query이다.

`search`



`search.id`

`search.name`

등으로 또 그 안의 요소에 접근

![1531703842004](C:\Users\student\AppData\Local\Temp\1531703842004.png)





#### 자바스크립트에 존재하는 이벤트들 종류 구글링 그때그때 검색

http://heavening.tistory.com/23

![1531703534812](C:\Users\student\AppData\Local\Temp\1531703534812.png)



`search.addEventListener('mouseover', function(){alert("안녕!")});`

==> 바로 함수를 정의할 수 있음

![1531703647308](C:\Users\student\AppData\Local\Temp\1531703647308.png)

**cf.*  undefined는 리턴된 값이 없다는 의미.

![1531703700284](C:\Users\student\AppData\Local\Temp\1531703700284.png)

검색창에 마우스 커서 올려 놓으면 이렇게 알람창이 뜬다!

(이벤트 추가했당)

==> 이벤트 추가하고 새로고침하면 안됨.



그럼 이제,

#### 모든 a태그에 이벤트 추가해보기

![1531704239938](C:\Users\student\AppData\Local\Temp\1531704239938.png)

![1531704202583](C:\Users\student\AppData\Local\Temp\1531704202583.png)





![1531704469883](C:\Users\student\AppData\Local\Temp\1531704469883.png)

![1531704597305](C:\Users\student\AppData\Local\Temp\1531704597305.png)

![1531704525550](C:\Users\student\AppData\Local\Temp\1531704525550.png)

![1531704656605](C:\Users\student\AppData\Local\Temp\1531704656605.png)

오타 수정..







* cf. **jquery**  :  자바스크립트 쉽게 사용하게 해주는 애





---

## 본격적 네이버맵 api 이용



![1531704699021](C:\Users\student\AppData\Local\Temp\1531704699021.png)

![1531704713765](C:\Users\student\AppData\Local\Temp\1531704713765.png)

![1531704943198](C:\Users\student\AppData\Local\Temp\1531704943198.png)

![1531705081455](C:\Users\student\AppData\Local\Temp\1531705081455.png)

c9프로젝트 :  navermap_api



![1531705101917](C:\Users\student\AppData\Local\Temp\1531705101917.png)



다시 c9으로

`rails g controller map index`



routes.rb파일에서

(config폴더 안에)

![1531705177938](C:\Users\student\AppData\Local\Temp\1531705177938.png)

루트로 바꿔



![1531705197662](C:\Users\student\AppData\Local\Temp\1531705197662.png)

루트가 map컨트롤러의 index 액션인 것을 확인 가능 (app기본 페이지 아니고.)

![1531705230015](C:\Users\student\AppData\Local\Temp\1531705230015.png)

원래 기본 화면... 



![1531705281113](C:\Users\student\AppData\Local\Temp\1531705281113.png)

이 코드 복사



![1531705299989](C:\Users\student\AppData\Local\Temp\1531705299989.png)

붙여넣기



![1531705320366](C:\Users\student\AppData\Local\Temp\1531705320366.png)

자동으로 들어가는 내 아이디



한 달인가 10만 건까지 무료.

그 이상이 되면 자동으로 api 사용 정지가 된다.. 그 이상 유료로, 상업적 용도로 사용하게 될 때는 naver에 신청해야 하고, 그 때는 이 clientId를 안보이게 처리한다든가 해야함.



![1531705457787](C:\Users\student\AppData\Local\Temp\1531705457787.png)

`F12` 눌러 검사로 들어간다  (이 때, 빨간색 에러 뜨면 오타나 뭐 잘못된 것 ㅎ)



![1531705493866](C:\Users\student\AppData\Local\Temp\1531705493866.png)

![1531705502026](C:\Users\student\AppData\Local\Temp\1531705502026.png)



![1531705516729](C:\Users\student\AppData\Local\Temp\1531705516729.png)

복사



![1531705582906](C:\Users\student\AppData\Local\Temp\1531705582906.png)

인덱스 페이지에 붙여넣기



![1531705639317](C:\Users\student\AppData\Local\Temp\1531705639317.png)

복사

![1531705708315](C:\Users\student\AppData\Local\Temp\1531705708315.png)

붙여넣기

![1531705722993](C:\Users\student\AppData\Local\Temp\1531705722993.png)



![1531706668248](C:\Users\student\AppData\Local\Temp\1531706668248.png)

(이렇게 마우스 hover했을 때 내려오는 것도 자바스크립트 >_<)

![1531706681312](C:\Users\student\AppData\Local\Temp\1531706681312.png)

![1531706690644](C:\Users\student\AppData\Local\Temp\1531706690644.png)

![1531706700985](C:\Users\student\AppData\Local\Temp\1531706700985.png)

![1531706716878](C:\Users\student\AppData\Local\Temp\1531706716878.png)

![1531706786461](C:\Users\student\AppData\Local\Temp\1531706786461.png)

![1531706913191](C:\Users\student\AppData\Local\Temp\1531706913191.png)

```javascript
var jeju = new naver.maps.LatLng(33.3590628, 126.534361);	
//제주도의 위도와 경도를 jeju변수에 저장
map.setCenter(jeju); // 중심으로 좌표 이동
```

![1531706890645](C:\Users\student\AppData\Local\Temp\1531706890645.png)

![1531706941557](C:\Users\student\AppData\Local\Temp\1531706941557.png)

![1531706951939](C:\Users\student\AppData\Local\Temp\1531706951939.png)

 zoom값은 1~15

1일수록 전체적으로 보임. 15일수록 가까이 확대되는 것



![1531706988835](C:\Users\student\AppData\Local\Temp\1531706988835.png)

![1531706999473](C:\Users\student\AppData\Local\Temp\1531706999473.png)



### 지도 축적 확대 /축소 막대 추가하기

![1531707044927](C:\Users\student\AppData\Local\Temp\1531707044927.png)

![1531707071160](C:\Users\student\AppData\Local\Temp\1531707071160.png)

이 줌 컨트롤만 필요한 것. 다른 것들은 뭐 네이버 로고 쓸거냐 안쓸 거냐 이런 거임.



![1531707103676](C:\Users\student\AppData\Local\Temp\1531707103676.png)

![1531707116128](C:\Users\student\AppData\Local\Temp\1531707116128.png)

![1531707135007](C:\Users\student\AppData\Local\Temp\1531707135007.png)

변수 map 위에 붙여넣을 것



![1531707164097](C:\Users\student\AppData\Local\Temp\1531707164097.png)

mapOptions 추가!!

![1531707181069](C:\Users\student\AppData\Local\Temp\1531707181069.png)



오른쪽 하단으로 이동시키기

![1531707239789](C:\Users\student\AppData\Local\Temp\1531707239789.png)

![1531707258803](C:\Users\student\AppData\Local\Temp\1531707258803.png)

![1531707294407](C:\Users\student\AppData\Local\Temp\1531707294407.png)

zoomControl 안에 , 하고 붙여넣기

![1531707318589](C:\Users\student\AppData\Local\Temp\1531707318589.png)

이동할 곳으로 수정



![1531707337230](C:\Users\student\AppData\Local\Temp\1531707337230.png)

* cf. 자바스크립트 주석 :  //

디폴트값은 large / 지금은 small이라서 작게 나온 것.

![1531707372461](C:\Users\student\AppData\Local\Temp\1531707372461.png)



![1531707423699](C:\Users\student\AppData\Local\Temp\1531707423699.png)

대한민국까지 줌을 넓게 볼 필요는 없으니 적당히 축소되도록 정의할 수 있다



아래는 최소 5 / 최대 13 정도로 적용한 모습

![1531707508394](C:\Users\student\AppData\Local\Temp\1531707508394.png)

![1531707590035](C:\Users\student\AppData\Local\Temp\1531707590035.png)

naver라는 오브젝트에 maps라는 key가 있고 거기에 접근했더니 또 Map이라는 오브젝트가 있고 그런 구조다..



![1531707629279](C:\Users\student\AppData\Local\Temp\1531707629279.png)

![1531707643565](C:\Users\student\AppData\Local\Temp\1531707643565.png)

![1531707700669](C:\Users\student\AppData\Local\Temp\1531707700669.png)

(네이버 그린팩토리 주소)

![1531707716544](C:\Users\student\AppData\Local\Temp\1531707716544.png)

![1531707760764](C:\Users\student\AppData\Local\Temp\1531707760764.png)

![1531707871980](C:\Users\student\AppData\Local\Temp\1531707871980.png)

![1531707806422](C:\Users\student\AppData\Local\Temp\1531707831612.png)







---

![1531707911999](C:\Users\student\AppData\Local\Temp\1531707911999.png)

==`document.getElementById('map');`

그래서 이 부분 map 이름을 바꾸면 동작 안함.



![1531708052931](C:\Users\student\AppData\Local\Temp\1531708052931.png)

지도의 크기는 이 div태그의 수치를 따라간다



![1531708082450](C:\Users\student\AppData\Local\Temp\1531708082450.png)

naver api 인증 코드





![1531708304156](C:\Users\student\AppData\Local\Temp\1531708304156.png)

마커 하나 더 추가

![1531708286575](C:\Users\student\AppData\Local\Temp\1531708286575.png)

제주도에도 추가로 핀이 꽂힘 ㅎㅎ





![1531708356817](C:\Users\student\AppData\Local\Temp\1531708356817.png)

![1531708373373](C:\Users\student\AppData\Local\Temp\1531708373373.png)

![1531708498524](C:\Users\student\AppData\Local\Temp\1531708498524.png)

![1531708650508](C:\Users\student\AppData\Local\Temp\1531708650508.png)







- 원래` 'ㅇㄹㅇㅁ`

  `ㅁㅎ'` 이런식으로 스트링 중간에 엔터를 치면 위에 줄만 스트링으로 됨. 다른 언어들도 그럼.

  ==> ` 2015년부터 추가된 기능 (빽틱) 을 쓰면 엔터 쳐도 스트링으로 추가됨







---



![1531715485497](C:\Users\student\AppData\Local\Temp\1531715485497.png)

맨 밑까지 스크롤 내리면

![1531715580175](C:\Users\student\AppData\Local\Temp\1531715580175.png)

함수 복사

![1531715609551](C:\Users\student\AppData\Local\Temp\1531715609551.png)

붙여넣기



![1531715723217](C:\Users\student\AppData\Local\Temp\1531715723217.png)

이 이름대로 배열을 만들어 마커들이랑 정보창들을 넣어 준다



![1531715763378](C:\Users\student\AppData\Local\Temp\1531715763378.png)

![1531715773629](C:\Users\student\AppData\Local\Temp\1531715773629.png)









![1531716047377](C:\Users\student\AppData\Local\Temp\1531716047377.png)







![1531717739620](C:\Users\student\AppData\Local\Temp\1531717739620.png)





---

https://github.com/43dp/daily-notes/issues/1

```
var data = [
{name: "아리차이", address: "서울특별시 관악구 신림동길 4", link: "https://store.naver.com/restaurants/detail?id=11704746", x: 126.9282765, y: 37.4876462},
{name: "한우등촌골", address: "서울특별시 강서구 등촌로 201", link: "https://store.naver.com/restaurants/detail?id=35966485", x:126.86273, y: 37.5476847},
{name: "수유부추곱창", address: "서울특별시 강북구 도봉로87길 26-21", link: "https://store.naver.com/restaurants/detail?id=37111836", x: 127.0247721, y: 37.6393168},
{name: "강천민물장어", address:"서울특별시 강동구 올림픽로 834 한강시티라이프", link: "https://store.naver.com/restaurants/detail?id=18905396", x: 127.1297937, y: 37.5553916 }
];
```











---

https://docs.google.com/spreadsheets/d/1UPUU_-KYpQ1FlhYRlISIH7YAcuNCAMVl90XGxCc8p5w/edit#gid=0

![1531721053068](C:\Users\student\AppData\Local\Temp\1531721053068.png)

다운받은 파일 c9에 떤져!!

![1531721229667](C:\Users\student\AppData\Local\Temp\1531721229667.png)



`rails g model School name:string address:string lng:float lat:float`

(model 치다가 중간에 엔터 쳤을 경우)

`rails d model School`

![1531721531174](C:\Users\student\AppData\Local\Temp\1531721531174.png)





씨드 넣자아

![1531721335483](C:\Users\student\AppData\Local\Temp\1531721335483.png)

```ruby
require 'csv'
CSV.foreach(Rails.root.join("school.csv"), headers: true) do |row|
    School.create! row.to_hash
end
```

![1531721485481](C:\Users\student\AppData\Local\Temp\1531721485481.png)

`rake db:migrate`

`rake db:seed`



![1531721665207](C:\Users\student\AppData\Local\Temp\1531721665207.png)

data 개수 확인 (999개)



![1531721722991](C:\Users\student\AppData\Local\Temp\1531722023428.png)

map 컨트롤러에.

(Schools 데이터 배열로 다 들어가 있는 거 콘솔창에서 확인해 보려면 아래같이)

![1531723523436](C:\Users\student\AppData\Local\Temp\1531723523436.png)





![1531722100904](C:\Users\student\AppData\Local\Temp\1531722100904.png)

index페이지에.



![1531722058698](C:\Users\student\AppData\Local\Temp\1531722058698.png)







---

### 마커 모양 (핀) 바꾸기



![1531722144038](C:\Users\student\AppData\Local\Temp\1531722144038.png)

![1531722226946](C:\Users\student\AppData\Local\Temp\1531722226946.png)

![1531722296723](C:\Users\student\AppData\Local\Temp\1531722296723.png)



![1531722317053](C:\Users\student\AppData\Local\Temp\1531722317053.png)

HOME_PATH는 우리가 갖고 있는 게 아님

https://navermaps.github.io/maps.js/docs 이거로 바꿔  (이 문서의 HOME_PATH가 docs까지임)

![1531722407054](C:\Users\student\AppData\Local\Temp\1531722407054.png)



![1531722505628](C:\Users\student\AppData\Local\Temp\1531722505628.png)

![1531722527589](C:\Users\student\AppData\Local\Temp\1531722527589.png)

샐리가 계속 뜀

![1531722551498](C:\Users\student\AppData\Local\Temp\1531722551498.png)

ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ





---

![1531723144472](C:\Users\student\AppData\Local\Temp\1531723144472.png)

![1531723163728](C:\Users\student\AppData\Local\Temp\1531723163728.png)

이 코드만 필요해용



![1531723211791](C:\Users\student\AppData\Local\Temp\1531723211791.png)

for 문 끝나는 곳에 복붙



마우스로 지도 끌 때마다 새로운 지도 영역 나타날 때마다 그 때 그 때  

(막 만 개 이상 되고 그러면 안됨..따로 컨트롤러 지정해야함)



