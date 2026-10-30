# [Day 04] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-10-30
과목: FE

## 오늘 학습한 주제
- React useState와 Next.js searchParams의 렌더링 차이
  
## 오늘 배운 것 
- useState는 컴포넌트 내부에서 상태를 관리하고, searchParams는 URL에 있는 값을 가져온다.

## React - useState
<img width="438" height="118" alt="image" src="https://github.com/user-attachments/assets/299725cb-c7f3-4330-911a-61bbc1b82273" />
- 버튼을 클릭하면 setPage()를 통해 상태가 변경된다.
- 상태가 변경되면 React가 브라우저에서 컴포넌트를 다시 렌더링한다.
- URL은 변경되지 않으며, 새로고침하면 일반적으로 초기값으로 돌아간다.

## Next.js - searchParams
<img width="500" height="40" alt="image" src="https://github.com/user-attachments/assets/1396f01e-a062-4f48-9f6b-2adb7b133a41" />
- searchParams는 URL의 쿼리 문자열에서 값을 가져온다.
- 예를 들어 /feed?page=2&limit=10이라면 page는 "2", limit는 "10"이 된다.

<img width="692" height="76" alt="image" src="https://github.com/user-attachments/assets/2ac48553-64a3-45e6-aaeb-4d16ba475795" />
- 버튼을 클릭하면 router.push()를 통해 URL이 변경된다.
- 변경된 URL을 바탕으로 Next.js 서버 컴포넌트가 새로운 결과를 생성하고 브라우저가 화면을 갱신한다.
- 전체 페이지를 새로고침하지 않고 이동할 수 있으며, URL에 값이 남아 있어 새로고침해도 페이지 번호가 유지된다.
  
## 어려웠던 점 & 해결 과정
- 처음에는 useState와 searchParams가 모두 페이지 번호를 변경하고 화면을 업데이트하기 때문에 차이를 이해하기 어려웠다.
- 하지만 실제  코드를 비교하면서 useState는 브라우저에서 상태를 변경하여 리렌더링하고, 이번 Next.js 예제에서는 URL을 변경하여 서버에서 새로운 렌더링 결과를 가져온다는 차이를 조금 이해한 것 같다.

## 내일 계획 & 아직 모르는 것
- 아직 useState와 searchParam의 작동방식을 완전히 이해하지는 못했다. 주말동안 학습이 더 필요해 보인다.
