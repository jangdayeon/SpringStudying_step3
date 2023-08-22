# HTTP 헤더1 - 일반 헤더
> 요약 : 1,2,3,4,5백번대 대표적인 오류 메시지를 확인해보았다.
## HTTP 헤더 개요
- HTTP 헤더는 HTTP 전송에 필요한 모든 부가정보가 들어 있음
- RFC2616(과거)에는 HTTP 헤더를 General 헤더, Request 헤더, Response 헤더, Entity 헤더로 분류하였고, HTTP BODY부분 즉, message body는 **entity** body를 전달하는데 사용하였음
- 현재 RFC723x에서는 이 **entity**에서 **representation**으로 바뀜
- 이 representation(표현)은 표현 메타데이터 + 표현 데이터를 뜻
- 참고로 표현 헤더는 표현 메타데이터 + 페이로드(=메시지 본문) 메시지임
 ![image](https://github.com/jangdayeon/SpringStudying_step3/assets/84323684/57ba9539-fde4-4134-9446-4cbf7e822857)
## 표현
- Content-Type : 표현 데이터의 형식 (ex - text/html; charset=utf-8 )
- Content-Encoding : 표현 데이터의 압축 방식 (ex - gzip 이나 deflate 이나 identity(압축x) )
- Content-Language : 표현 데이터의 자연 언어 (ex - ko 나 en 나 en-US )
- Content-Length : 표현 데이터의 길이
  - 바이트 단위로 작성하되 전송 코딩(Transfer-Encoding)을 사용하면 Content-Length를 사용하면 안됨
## 콘텐츠 협상
## 전송 방식
## 일반 정보
## 특별한 정보
## 인증
## 쿠키
