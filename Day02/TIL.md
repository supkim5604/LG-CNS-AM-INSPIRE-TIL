# [Day 01] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-10-28
과목: FE

## 오늘 학습한 주제
- useState

## 오늘 배운 것 
- useState

useState는 React에서 제공하는 Hook 중 하나로, 컴포넌트의 상태(State)를 관리할 때 사용한다. state란 컴포넌트가 가질 수 있는 상태를 의미한다. 


<img width="246" height="25" alt="image" src="https://github.com/user-attachments/assets/02a3efe1-c359-4e9c-b032-534d4ae4753c" />


- 초기값을 useState에 넣어주면 state 와 setState를 배열 형태로 리턴해 준다. 현재 상태 값은 state에 있다. state값을 변경해주고 싶을 때는  setState 함수를 이용해서 변경할 수 있다.
위 코드 count의 초기값은 0이며, setCount() 함수를 통해 변경 가능하다. 


<img width="353" height="257" alt="image" src="https://github.com/user-attachments/assets/19f98612-92c5-4fbb-9486-46238fcc4382" />


- 버튼을 클릭하면 숫자가 10 씩 증가하도록 해보았다. 위 코드를 보면 초기값은 0, setCount(count + 10)을 통해 버튼을 클릭하면 10씩 증가하도록 했다. 여기서 onClick은 클릭 이벤트를 처리하는 속성이다. 버튼을 클릭하면 화살표 함수가 실행되고, setCount를 호출하여 count + 10을 수행한다.
React는 상태 변경을 처리한 후 컴포넌트를 다시 렌더링하여 변경된 값을 화면에 반영한다. 기존 JavaScript에서는 DOM 요소를 직접 선택하고 값을 변경해야 했지만, React에서는 상태를 변경하면 화면에 자동으로 반영된다는 차이가 있었다.

## 주의 사항

<img width="164" height="61" alt="image" src="https://github.com/user-attachments/assets/370ca3b1-e5fd-43dd-ba93-0fab840d10e9" />


- 위 코드에서 count의 초기값이 0이라고 가정해 보자. setCount(count + 1)을 세 번 호출했으므로 count가 3이 될 것이라고 생각할 수 있다.
하지만 실제 결과는 1이다. React에서는 한 번의 렌더링 동안 count 값이 고정되어 있기 때문이다.


<img width="224" height="102" alt="스크린샷 2026-10-28 20 21 47" src="https://github.com/user-attachments/assets/c56f73dd-8c82-40fe-8e67-cc979848edae" />

- 여기서 prev는 React가 전달하는 이전 상태값을 의미한다.
함수형 업데이트를 사용하면 이전 업데이트의 결과를 다음 업데이트에 반영할 수 있다.
따라서 0 → 1 → 2 → 3 순서로 계산되어 최종적으로 count가 3이 된다.



## 내일 계획 & 아직 모르는 것

- 오늘은 useState를 활용하여 간단한 카운터를 구현하고, React에서 상태를 관리하는 방법을 학습하였다. 기본적인 사용법은 이해했지만, 상태가 변경되었을 때 React가 컴포넌트를 다시 렌더링하는 과정은 아직 명확하게 이해하지 못했다. 내일은 next 와 react 의 전체적인 차이를 공부할 예정이다.
