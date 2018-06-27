rails crud



- `rails g controller posts index new create show edit update destroy`

- `rails g model post title:string content:text`    => post이름 가진 표 db 생성할 것이다(model)

- `rake db:migrate`

- 실제로 db에 저장하는 form을 만들어 볼게요

  => new.html.erb에





![1530062519164](C:\Users\student\AppData\Local\Temp\1530062519164.png)

레일즈에서는 보안을 신경써서 기본적으로 csrf방어 코드가 작동되게 돼있음.. 

--> **csrf**라는 공격이 있음(**사이트 간 요청 위조**)

우리가 돌리고 있는 서버가 아닌 다른 페이지에서 게시물이 작성됐는데 우리 게시판에 작성이 되면 안됨

- app폴더 -> appliction_controller ==> 이 코드가 csrf의 공격을 막아주는 코드

![1530062600878](C:\Users\student\AppData\Local\Temp\1530062600878.png)



- 어제는 get방식이었기 때문에 이 에러가 나지 않았음
- 저 코드를 주석처리하면(방어하지 않겠다고 하면) 에러 나지 않음
- token : 먼저 우리 사이트에서 토큰을 발행하고 form이랑 같이 보내고
  - authenticity token : 토큰값 같이 실어서 (전송)보내야 한다. 그럼 이 토큰이 우리 서버에서 발행된 거구나를 알 수 있음
  - form 액션 태그 안에다 `<input value="<%= form_authenticity_token %>">`
  - 랜덤하게 토큰 생성(새로고침 할 때마다 토큰 계속 바뀐당)



### http verb

: 토큰 실행 시 실제 행동하는 동사?

ex. 

포스트 작성하니 create

포스트 새로 작성하니 new

포스트 수정하니 edit



이런 식으로 동사로 붙였었음. 근데 길어지고 보기 안좋아져서 http verb 붙이기 시작했음

=> 아래 사진에 post / put /delete 이런 것들

![1530065071804](C:\Users\student\AppData\Local\Temp\1530065071804.png)





### --- 오늘 지금까지 어제 했던 것들을 restful 하게 바꿔본 것

<오창희 강사님이 해주신 오늘한 것들 메모>

# rails crud

- `rails g controller posts index new create show edit update destroy`
- `rails g model post title:string content:text`
- `rake db:migrate`



### Restful

```ruby
root 'posts#index'

# Create
get 'posts/new'
post 'posts' => "posts#create"

# Read
get 'posts/:id' => "posts#show"

# Update
get 'posts/:id/edit' => "posts#edit"
put 'posts/:id'=> "posts#update"

# Delete
delete 'posts/:id' => "posts#destroy"

# 'posts/:id' 가 똑같은 url요청이지만 앞부분의 get,put,delete verb의 차이로 다르게 요청이 보내집니다.
```

### form에서 post요청보내기

```html
<form action="/posts/create" method="post"> <!-- method속성 안에 "post"를 넣어줍니다. -->
    제목 : <input name="title" type="text">
    내용 : <input name="content" type="text">
    <input type="submit" value="저장">
    <input type= "hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
</form>
```

### form에서 put요청보내기

```html
<form action="/posts/<%= @post.id %>" method="post">
    <input type="hidden" name="_method" value="put"> 
    <!-- 새로운 hidden타입의 input태그를 넣어주고 name과 value를 설정했습니다. -->
    제목 : <input name="title" type="text" value="<%= @post.title %>">
    내용 : <input name="content" type="text" value="<%= @post.content %>">
    <input type="submit" value="저장">
    <input type= "hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
</form>
```

### a태그에 delete 방식 추가하기

```html
<a href="/posts/<%= @post.id %>" data-method="delete" data-confirm="너 진짜 지울꺼야??">삭제하기</a>
```







<오후>

---

 #### 쭐루님

## bit.do   처럼 긴 url 짧게 만들어 주는 기능 만들기

![1530073284532](C:\Users\student\AppData\Local\Temp\1530073284532.png)







1. 보통은 model을 먼저 만든다  (지금까지 컨트롤러 먼저 만들었지만..)

   `rails g model link short long`		short / long 항목이 든 db 이름 link

![1530073184119](C:\Users\student\AppData\Local\Temp\1530073184119.png)

2. 데이터베이스 생성  `rake db:migrate`

3. 컨트롤러 만들기

   (컨트롤러 이름은 복수로 만들어 준다. 모델이랑 같은 이름으로. 즉, 그 모델이름의 복수형으로)

   ![1530073473724](C:\Users\student\AppData\Local\Temp\1530073473724.png)

- 딱 컨트롤러 만들었을 때의 모습

![1530073678258](C:\Users\student\AppData\Local\Temp\1530073678258.png)

- restful하게 바꾼 모습!!!  ==> **crud** url 만들 때 규칙!! 지키자! (관례)



#routes.rb 의 url 정해주는 거는 / 안해주는 게 관례고 (앞에)  각 html 페이지에선 / 해줘야 함. 

	- 안그럼 /users/user/create 이런식으로 두 번 생김..



- 무언가 만들 때는(회원가입/로그인/글 같은 거) 다 post 방식으로 넘긴다





---

## cf.  쭐루님이 zzu.li 사셨댕 ㅎㅎㅎㅎㅎ

**고대디**는 좀 싸고

.tk  도메인은 공짜!

**가비아** - 가격차이가 많이 나용.. 사이트마다도 같은 도메인이라도 가격 차이가 나는뎅..

.io  국가 도메인

**namecheap**  쭐루님 여기 쓴댕..

---







---

- method 지정 안해주면 get방식으로 날아간다.  delete로 해주지 않으면 restful하지 않다

![1530077650188](C:\Users\student\AppData\Local\Temp\1530077650188.png)