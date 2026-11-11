# [Day 11] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-11  
과목: FE

## 오늘 학습한 주제
- Optimistic Update (낙관적 업데이트)

## 오늘 배운 것

어제부터 팀 프로젝트를 진행하고 있다. 내가 맡은 부분은 Feed 페이지로, 좋아요와 북마크 버튼을 클릭해도 state만 변경되고 API는 호출되지 않는 문제가 있었다. 이를 해결하는 과정에서 **Optimistic Update**에 대해 알게 되었다.

### Optimistic Update란?

서버 응답을 기다리지 않고 **UI를 먼저 변경한 뒤 API를 호출하는 방식**이다. 요청이 성공하면 변경된 상태를 유지하고, 실패하면 이전 상태로 되돌린다.

<img width="672" height="532" alt="Optimistic Update" src="https://github.com/user-attachments/assets/007be23f-9e4a-4e2f-aec2-3a2c34ec3ae4" />

```text
클릭 → UI 먼저 변경 → API 호출
                       ├─ 성공: 상태 유지
                       └─ 실패: 이전 상태로 복구
```

### 구현 시 주의사항

- **상태값 미리 계산:** 클릭 시 다음 상태값을 정해 API 호출과 상태 복구에 사용한다. `setState` 콜백 내부에서 API를 호출하면 StrictMode에서 중복 요청이 발생할 수 있다.
- **중복 클릭 방지:** 연속 클릭으로 POST와 DELETE 요청이 꼬이지 않도록 `useRef(new Set())`으로 요청 중인 버튼을 관리했다.
- **POST/DELETE 처리:** 다음 상태에 따라 요청을 구분했다.

```javascript
const toggle = (url, on) =>
  on ? api.post(url) : api.delete(url);
```

### 테스트 방법

개발자 도구의 **Network 탭 → Offline**으로 변경한 뒤 좋아요 버튼을 클릭한다. UI가 먼저 변경되었다가 API 요청 실패 후 이전 상태로 돌아오는지 확인할 수 있다.

## 어려웠던 점 & 해결 과정

처음에는 `useState`로 화면의 상태만 변경하면 되는 줄 알았다. 하지만 실제 서버 데이터와 UI 상태를 일치시키는 것이 중요하다는 것을 알게 되었다. 특히 API 요청 실패 시 상태 복구와 중복 요청 방지가 필요하다는 점을 배웠다.

## 내일 계획 & 아직 모르는 것

- 여러 API 요청이 동시에 발생할 때 상태를 관리하는 방법은 아직 익숙하지 않다. Feed 페이지의 API 연동을 진행하면서 더 공부할 예정이다.
