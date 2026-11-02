# [Day 05] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-02
과목: FE

## 오늘 학습한 주제
- Next 에서 Client Componet, Server Action

## 오늘 배운 것 
- Client Component
  - Client Component는 브라우저에서 사용자와의 상호작용을 처리하는 컴포넌트이다. 파일 상단에 "use client"를 선언하여 사용한다.
    useState, useEffect와 같은 React Hook을 사용할 수 있다.  FormField.tsx에서는 useState를 사용하여 비밀번호 표시 여부를 관리하였다.

    
    
  <img width="366" height="22" alt="image" src="https://github.com/user-attachments/assets/a675955b-d98e-43e3-847a-fa078d1b8e86" />


   - setIsVisible()로 상태가 변경되면 컴포넌트가 다시 렌더링되어 비밀번호 표시 여부가 변경된다.

- Server Action
  - Server Action은 서버에서 실행되는 비동기 함수이다. 함수 내부에 "use server"를 선언하여 사용할 수 있다. 폼 데이터를 전달받아 서버에서 처리하거나 DB 작업을 수행할 때 사용할 수 있다.
  page.tsx에서는 FormData를 통해 로그인 정보를 전달받았다.


  <img width="564" height="136" alt="image" src="https://github.com/user-attachments/assets/cf299f01-7b87-4748-82e4-d2dd34a7c840" />


   - handleSubmit을 LoginSection에 전달하여 폼 제출 시 서버에서 실행되도록 하였다.


- 비교

  
  <img width="619" height="217" alt="image" src="https://github.com/user-attachments/assets/6cf71b6f-7004-44fc-8cc9-7a850e14067f" />


## 어려웠던 점 & 해결 과정
- 처음에는 Client Component와 Server Action이 각각 어떤 역할을 하는지 헷갈렸다. 실제 로그인 폼 코드를 비교하면서 Client Component는 사용자와의 상호작용을 담당하고, Server Action은 전달받은 데이터를 서버에서 처리한다는 차이를 이해하였다.
