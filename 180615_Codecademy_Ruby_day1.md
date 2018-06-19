# codecademy

##### https://www.codecademy.com/learn Learn Ruby

### 1장 - 4장

18.06.15





## Intro of Ruby

- Ruby is case-sensitive (it cares about capitalization). 루비 대소문자 구분함!!!

<words>

#execute  실행하다 / 해내다

#parentheses = bracket

#bio  2.(짧은) 전기; (예능인의) 경력; (연감·선전 기사 등에서의) 인물 소개, 약력



### 1. Math

- Exponentiation (`**`) 

- Modulo 나눗셈 나머지 (`%`)   ( remainder of division )

  

### 2. Puts and Print

- `puts`(for "put string") is slightly different: it adds a new (blank) line after the thing you want it to print. 
- You can print out any strings you like! (Make sure to put your strings between quotes, like this: `"Hello!"`.) 



### 3. Everything in Ruby is an Object 

- Because everything in Ruby is an object (more on this later), everything in Ruby has certain built-in abilities called **methods **: "skills" that certain objects have 

  - ex. strings  : methods 예시 . the length of the string 

    

### 4. Interpreter / Editor / Console

The interpreter is the program that takes the code you write and runs it. You type code in the **editor**, the interpreter reads your code, and it shows you the result of running your code in the **console**. 

#### The `.length` Method

Methods are summoned using a `.`

<words>

#summon   소환하다

#conventions  (전산학)규약

#quotient  몫

#prompt   1. (사람에게 어떤 결정을 내리도록・어떤 일이 일어나도록) 하다[촉발하다]

2. (질문・힌트 등을 주어 말을 하도록) 유도하다



- string : `.length` of it, Ruby will return the length of the string (that is, the number of characters—letters, numbers, spaces, and symbols). 



#### `.reverse` Method 

: 	대상의 순서를 바꾸어줌 (ex. Exercise -> esicrexE )

- ex. to sort a list of values from highest to lowest instead of lowest to highest. 



#### `.upcase` / `.downcase` Method

: 	convert a string to ALL UPPER CASE or all lower case, respectively. 



### 5. Multi-Line Comments주석

: `=begin`과`=end` 사이에 넣는다

```Ruby
=begin
I'm a comment!
I don't need any # symbols.
=end

#I am Groot! :  이건 한 줄용 주석
```

- Don't put any space between the `=` sign and the words `begin` or `end`.  
  - math (`2 + 5` is the same as `2+5`) 에서는 띄어쓰기 상관 없는데 `=begin =end`는 =다음에 띄어쓰면 안된다!!
- `=begin` and `=end` also need to be on lines all by themselves :  그 줄에 단독으로 있어야 함



### 6. Naming Conventions

- **local variables** 

  By convention,

  - should start with a lowercase letter and words should be separated by **underscores**, 

  		like `counter`and `masterful_method` 

  - Ruby **won't** stop you from starting your local variables with other symbols, such as capital letters, `$`s, or `@`s,  (다른 거 써도 상관은 없지만) 
  - But by convention,
  - these mean different things, so it's best to avoid confusion by doing what the **Ruby community **does. 



### 7. Variables & Data Types

- 변수 선언 :`변수 이름 적고 = 값`만 하면 된다!!



### 8. Strings and String Methods

다시 리마인딩! ==> call a method by using the `.` operator 

`"string".method `

-  you can chain methods together

  ex. `name.method1.method2.method3 `

  - 왼쪽부터 순서대로 실행되는 듯하다







## Putting the Form in Formatter

* create a small program that will read a user's input and correct his or her capitalization

### 1. Prompting the User

`print "What's your first name?"`

<word>

#peek  1. (재빨리) 훔쳐보다   2. 살짝 보이다 

### 2. Getting Input

`variable_name = gets.chomp `

- `gets` :  the Ruby method that *gets* input from the user.  사용자가 입력한 input을 받을 수 있는 method
- `.chomp`:  input받을 때 자동으로 생성되는 enter라인들을 지워주는 명령어. When getting input, Ruby automatically adds a blank line (or **newline**) after each bit of input; `chomp` removes that extra line.  
- (오른쪽에 있는) 터미널이 `gets.chomp`  때문에 계속 인풋을 기다리고 있다. the terminal to the right is actually waiting for input because of `gets.chomp` 

### 3. Repeat for More Input

### 4. Printing the Output

##### - **string interpolation** 

​	:  "I took #{monkey} to the zoo" 

