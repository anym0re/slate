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
      "UUID":"00000000-2edc-3639-26ae-dd4a2a9258b2",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": "아이디와 비밀번호를 확인해주세요."
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
uuid | 필수아님 | 36자 | 기기 고유번호

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
curl "https://gameruncher.com/v1/auth/SighUpEmailValidation"
  -H "content-Type: application/json"
  -d '{
      "email":"hi_im_groot@naver.com",
      }'
```

> Example Response

```json
 {
    "code": -1,
    "msg": {
        "email": [
            "이미 가입된 이메일입니다."
        ]
    }
  }
```

입력받은 이메일이 이미 존재하는 이메일인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/SighUpEmailValidation`

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
curl "https://gameruncher.com/v1/auth/SighUpNicknameValidation"
  -H "content-Type: application/json"
  -d '{
      "nickanme":"아임그루트",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": {
        "nickname": [
            "이미 존재하는 닉네임입니다."
        ]
    }
  }
```

입력받은 닉네임 이미 존재하는 닉네임인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/SighUpNicknameValidation`

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
curl "https://gameruncher.com/v1/auth/SighUpPhoneValidation"
  -H "content-Type: application/json"
  -d '{
      "phone":"010-0000-0000",
      }'
```

> Example Response

```json
  {
    "code": -1,
    "msg": {
        "phone": [
            "이미 가입된 휴대폰 번호입니다."
        ]
    }
  }
```

입력받은 휴대폰 번호가 이미 존재하는 휴대폰 번호인지 확인힙니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/SighUpPhoneValidation`

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
    ]
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


## 아이디 찾기

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/findIdentity"
  -H "content-Type: application/json"
  -d '{
      "name":"홍길동",
      "birth":"1997-11-26",
      "phone":"010-0000-0000",
      }'
```

> 실패 Example Response

```json
  {
    "code": -1,
    // 1번
    "msg": {
        "name or birth or phone": [
            "일치하는 회원 정보가 없습니다."
        ]
    },
    // 2번 편하신 방법으로 알려주세요.
     "msg": "일치하는 회원 정보가 없습니다."
  }
```

> 성공 Example Response

```json
  {
      "code": 0,
      "return": "example@gameruncher.com"
  }
```

입력받은 값으로 일치하는 아이디를 리턴합니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/findIdentity`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
name | <span style="color:#c25300">**필수**</span>| 2~16자 한글,영어,숫자 | 회원 닉네임
birth | <span style="color:#c25300">**필수**</span>| <span style="color:#c25300">**확정되지않음**</span> | 회원 생년월일
phone | <span style="color:#c25300">**필수**</span>| 13자 xxx-xxxx-xxxx | 회원 휴대폰 번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
아직 확정된 API가 아닙니다.
</aside>


## 비밀번호 찾기 1

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/findPasswordStepOne"
  -H "content-Type: application/json"
  -d '{
      "email":"example@gameruncher.com",
      "name":"홍길동",
      "phone":"010-0000-0000",
      }'
```

> 실패 Example Response

```json
  {
    "code": -1,
    // 1번
    "msg": {
        "email or name or phone": [
            "일치하는 회원 정보가 없습니다."
        ]
    },
    // 2번 편하신 방법으로 알려주세요.
     "msg": "일치하는 회원 정보가 없습니다."
  }
```

> 성공 Example Response

```json
  {
      "code": 0
  }
```

입력받은 값과 일치하는 계정이 있는지 확인합니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/findPasswordStepOne`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
email | <span style="color:#c25300">**필수**</span>| Email 4~32자 소문자,대문자,숫자,@,. | 회원 이메일
name | <span style="color:#c25300">**필수**</span>| 2~16자 한글,영어,숫자 | 회원 닉네임
phone | <span style="color:#c25300">**필수**</span>| 13자 xxx-xxxx-xxxx | 회원 휴대폰 번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
아직 확정된 API가 아닙니다.
</aside>

## 비밀번호 찾기 2

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/findPasswordStepTwo"
  -H "content-Type: application/json"
  -d '{
      "phone":"010-0000-0000"
      }'
```

> 실패 Example Response

```json
  {
    "code": -1,
    "msg": {
        "phone": [
            "올바른 형식으로 입력해주세요."
        ]
    }
  }
```

> 성공 Example Response

```json
  {
      "code": 0
  }
```

비밀번호 찾기 1에 이용된 전화번호로 인증번호를 전송합니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/findPasswordStepTwo`

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
아직 확정된 API가 아닙니다.
</aside>

## 비밀번호 찾기 3

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/findPasswordStepThree"
  -H "content-Type: application/json"
  -d '{
      "code":"147329"
      }'
```

> 실패 Example Response

```json
  {
    "code": -1,
    "msg": "일치하는 코드가 없습니다."
  }
```

> 성공 Example Response

```json
  {
      "code": 0
  }
```

비밀번호 찾기 2에서 요청한 인증번호가 일치하는지 확인합니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/findPasswordStepThree`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
code | <span style="color:#c25300">**필수**</span>| 6자 숫자 | 회원 휴대폰 인증번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
아직 확정된 API가 아닙니다.
</aside>


## 비밀번호 찾기 4

> Example Request

```shell
curl "https://gameruncher.com/v1/auth/findPasswordStepFour"
  -H "content-Type: application/json"
  -d '{
      "email":"example@naver.com"
      "passowrd":"weareawesome!"
      }'
```

> 실패 Example Response

```json
  {
    "code": -1,
    "msg": {
          "passowrd": [
                        "올바른 형식으로 입력해주세요."
              ]
    }
  }
```

> 성공 Example Response

```json
  {
      "code": 0
  }
```

비밀번호를 변경합니다.

### ENDPOINT

`POST https://gameruncher.com/v1/auth/findPasswordStepFour`

### PARAMETERS

Parameter | Default | DataType | Description
--------- | ------- | -------- | -----------
email | <span style="color:#c25300">**필수**</span>| Email 4~32자 소문자,대문자,숫자,@,. | 회원 이메일
password | <span style="color:#c25300">**필수**</span>| String 4~32자| 회원 비밀번호

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
msg | 응답이 성공이 아닌 경우 설명 메세지 

<aside class="notice">
아직 확정된 API가 아닙니다.
</aside>

## 테마 리스트 얻기

> Example Request

```shell
curl -X GET \
  'https://gameruncher.com/v1/theme/lists/{hash}' \
  -H 'content-type: application/json'
```

> Example Response

```json
{
    "code": 0,
    "lists": [
        {
            "id": "1",
            "thumbnail": "https://gameruncher.com/thumbnail/ready_player_one.jpg",
            "title": "돈가방을 갖고 튀어라!",
            "description": "진짜 돈가방은 어디에",
            "price": 0,
            "time": "(1회, 3시간)",
            "level": "보통",
            "category": "로맨스|스릴러",
            "tags": "서울|망원동"
        },
        {
            "id": "2",
            "thumbnail": "https://gameruncher.com/thumbnail/ready_player_one.jpg",
            "title": "돈가방을 갖고 튀어라!",
            "description": "진짜 돈가방은 어디에",
            "price": 5000,
            "time": "(1회, 3시간)",
            "level": "어려움",
            "category": "로맨스|스릴러",
            "tags": "청담동|키워드"
        },
        {
            "id": "3",
            "thumbnail": "https://gameruncher.com/thumbnail/ready_player_one.jpg",
            "title": "돈가방을 갖고 튀어라!",
            "description": "진짜 돈가방은 어디에",
            "price": 11000,
            "time": "(1회, 3시간)",
            "level": "쉬움",
            "category": "로맨스|스릴러",
            "tags": "청담동|키워드"
        }
    ],
    "hash": "asdfasdfasdfasdf"
}
```

예약 앱 메인 페이지에 들어가는 리스트 정보를 받아옵니다.

### ENDPOINT

`GET https://gameruncher.com/v1/theme/lists/{hash}`

### RESPONSE

Code | Description
--------- | -------
code | 응답코드 <span style="color:#2cc200">**1 캐시**</span> <span style="color:#2cc200">**0 성공**</span> <span style="color:#c25300">**-1 실패**</span>
lists | 테마 리스트에 대한 정보를 제공합니다. <span style="color:#c25300">**응답 코드가 1일때는 리턴하지 않습니다.**</span>
hash | lists를 해쉬화한 값 입니다.
