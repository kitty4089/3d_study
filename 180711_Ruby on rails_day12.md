18 .07 .11

## 지도 api 사용해 보기

(다음지도- 국내)



다음지도 새로 가입이 필요 없다는 장점도 있당. 모두가 카톡을 쓰기 때문에 ㅎㅎ

*c9 프로젝트 이름 :  "sample-map"



**kakao developer** 구글링 ㄱㄱ

https://developers.kakao.com/

카카오 개발자 사이트



로그인



앱만들기 페이지로 자동 넘어간다

![1531293939399](C:\Users\student\AppData\Local\Temp\1531293939399.png)



![1531293962516](C:\Users\student\AppData\Local\Temp\1531293962516.png)



- **위도.경도를 입력받아서 그것을 지도에 찍어주는 방식입니당**



우리나라 지도에서는 위도 경도값을 받을 수 없다... 구글은 가능...

다음지도를 사용하지만 위도 경도값은 구글지도에서 갖고 오겟습니다 ㅎㅎㅎ오홍홍



![1531294340254](C:\Users\student\AppData\Local\Temp\1531294340254.png)



지도의 가운데 위/경도를 찍어주는 거임!!!  지도 움직이면 url이 계쏙 바뀜!!

내가 위/경도 뽑으려는 곳을 가운데 오게 위치시킨 상태에서 url 번호를 본다

37로 시작하는게 위도

127로 시작하는게 경도



---

**다음지도 api**

http://apis.map.daum.net/

![1531294504648](C:\Users\student\AppData\Local\Temp\1531294504648.png)

![1531294513674](C:\Users\student\AppData\Local\Temp\1531294513674.png)

![1531294591310](C:\Users\student\AppData\Local\Temp\1531294591310.png)

복사해서 아래 show페이지에 복붙



![1531294572096](C:\Users\student\AppData\Local\Temp\1531294572096.png)



다음단계인 javascript 코드 복사 /  페이지 열릴 때 먼저 javascript ~sdk.js 파일을 불러와서 지도를 그릴 준비를 해야 하기 때문에 head에 넣어 줍니다. 어디에 넣어도 동작은 하지만!

![1531294638133](C:\Users\student\AppData\Local\Temp\1531294638133.png)

![1531294781209](C:\Users\student\AppData\Local\Temp\1531294781209.png)



![1531294714674](C:\Users\student\AppData\Local\Temp\1531294714674.png)

복사



![1531294734236](C:\Users\student\AppData\Local\Temp\1531294734236.png)

![1531294750681](C:\Users\student\AppData\Local\Temp\1531294750681.png)

자기의 키를 넣어준당



다음 단계 코드 복사

![1531294855437](C:\Users\student\AppData\Local\Temp\1531294855437.png)

![1531294838072](C:\Users\student\AppData\Local\Temp\1531294838072.png)



![1531294953505](C:\Users\student\AppData\Local\Temp\1531294953505.png)

우리 위도 /경도 넣어야 하니 위에 있는 코드를 복붙해서 넣어준당



![1531294998445](C:\Users\student\AppData\Local\Temp\1531294998445.png)

![1531295018351](C:\Users\student\AppData\Local\Temp\1531295018351.png)

우리 사이트 주소를 복붙

![1531295057664](C:\Users\student\AppData\Local\Temp\1531295057664.png)

![1531295076675](C:\Users\student\AppData\Local\Temp\1531295076675.png)

![1531295203831](C:\Users\student\AppData\Local\Temp\1531295203831.png)



이제 지도에 핀을 찍어주자

![1531295255055](C:\Users\student\AppData\Local\Temp\1531295255055.png)

마커 검색



![1531295320630](C:\Users\student\AppData\Local\Temp\1531295320630.png)

![1531295343535](C:\Users\student\AppData\Local\Temp\1531295343535.png)

복붙



![1531295379196](C:\Users\student\AppData\Local\Temp\1531295379196.png)

우리 위도 경도로 바꿔준당



![1531295428140](C:\Users\student\AppData\Local\Temp\1531295428140.png)



