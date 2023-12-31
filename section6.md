# HTTP 상태코드 : 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능
> 요약 : 1,2,3,4,5백번대 대표적인 오류 메시지를 확인해보았다.

## 1XX (Informational):요청이 수신되어 처리중
- 거의 사용X
## 2XX (Successful):요청 정상 처리
- 200 OK : 요청 성공
- 201 Created : 요청 성공해서 새로운 리소스가 생성됨
- 202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
  - ex) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리하는 경우
- 204 No Content : 서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 데이터가 없음
  - ex) 웹 문서 편집기에서 save 버튼 ( 버튼의 결과로 어떠한 화면도 어떠한 내용이 없어도 204 메시지만으로도 성공 인식 가능) 
## 3XX (Redirection):요청을 완료하려면 추가 행동이 필요 (ex - 3XX 응답 결과에 Location헤더가 있다면 해당 Location으로 이동)
- 300 Multiple Choices : 안씀
- 301 Moved Permanently : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)
- 302 Found : 리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY) -> 하지만 거의 항상 GET으로 변해 이미 많은 애플리케이션 라이브러리가 사용하고 있는 302가 아직까지 흔히 쓰임 
- 303 See Other : 302와 기능은 같으나 리다이렉트시 GET으로 변경 -> 302의 모호성 문제를 해결하기 위해 등장
- 304 Not Modified : 클라이언트에게 리소스가 수정되지 않았음을 알려줘서 로컬PC에 이미 저장된 캐시를 재사용하도록 함(캐시로 리다이렉트)
- 307 Temporary Redirect : 302와 기능은 같으나 리다이렉트시 요청 메서드(MUST)와 본문을 유지함 -> 302의 모호성 문제를 해결하기 위해 등장
- 308 Permanent Redirect : 301과 기능은 같으나 리다이렉트시 요청 메서드와 본문을 유지함(처음 POST를 보내면 리다이렉트도 POST 유지함)
- ## Redirection 종류
  - 영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동 (ex - /members -> /users) -> 301,308
  - 일시 리다이렉션 : 일시적인 변경(PRG) -> 302, 307, 303
    - PRG = Post/Redirect/Get -> PRG를 사용하지 않을 땐, 결과 화면을 새로고침을 하면 다시 POST로 요청을 해서 중복되는 문제가 있었는데 이걸 PRG가 URL을 POST에서 GET으로 리다이렉트를 해 새로 고침을 해도 GET으로 결과 화면만 조회하게 해서 중복 주문을 방지하였음
  - 특수 리다이렉션 : 결과 대신 캐시를 사용 -> 304
## 4XX (Client Error):클라이언트 오류, 잘못된 문법등으로 서버가 요청을 수행할 수 없음
- 401 Unauthorized : 클라이언트가 해당 리소스에 대한 인증(Authentication)이 필요
  - 401 오류 발생 시 응답에 WWW-Authenticate 헤더와 함께 인증 방법을 설명
  - Authentication이 인증이고, Authorization이 인가인데, 인증이 있어야 인가가 있는건데 401은 인증이 필요하다는 것에 대한 메시지이므로 엄연히 말하면 UnAuthenticated가 맞지 않나
- 403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함 (ex- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분할 경우)
- 404 Not Found : 요청 리소스를 찾을 수 없음
  - 요청 리소스가 서버에 없거나 클라이언트가 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때 발생
## 5XX (Server Error):서버 오류, 서버가 정상 요청을 처리하지 못함
- 500 Internal Server Error : 서버 문제로 오류 발생, 애매하면 500 오류
- 503 Service Unavailable : 서비스 이용 불가
  - 서버가 일시적인 과부화 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
  - Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

