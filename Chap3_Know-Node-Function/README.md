# 3장 노드 기능 알아보기

## 3.1 REPL 사용하기
* 읽고(Read), 해석하고(Eval), 결과물을 반환하고(Print), 종료할 때까지 반복(Loop)
* 터미널에서 `node` 입력하면 자바스크립트 코드 사용 가능

## 3.2 JS 파일 실행하기
* 파일 생성 후 콘솔에서 node [자바스크립트 파일 경로(확장자 생략)]

## 3.3 모듈로 만들기
* 모듈이란?     
`특정한 기능을 하는 함수나 변수들의 집합`     
하나의 프로그램이면서 다른 프로그램의 부품으로도 사용 가능(재사용 가능)     
3.3(index.js / func.js / var.js)

## 3.4 노드 내장 객체 알아보기
* global
브라우저의 window와 같은 전역 객체     
모든 파일에서 접근 가능     
3.4(globalA.js / globalB.js)

* console
time(레이블) : timeEnd와 대응되어 같은 레이블을 가진 time과 timeEnd 사이의 시간을 측정     
log(내용) : 평범한 로그를 콘솔에 표시     
error(에러 내용) : 에러를 콘솔에 표시     
table(배열) : 배열의 요소로 객체 리터럴을 넣으면, 객체의 속성들이 테이블 형식으로 표현     
dir(객체, 옵션) : 객체를 콘솔에 표시할 때 사용 / 첫 번째 인수 : 표시할 객체, 두 분째 인수 : 옵션(true: 콘솔에 색이 추가 됨)     
trace(레이블) : 에러가 어디서 발생 했는지 추적할 수 있게 함     
3.4(console.js)

* __filename, __dirname
현재 파일명(__filename)과 현재 파일 경로(__dirname)     
3.4(filename.js)

* module, exports, require
module.exports === exports     
require     
-require는 함수이고, 함수는 객체이므로 객체로서 몇 가지 속성을 가지고 있음     
-require가 반드시 파일 최상단에 위치할 필요가 없고, moodule.exports도 최하단에 위치할 필요가 없음     
require.cache     
-파일 이름이 속성명으로 들어 있음 / 속성값으로난 각 파일의 모듈 객체가 들어 있음     
-한번 require한 파일은 cache에 저장되어서 새로 불러오지 않고 cache에 있는 것이 재사용     
-새로 require하길 원한다면 cache의 속성을 제거(프로그램 동작이 꼬일 수 있으므로 권장하지는 않음)     
require.main     
-노드 실행 시 첫 모듈을 가리킴     
-객체 모양은 cache의 모듈 객체와 같음     
-`순환참조`가 발생하는 경우 순환 참조되는 대상을 빈 객체로 만듬

* process
`현재 실행되고 있는 노드 프로세스에 대한 정보를 담고 있음`     
`````
    process.version : 설치되 노드의 버전
    process.arch : 프로세서 아키텍처 정보
    processs.platform : OS 플랫폼 정보(linux, darwin, freebsd 등)
    process.pid : 현재 프로세스의 아이디
    process.uptime() : 프로세스가 시작된 후 흐른 시간(단위: 초)
    process.execPath : 노드의 경로
    process.cwd() : 현재 프로세스가 실행되는 위치
    process.cpuUsage() : 현재 cpu 사용량
`````
     
process.env     
시스템의 환경 변수     
노드에 직접 영향을 미치기도 함     
서비스의 중요한 키를 저장하는 공간으로도 사용     
      
process.nextTick(콜백)     
이벤트 루프가 다른 콜백 함수들보다 nextTick의 콜백 함수를 우선으로 처리     
마이크로태스트(microtask)라고 따로 구분지어 부름     
     
process.exit(코드)     
실행 중인 노드 프로세스를 종료
     
## 3.5 노드 내장 모듈 사용하기
`공식 문서에 모두 나와 있는 내용이지만 중요하고 자주 사용하는 것들만 소개`

* os
노드는 os모듈에 정보가 담겨 있어 정보를 가져올 수 있음    
3.5(os.js)

* path
`os별로 경로 구분자가 다르기 때문에 필요`     
폴더와 파일의 경로를 쉽게 조작하도록 도와주는 모듈     
3.5(path.js)

* url
인터넷 주소를 쉽게 조작하도록 도와주는 모듈     
url.parse(주소): 주소를 분해 / WHATWG 방식과 비교하면 username, password 대신 auth 속성이 있고, searchParams 대신 query가 있음     
url.format(객체): WHATWG 방식 url과 기존 노드의 url을 모두 사용할 수 있음 / 분해되었던 url 객체를 다시 원래 상태로 조립     
<img src="WHATWG.png" alt="WHATWG" />
3.5(url.js, searchParams.js)     

* querystring
WHATWG 방식의 url 대신 기존 노드의 url을 사용할 떄, search 부분을 사용하기 쉽게 객체로 만드는 모듈     
3.5(querystring.js)