# [Day 09] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-06
과목: FE

## 오늘 학습한 주제
- SSE

## 오늘 배운 것 
- SSE
  <p>
  SSE는 Sever-Sent Events 의 약자로 서버에서 클라이언트로 실시간 데이터를 전달하는 기술이다.
  일반적인 HTTP 통신은 클라이언트가 요청하면 서버가 응답을 보내고 연결이 끝난다. 하지만 SSE는 HTTP 연결을 유지하면서
  서버에서 새로운 데이터가 발생할 때마다 클라이언트에게 전달할 수 있다.<br>
  비슷한 기술로 WebSocket이 있다. WebSocket은 양방향 통신이 가능하다. SSE는 서버에서 클라이언트로 데이터를 전달하는 단방향 통신이기에 둘의 차이가 있다.
  </p>
<br>
<br>

## SSE 동작 방식
- 오늘 실습에서는 알림 기능에 SSE를 적용했다.
<br>
<br>

<img width="467" height="200" alt="스크린샷 2026-11-06 19 44 16" src="https://github.com/user-attachments/assets/bd8a0b3e-f49c-4ad8-8157-1affd1b5149f" />
<br>
<br>


- 브라우저에 내장된 EventSource로 연결된다. 일반 fetch와 달리 한 번 열어 두면 메시지가 올 떄마다 onmessage가 실행된다.<br>
  단, EventSource는 브라우저 API라서 서버 렌더링 중에는 쓸 수 없다. 대신, "use client" 컴포넌트의 useEffect 안에서 연결한다. 
<br>
<br>


<img width="479" height="191" alt="스크린샷 2026-11-06 19 57 50" src="https://github.com/user-attachments/assets/54d3dbd0-384b-4a53-87cf-cf2ac9bc1fba" />
<br>
<br>

- EventSource가 클라이언트에서 서버의 이벤트를 받는 역할이라면, ReadableStream은 서버에서 데이터를 전달하는 역할이다. 일반 HTTP응답과 달리 연결을 바로
종료하지 않고, 처음 연결할 때 현재 변경 내용을 전달한다.
<br>
<br>

## MongoDB

MongoDB atlas에는 Change Stream이라는 기능이 있다. Change Stream은 MongoDB에서 데이터의 추가,수정,삭제 등 변경 사항을 감지하는 기능이다. 
Change Stream을 통해 DB의 변경 사항을 감지하고 SSE는 변경된 데이터를 클라이언트에게 전달하는 역할을 한다. 
<br>
<br>


## 어려웠던 점

오늘 SSE에 대해 공부하면서 WebSocket, 폴링과 같은 실시간 데이터 처리 기술들이 있다는 것을 알게 되었다. 각각의 동작 방식과 차이점은 어느 정도 이해했지만, 실제 프로젝트에서 어떤 상황에 어떤 기술을 
사용해야 하는지는 아직 명확하게 이해하지 못했다. 단순히 기술의 차이점을 아는 것뿐만 아니라 상황에 맞는 기술을 선택하는 기준에 대해서도 공부가 필요할 것 같다. 

