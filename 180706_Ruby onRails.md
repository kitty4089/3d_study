18. 07 .06

## fake Instagram  (이 날 하루종일 졸고 하나도 못들음 ㅎㅎ)

- Post(CRUD)  ==> 'carrier wave' gem 쓸 것.
- User(CRUD ==> 'devise')

---

스캐폴딩(rails가 갖고 있는 강력한 툴)

---

***c9프로젝트;  'fake_Ingstagram'**





scaffold  ==> model 대신 scaffold라고만 해줌 된다

`rails g scaffold Post content image user_id:integer tag`

: .fh

`rake db:migrate`  위에 만든 설계도를 실제로 db에 적용시킨다.





` rake routes`   : 모든 롸우트를 보여준다 (내가 만든게 아닌 것도)



jpg로 끝나는 거 복붙 



![1530837611396](C:\Users\student\AppData\Local\Temp\1530837611396.png)



새로운 gem을 깔았어도 서버 껐ㄷ다 켜



`rails g uploader Image`

- 우리는 active record란 orm을 쓰고 있당





##### 파일을 업로드하는 form하겠다

![1530838423056](C:\Users\student\AppData\Local\Temp\1530838423056.png)





`rails g devise:install`

`rails g devise User`



`rake db:migrate`

![1530839696671](C:\Users\student\AppData\Local\Temp\1530839696671.png)





`rails

/rails/inlfo/routes   : 우리 앱이 갖고있는 콘트롤러,



rails hidden field  구글링 ㄱㄱ

