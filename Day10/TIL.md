# [Day 10] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-09
과목: FE

## 오늘 학습한 주제
- Pagination
- Infinite Scroll

## 오늘 배운 것 
# Pagination
- Pagination은 많은 데이터를 일정한 개수로 나누어 보여주는 방식이다. 사용자가 페이지 번호나 다음 버튼을 클리하면 해당 페이지의 데이터를 불러온다.<br>


# Infinite Scroll
- Infinite Scroll은 사용자가 스크롤을 내리면 다음 데이터를 자동으로 불러오는 방식이다. 인스타그램이나 SNS 피드에서 흔히 볼 수 있다.
  Pagination과 달리 페이지 번호를 클릭할 필요가 없으며, 기존 게시글 아래에 새로운 게시글이 추가된다.

  <img width="588" height="288" alt="image" src="https://github.com/user-attachments/assets/18304ef3-e2b1-4a4b-a8bb-9298ac1483ac" />
<br>
- IntersectionObserver는 특정 요소가 화면에 들어왔는지 감지하는 Web API이다. 목록 마지막에 위치한 요소가 화면에 보이면 다음 페이지를 요청하도록 하였다.
  여기서 router.replace()는 URL을 변경하지만 브라우저의 방문 기록을 새로 추가하지 않는다. 또한 { scroll: false }를 사용하여 페이지가 변경되어도 스크롤 위치가 초기화되지 않도록 하였다.

## 어려웠던 점 & 해결 과정
- 처음에는 Infinite Scroll이 Pagination은과 완전히 다른 방식으로 데이터를 가져온다고 생각했다. 하지만 실제 코드를 살펴보니 서버에서는 동일한 페이지 단위 API를 사용하고 있었다.
- Pagination은 현재 페이지의 데이터만 보여주는 반면, Infinite Scroll은 이전에 불러온 데이터들을 유지하면서 새로운 데이터를 추가한다는 차이가 있었다.

## 내일 계획 & 아직 모르는 것
- Pagination과 Infinite Scroll의 기본적인 동작 방식은 이해한 것 같다. 어떠한 방식이 더 나은 것이 아니라 클라이언트가 원하는 방향에 따라 선택하면 된다.
- 각각의 방식에 따른 서버에 부하가 얼마나 걸리는지, 게시글이 계속 추가될 경우 성능에 어떤 영향을 미치는지에 대해서도 추가적인 공부가 필요해 보인다.
