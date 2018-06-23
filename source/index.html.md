---
title: GameRuncher API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: false
---

# GameRuncher API 소개

GameRuncher를 통한 클라이언트와 서버가 통신하기 위한 API입니다. 

개발 중 질문사항이 있으시면 Discord 이승준#1926으로 연락주세요.

# API 목록

## 로그인

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/login"
  -H "content-Type: application/json"
  -d '{
      "email":"hi_im_groot@example.com",
      "password":"passwd123!",
      "UUID":"FFFF-FFFF-FFFF-FFFF (UUID 형식을 몰라서 대충 채워넣었습니다)",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": "아이디와 비밀번호를 확인해주세요.",
  }
```

입력받은 회원 정보를 기반으로 로그인을 시도합니다.

최초 로그인 시 UUID를 함께 보내면 회원정보에 UUID를 등록합니다.

앱 실행시에 UUID 확인 API로 true가 반환되면 자동으로 로그인을 시도해주세요.

<aside class="notice">만약 다른 휴대폰에서 같은 아이디로 로그인에 성공 한다면 UUID가 덮어쓰기 처리됩니다.</aside>

### ENDPOINT

`POST https://gameruncher.com/v1/auth/login`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
email | <span style="color:#c25300">**필수**</span>| Email 4~32자 소문자,대문자,숫자,@,. | 회원 이메일
password | <span style="color:#c25300">**필수**</span>| String 4~32자| 회원 비밀번호
uuid | 필수아님 | - | 기기 고유번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## 아이디 중복 확인

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/duplicateIdentityCheck"
  -H "content-Type: application/json"
  -d '{
      "email":"hi_im_groot@naver.com",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": "이미 가입된 이메일입니다.",
  }
```

입력받은 이메일이 이미 존재하는 이메일인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/duplicateIdentityCheck`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
email | <span style="color:#c25300">**필수**</span>| Email 4~32자 소문자,대문자,숫자,@,. | 회원 이메일

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
올바른 이메일 형식인지 여부의 에러도 출력함 code가 0이 아니면 msg내용을 그대로 출력
</aside>

## 닉네임 중복 확인

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/duplicateNicknameCheck"
  -H "content-Type: application/json"
  -d '{
      "nickanme":"아임그루트",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": "이미 존재하는 닉네임입니다.",
  }
```

입력받은 닉네임 이미 존재하는 닉네임인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/duplicateNicknameCheck`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
nickname | <span style="color:#c25300">**필수**</span>| 2~16자 한글,영어,숫자 | 회원 닉네임

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
올바른 닉네임 형식인지 여부의 에러도 출력함 code가 0이 아니면 msg내용을 그대로 출력
</aside>

## 휴대폰번호 중복 확인

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/duplicatePhoneCheck"
  -H "content-Type: application/json"
  -d '{
      "phone":"010-0000-0000",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": "이미 가입된 휴대폰 번호입니다.",
  }
```

입력받은 휴대폰 번호가 이미 존재하는 휴대폰 번호인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/duplicatePhoneCheck`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
phone | <span style="color:#c25300">**필수**</span>| 13자 xxx-xxxx-xxxx | 회원 휴대폰 번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
올바른 휴대폰 번호인지 여부의 에러도 출력함 code가 0이 아니면 msg내용을 그대로 출력
</aside>

## 힙한 회원가입 ! (둠칫)

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/join"
  -H "content-Type: application/json"
  -d '{
      "email":"hi_im_groot",
      "password":"wedidit!",
      "nickname":"우리는해낼것이다",
      "name":"김이박",
      "gender":0,
      "birth":"1997-11-26",
      "phone":"010-0000-0000",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": [
        { "name":"email", "msg":"아이디를 입력해주세요." },
        { "name":"password", "msg":"비밀번호를 입력해주세요."},
        { "name":"gender", "msg":"성별을 선택해주세요." }
    ],
  }
```

<del>드디어</del> 입력받은 회원정보들로 회원가입을 시도합니다.

이전 단계에서도 검증을 거치지만 최종적으로 모든 입력값에 대한 검증을 한번 더 한 다음 각각의 입력값에 대한 검증(에러)값이 리턴됩니다.

해당 단계에서는 여러 에러가 동시에 발생할 수 있기에 전의 입력 페이지로 넘어갈지 등의 여부는 논의해보는게 좋을 것 같습니다.


<aside class="warning">
아직 확정된 API가 아닙니다.
</aside>

### ENDPOINT

`POST https://gameruncher.com/v1/auth/join`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
email | <span style="color:#c25300">**필수**</span>| Email 4~32자 소문자,대문자,숫자,@,. | 회원 이메일
password | <span style="color:#c25300">**필수**</span>| String 4~32자| 회원 비밀번호
nickname | <span style="color:#c25300">**필수**</span>| 2~16자 한글,영어,숫자 | 회원 닉네임
name | <span style="color:#c25300">**필수**</span>| 2~16자 한글 | 회원 이름
gender | <span style="color:#c25300">**필수**</span>| 0 남자 1 여자 | 회원 성별
birth | <span style="color:#c25300">**필수**</span>| <span style="color:#c25300">**확정되지않음**</span> | 회원 생년월일
phone | <span style="color:#c25300">**필수**</span>| 13자 xxx-xxxx-xxxx | 회원 휴대폰 번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 ( 여러 입력값에 대해 묶음으로 리턴됩니다. example response 참조 )

## 테마 리스트 얻기

> Example Request

```shell
curl -X GET \
  'https://gameruncher.com/v1/theme' \
  -H 'content-type: application/json'
```

> Example Response

```json
  {
    "code": -1,
    "msg": [
        { "id":"1",
          "thumbnail_img":"https://gameruncher.com/assets/thumbnail_img/money_bag_run_away.jpg",
          "title":"돈가방을 갖고 튀어라!",
          "description":"진짜 돈가방은 어디에",
          "date":"2018-06-20",
          "time":"11:00~13:00",
          "level":"high",
          "category":"로맨스|스릴러",
          "tags":"청담동|키워드",
        },
        { "id":"2",
          "thumbnail_img":"https://gameruncher.com/assets/thumbnail_img/money_bag_run_away.jpg",
          "title":"돈가방을 갖고 튀어라!",
          "description":"진짜 돈가방은 어디에",
          "date":"2018-06-20",
          "time":"11:00~13:00",
          "level":"low",
          "category":"로맨스|스릴러",
          "tags":"청담동|키워드",
        },
        { "id":"3",
          "thumbnail_img":"https://gameruncher.com/assets/thumbnail_img/money_bag_run_away.jpg",
          "title":"돈가방을 갖고 튀어라!",
          "description":"진짜 돈가방은 어디에",
          "date":"2018-06-20",
          "time":"11:00~13:00",
          "level":"very high",
          "category":"로맨스|스릴러",
          "tags":"청담동|키워드",
        }
    ],
  }
```

예약 앱 메인 페이지에 들어가는 리스트 정보를 받아옵니다.

### ENDPOINT

`GET https://gameruncher.com/v1/theme`

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 ( 여러 입력값에 대해 묶음으로 리턴됩니다. example response 참조 )
