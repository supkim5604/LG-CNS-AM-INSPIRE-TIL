# [Day 01] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-10-27
과목: FE

## 오늘 학습한 주제
- CSR(Client-Side Rendering)
- SSR(Server-side Rendering)

## 오늘 배운 것 
1. CSR

CSR은 Client-Side Rendering의 약자로 모든 정보들을 한번에 받는다. 메타가 만든 리액트를 사용하여 웹을 만들 경우 이 렌더링 기술을 사용할 수 있다. SPA
웹 페이지 시작시 모든 정보들을 받아야 해서 초기 화면 로드가 느릴 수 있으나, 화면 로드가 된 후에는 이미 모든 정보들이 있으므로 다른 정보들을 받아 올 필요가 없다. 

2. SSR

SSR은 Server-side Rendering의 약자로 서버에서 HTML을 미리 생성하여 브라우저에 전달하는 방식이다. 서버에서 완성 된 HTML을 받기 때문에 초기 화면 로드는 빠를 수 있다. 
단 CSR과 달리 웹에서 필요한 정보들을 요청할 때 마다 받아오기 때문에 렌더링 작업이 발생하므로 서버 부하를 고려해야 한다. 

## 어려웠던 점 & 해결 과정
- 단순히 이론으로만 들었을 때는 이해가 잘되지 않았다. CSR과 SSR의 웹페이지 비교를 통해 두 렌더링 기술의 어떤 차이가 있는지 알 수 있었다. 

<img width="600"
     alt="CSR과 SSR"
     src="https://github.com/user-attachments/assets/3ad600b3-ac30-45be-8764-af35af2a1fee" />

-  React 홈페이지에서는 내부 메뉴를 이동하더라도 기존 HTML 문서의 전체 구조가 유지되는 것처럼 보였다. 이는 SPA(Single Page Application)에서 사용하는 클라이언트 라우팅의 특징과 관련이 있다. 클라이언트 라우팅에서는 페이지 이동 시 새로운 HTML 문서를 불러오는 대신 JavaScript를 이용해 필요한 DOM 요소를 변경할 수 있다. 

- 페이지 이동 전

<img width="600" alt="LG전자 홈페이지 페이지 이동 전 Elements 탭" src="https://github.com/user-attachments/assets/fb5d7e7d-358b-49e2-a90f-0a0bc05a4be6" />

- 페이지 이동 후

<img width="600" alt="LG전자 홈페이지 페이지 이동 후 Elements 탭" src="https://github.com/user-attachments/assets/759c18bc-f378-4af7-910a-9d8b36928a0a" />

- LG전자 홈페이지에서는 다른 페이지로 이동한 후 Elements 탭에서 확인되는 HTML 구조가 크게 달라지는 것을 관찰하였다.
특히 <body> 내부의 요소와 <script> 태그의 구성이 이전 페이지와 달라진 것을 확인할 수 있었다.
이러한 변화는 새로운 HTML 문서를 불러오는 전통적인 페이지 이동 방식에서 나타날 수 있다.


## 내일 계획 & 아직 모르는 것
- 내일부터 FE에 대한 수업을 시작한다. HTML, CSS, JavaScript가 어떤 역할을 하는지 정도는 이해한 것 같다. 하지만 각각의 역할을 넘어 어떻게 동작하고, 서로 어떤 방식으로 연결되어 웹을 구성하는지에 대한 나의 이해도는 아직 부족하다.
