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

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

