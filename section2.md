# URI와 웹 브라우저 요청 흐름
> 요약 : URL , URN ⊂ URI이지만, URN은 고정적이라 잘 사용하지 않기 때문에 URL≒URI로 쓰임
> URL은 scheme, userinfo, host, port, path, query, fragment로 이루어져 있으며 이 정보를 바탕으로 HTTP 요청 메시지를 생성함

## URI(Uniform Resource Identifier)
 - *URI는 로케이터(Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있다*
 - URL , URN ⊂ URI
 - ```
   URL : foo://example.com:8042/over/there?name=ferret#nose
         \ /   \______________/ \________/ \_________/\___/
        scheme     authority      path        query    fragment
          |   _____________________|__
         / \ /                        \
   URN : urn:example:animal:ferret:nose
   ```
 - URI : Uniform-리소스 식별하는 통일된 방식 / Resource-자원, URI로 식별할 수 있는 모든 것 / Identifier-다른 항목과 구분하는데 필요한 정보
 - URL : Locator:리소스가 있는 위치를 지정
 - URN : Name:리소스에 이름을 부여
 - 위치는 변할 수 있지만, 이름을 변경하기 힘들며 URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화되어 있지 않아서 잘 사용 X
 - 그렇기 때문에 URI를 URL과 같은 의미로 이야기하는 경우가 많음
 - URL 전체 문법
   ```
   scheme://[userinfo@]host[:post][/path][?query][#fragment]
   https://www.google.com:443/search?q=hello&hl=ko#example
   ```
   - 프로토콜 : https   
     **scheme**
     - 주로 프로토콜 사용
     - 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙(http, https, ftp ...)
     - http는 80포트, https는 443 포트를 주로 사용하고 포트는 생략 가능함
     - https는 http에 보안을 추가한 것임

     **userinfo**
     - URL에 사용자정보를 포함하여 인증
     - 거의 사용하지 않음
          
   - 호스트명 : `www.google.com`   
     **host**
     - 호스트명
     - 도메인명 또는 IP주소를 직접 사용 가능함
          
   - 포트번호 : 443   
     **PORT**   
     - 포트(PORT)
     - 접속 포트
     - 일반적으로 생략, 생략시 http는 80, https는 443
          
   - 패스 : /search   
     **path**
     - 리소스 경로,계층적 구조(ex - /home/file1.jpg)
        
   - 쿼리 파라미터 : q=hello&hl=ko   
     **query**
     - key=value 형태
     - ?로 시작, &로 추가 가능
     - query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터,문자 형태
     
   - 프래그먼트 : #example   
     **fragment**
     - html 내부 북마크 등에 사용
     - 서버에 전송하는 정보X
       
## 웹 브라우저 요청 흐름
 **`https://www.google.com:443/search?q=hello&hl=ko`에 접속할 때**   
 1. IP주소를 DNS 서버에서 조회 및 Https port인 443은 생략
 2. HTTP 요청 메시지 (`GET /search?q=hello&hl=ko HTTP/1.1 Host:www.google.com`)을 생성
 3. SOCKET 라이브러리를 통해 전달(HTTP 프로토콜 사용)
 4. TCP 정보 생성, 메시지 데이터 포함(TCP 프로토콜 사용)
 5. IP 패킷 생성, TCP 데이터 포함(IP 프로토콜 사용)
 6. Ethernet frame을 씌움, IP 데이터 포함하여 LAN카드에서 인터넷을 통해 데이터 전달

