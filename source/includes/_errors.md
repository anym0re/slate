# HTTP 응답 코드 

### HTTP RESPONSE CODE


Code | Meaning
---------- | -------
200 | OK : 정상
400 | Bad Request -- Your request is invalid. ( 파라미터 오류 )
401 | Unauthorized -- Your API key is wrong.  ( 인증 오류 - 로그인되지 않은 상태에서 로그인이 필요한 url 접근 시 발생 )
404 | Not Found -- 존재하지 않는 요청 ( 페이지를 찾을 수 없음 )
429 | Too Many Requests -- throttle 제한 ( 짧은 시간 내에 너무 많은 요청을 보낼 시 발생 )
500 | Internal Server Error -- 서버 오류
503 | Service Unavailable -- 서버 오류


<!-- 403 | Forbidden -- The kitten requested is hidden for administrators only. -->
<!-- 405 | Method Not Allowed -- You tried to access a kitten with an invalid method. -->
<!-- 406 | Not Acceptable -- You requested a format that isn't json. -->
<!-- 410 | Gone -- The kitten requested has been removed from our servers. -->
<!-- 418 | I'm a teapot. -->