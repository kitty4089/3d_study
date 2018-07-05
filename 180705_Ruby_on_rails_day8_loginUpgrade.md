18. 07 .05

## login 3단계로 업그레이드!



> 1. 비밀번호 암호화
>
>    1) 단순 암호화 (MD5)
>
>    2) 빡센 암호화 (bcrypt)
>
>    
>
> 2. 로그인 이후 기능 추가
>
>    == helper method 만들기



> **오늘 한 c9 프로젝트**
>
> - 'login_upgrade'
> - 'devise'







---

**users** 컨트롤러를 만들어 준다

`rails g controller users login sessions signup register`



**User** 모델을 만든다

`rails g model User email password`



**rake** 해준다

`rake db:migrate`



홈페이지로 쓸 **home** 컨트롤러를 만들어 준다

`rails g controller home index`





*`rails c`  : 데이터베이스 콘솔

![1530754012236](C:\Users\student\AppData\Local\Temp\1530754012236.png)

데이터베이스에 그대로 비밀번호가 그대로 들어가 있기 때문에 안됨. 철컹철컹 각임

=> 암호화 해야함

=> 직접 하려면 어렵다 ==> MD5라는 암호화 모듈이 있당 //



![1530754331974](C:\Users\student\AppData\Local\Temp\1530754331974.png)

`require 'digest'` (digest가 클래스라고?!?! ㅇㅇ) 

digest 다이제스트란 모듈 안에 MD5가 있당.. 암호화 알고리즘이 다 공개되어 버림. 해쉬 알고리즘이 추적이 되었따. ==> 이거로 암호화 시키면 개나소나 다 풀  수 있게 되었다. (**md5 복호화 / decrypter**  구글링)



다이제스트 안에 여러 암호화 모듈이 있따. MD5는 그래서 이제 거의 쓰이지 않음. (쓰면 안됨)

유효성 검증할 때만 쓴당..

SHA-2  이더리움/비트코인 가장 많이 활용되고 있다. 이 기법이 없으면 비트코인이 존재조차 못한다

- 미국 국가안보국(NSA) 가 만들었고 양자 컴퓨터가 없으면 못 뚫는대. 디코더가 없어요.
- SHA-3로 더 업그레이드된 애...



`Digest::MD5.hexdigest("hello")` == digest 클래스 안에 MD5란 모듈이 있다

- hexdigest : 16진수 (hexadecimal)  - 0~9 10부터는 abcdef 까지 0~15 숫자로 표현. / 즉 0~9숫자와 abcdef로 표현

- MD5는 16진수와 타겟 스트링이든 뭐든 타겟과 일 대 일 암호화 해줌

- 근데 몇 개 아주 작은 쩜 하나의 변화도 큰 변화로 암호화해줌. 원리는 이런데 이제 MD5는 복호화 완전 가능.

  (쓰면 안돼!)  (같은 대상에 대해서는 딱 1대1 대응이기 때문에.. db화가 되어버려서 이미 해커들이 다 많이 쓰는 것들부터 1대1로 매핑다 되엉서)

  - 심지어 SHA-2도 통계적으로 많이 쓰였던 매핑은 밝혀졌.. 암호화 되어도 1대 1이기 때문에 어쩔 수 없..

  - a부터 단어들 다 써가면서 SHA-2로 어떻게 바뀌나 맞춰보면 되니까..

  - 그래서 salting을 하면 거의 뚫는 거 불가능이라고 보면 된다.. 

    ==> 비밀번호 + salt(첨가하는 랜덤글자) 처리를 해서 그 자체를 SHA-2로 바꿈.

    ==> **bcrypt**

    

![1530755226975](C:\Users\student\AppData\Local\Temp\1530755226975.png)





bcrypt

![1530758091407](C:\Users\student\AppData\Local\Temp\1530758091407.png)

풀어준당

![1530758106887](C:\Users\student\AppData\Local\Temp\1530758106887.png)



저장 후 콘솔에 `bundle`

![1530758130076](C:\Users\student\AppData\Local\Temp\1530758130076.png)





![1530758402871](C:\Users\student\AppData\Local\Temp\1530758402871.png)

bcrypt는 내부적으로 salt가 되어 있다! 

같은 1234도 다르게 해줌.



![1530758662032](C:\Users\student\AppData\Local\Temp\1530758662032.png)



![1530758647829](C:\Users\student\AppData\Local\Temp\1530758647829.png)

![1530758702469](C:\Users\student\AppData\Local\Temp\1530758702469.png)

![1530758734324](C:\Users\student\AppData\Local\Temp\1530758734324.png)

![1530758777967](C:\Users\student\AppData\Local\Temp\1530758777967.png)



![1530758820591](C:\Users\student\AppData\Local\Temp\1530758820591.png)











---

근데 비크립트고 뭐고 

그냥 `gem devise` 이용하면 ㅎㅎㅎㅎ 다 된당

(rails앱을 만들 때 웬만하면 다 쓰는 것. 이렇게 하는게 보안상 안전함.	ex. 왓챠도..텀블벅도 예전엔.)





1. devise c9 프로젝트 만들어 준당

2. Gemfile에 gem을 넣어준다

   ![1530764643810](C:\Users\student\AppData\Local\Temp\1530764643810.png)

   - 콘솔에 `bundle`

     ![1530764662548](C:\Users\student\AppData\Local\Temp\1530764662548.png)

     

   3. `rails generate devise:install`   (혹은  `rails g devise:install`)

      -> 암호화 시키고 홈으로 돌리므로 home정보가 필요

   4. 홈을 만들어 준당

      `rails g controller home index`

      -> 루트에 홈 지정

      ![1530764814543](C:\Users\student\AppData\Local\Temp\1530764814543.png)

      

   5. `rails g devise User`  (cf. 모델 만드는 코드와 비슷)

      ![1530764883532](C:\Users\student\AppData\Local\Temp\1530764883532.png)

      실제로 db migrate 안에 여러가지 만들어져있다 방금 전 코드로 인해

   6. rake 해준당 

      `rake db:migrate`

      ----끝---



> > >  서버를 켜보자

할당된 url 뒤에 ` /users/sign_up` 붙여서 로드해 보면 회원가입 가능.

![1530765518842](C:\Users\student\AppData\Local\Temp\1530765518842.png)

계정 만들어준 후



![1530765247166](C:\Users\student\AppData\Local\Temp\1530765247166.png)

![1530765381544](C:\Users\student\AppData\Local\Temp\1530765381544.png)