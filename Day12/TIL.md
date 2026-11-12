# [Day 12] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-12
과목: FE

## 오늘 학습한 주제
- React의 API 요청 상태 관리
- `useEffect`를 활용한 데이터 재요청과 오류 처리

## 오늘 배운 것

### 1. API 요청 상태 구분하기

프로젝트에서 사용자의 식재료 목록을 API로 불러오는 기능을 구현했다.

기존에는 API 요청이 실패해도 빈 배열로 처리했기 때문에 실제로 식재료가 없는 것인지, 데이터를 불러오지 못한 것인지 구분할 수 없었다.

이를 해결하기 위해 API 요청 상태를 세 가지로 구분했다.

- `loading`: 데이터를 불러오는 중
- `done`: 데이터 요청 성공
- `error`: 데이터 요청 실패

이렇게 구분하면 요청이 실패했을 때 사용자에게 오류 메시지와 '다시 시도' 버튼을 보여줄 수 있다.

### 2. useEffect를 이용한 API 재요청

```jsx
const [attempt, setAttempt] = useState(0);

useEffect(() => {
  let ignore = false;

  setStatus("loading");

  getMyIngredients()
    .then((result) => {
      if (!ignore) {
        setNames(result);
        setStatus("done");
      }
    })
    .catch(() => {
      if (!ignore) setStatus("error");
    });

  return () => {
    ignore = true;
  };
}, [isLoggedIn, attempt]);
```

`useEffect`는 의존성 배열에 있는 값이 변경되면 다시 실행된다.

여기서는 `attempt` 값이 변경되면 API를 다시 호출하도록 구현했다.

```jsx
const reload = useCallback(
  () => setAttempt((n) => n + 1),
  []
);
```

'다시 시도' 버튼을 누르면 `attempt` 값이 증가하고, `useEffect`가 다시 실행되면서 데이터를 요청한다.

또한 `ignore` 변수를 사용하여 컴포넌트가 언마운트되거나 이전 Effect가 정리된 후 도착한 응답이 상태를 변경하지 않도록 처리했다.

## 어려웠던 점 & 해결 과정

PI 데이터를 불러오기 전에 식재료를 추가하면 중복으로 등록될 수 있는 문제가 있었다. 데이터 로딩이 완료된 후에만 추가할 수 있도록 조건을 수정했다.

팀 프로젝트 3일 차인데 아직 오류가 발생했을 때 원인을 파악하고 해결하는 트러블슈팅 능력이 부족하다고 느꼈다. 

## 내일 계획 & 아직 모르는 것

내일 오전까지 팀 프로젝트의 남은 작업을 모두 마무리하고 배포할 예정이다.

배포 전 기능들이 정상적으로 동작하는지 최종 점검하고, 오류가 발생하면 원인을 직접 분석하고 해결해 볼 계획이다.
