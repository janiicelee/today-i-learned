## 콘솔 빌드해서 실행해보기   
- backend.ai-console 클로닝하기   
``` git clone https://github.com/lablup/backend.ai-console.git ```
- 디렉토리 들어가서 node.js 패키지 설치 : npm i
- 디렉토리 안에 샘플 config.toml.sample 복사하기
- menu의 blocklist 주석처리하기
- 앱 프록시를 컴파일하기 : make compile_wsproxy
- 타입스크립트 컴파일하기 : npm run build:d
- 별도의 터미널 열고 테스트용 웹서버 띄우기 : npm run server:d (http://127.0.0.1:9081 에서 확인.)
- 세번째 터미널 열고 프록시 띄우기 : npm run wsproxy