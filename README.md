# [Hertz](https://www.hertz-radio.gq/)

<br>

# Model

### User

- Devise gem 사용

  `gem 'devise'`

  `bundle install`



### Category

- Helper 메서드 사용해서 보여줄 때 처리
- default : 0



### Channel

`rails g model channel user:references frequency:float title:string onair:integer category:integer`

##### frequency (not null)

- 87.5 ~ 108.0 MHz 
- 소수점 3자리수까지

##### category (not null)

- default : 0 ----> 음악

##### title

- null 가능

```ruby
has_many :diary
has_many :timetable
```

##### onair

- 0 : off  방송안함
- 1 : on 방송 중
- 2 : 방송 준비 중



### Diary

`rails g model diary channel:references max_audience:integer title:string content:text finished_at:datetime index:integer  `

##### max_audience

- default : 0

##### index (not null)

- 몇 번째 diary인지 
- title 앞에 표시 ( 첫 번째 다이어리, 두 번째 다이어리 ..  .)
- channel.diaries.count + 1



### Timetable

`rails g model timetable channel:references start:datetime end:datetime  `





# Controller

- main

  `rails g controller main main`

- channel 컨트롤러 

  `rails g controller channels index new create show edit update destroy`

  get 'channels/:id' => 'channels#show'  사용 X

  get '/:id' => 'channels#show'  사용

- diary

  `rails g controller diaries index new create show edit update destroy`

- timetable

  `rails g controller timetables index new create show edit update destroy`



```ruby
# routes.rb

root 'main#main'
get	'main/main'

resources :timetables
resources :channels
resources :diaries

devise_for :users
```



### Channels controller

| HTTPVerb     | Path               | action  | used for                                                     |
| ------------ | ------------------ | ------- | ------------------------------------------------------------ |
| GET          | /channels          | index   | display a list of all channels                               |
| GET          | /channels/new      | new     | return an HTML form for creating a new channel<br /> if current_user has channel already, redirect to '/channels/:id/edit' |
| POST         | /channels          | create  | create a new channel                                         |
| GET (사용 X) | /channels/:id      | show    | display a specific channel                                   |
| GET          | /:id               | show    | display a specific channel                                   |
| GET          | /channels/:id/edit | edit    | return an HTML form for editing an channel (diaries and broadcast state) |
| PUT          | /channels/:id      | update  | update a specific channel                                    |
| DELETE       | /channels/:id      | destroy | delete a specific channel                                    |

<br>

<br>

![img1](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_1.png)

<br>

### 메인 페이지

![img2](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_2.png)

<br>

### 로그인 / 회원가입 

![img3](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_login.png)

<br>

### 채널생성 / 방송하기

![img4](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_4.png)

![img5](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_5.png)

![img6](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_6.png)

<br>

![img7](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_7.png)

<br>

### 타임테이블

![img8](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_table1.png)

![img9](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_table2.png)

<br>

### 방송듣기

![img10](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_custom1.png)

<br>

### 사연보내기

![img11](https://raw.githubusercontent.com/zoe0-0/mypages/master/img/portfolio/pj4/pj4_custom2.png)

