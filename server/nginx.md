## Nginx
- Nginx는 웹서버이다. 간단하게 웹서버는 클라이언트로 부터 요청이 발생했을 때 요청에 맞는 정적파일을 보내 주는 역할을 한다. Nginx는 규모가 작은 서비스이면서 정적 데이터 처리가 많은 서비스에 적합하다. 

- Nginx는 일반적인 HTTP의 웹서버의 역할 외에도 proxy, reverse proxy 서버의 역할 또한 가능하다. 양대산맥인 Apache와 두드러지게 다른 특징을 가지고 있는데, Apache는 MPM(multi Processing Module: 다중 처리 모듈) 방식을 사용하는 반면, Nginx는 Event driven 방식을 통해 구동된다. Event driven은 Node.js에서도 사용하는 방식이다. 이러한 장점은 메모리를 좀 더 효율적으로 운용할 수 있는 결과를 가져온다.