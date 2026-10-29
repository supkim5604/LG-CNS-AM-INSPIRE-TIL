# [Day 01] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-10-29
과목: FE

## 오늘 학습한 주제
- Atomic Design Pattern

## 오늘 배운 것 
- Atomic Design은 화학에서 원자들이 결합해 분자를 만들고, 분자들이 결합해 더 복잡한 구조를 만드는 개념에서 시작됐다.

  
 <img width="872" height="314" alt="스크린샷 2026-10-29 19 59 56" src="https://github.com/user-attachments/assets/b3bd409d-eb5b-46d9-870c-845019c9f60e" />
 > 이미지 출처: [Brad Frost - Atomic Design, Chapter 2](https://atomicdesign.bradfrost.com/chapter-2/)<br>
<br>


 - atomic design pattern을 제안한 Brad Frost의 설명에 따르면 atomic design은 linear 적인 과정이 아니라, 사용자 인터페이스를 하나의 응집력 있는 집합체로 볼 수 있도록 설계되었다.


1. 먼저 Atoms 즉 원자는 더 이상 분해 할 수 없는 단계를 의미 한다. 기본적인 HTML 요소들이 포함된다고 볼 수 있다.
2. Molecules, 분자는 여러 원자가 결합하여 각기 다른 성질을 지닌 원자들의 집합체이다.
3. Oranisms, 유기체는 분자, 원자 혹은 또 다른 유기체의 그룹이다.
4. Templates은 페이지 수준의 객체로, 레이아웃에 구성 요소를 배치하가고 디자인의 구조를 명확하게 정의하는 단계이다.
5. Page는 사용자가 보게 될 최종 인터페이스라고 볼 수 있다. 가장 중요한 단계이며 모든 Atomic design의 결과물이다. 

## 프로젝트에 적용된 Atomic Design

<img width="264" height="385" alt="스크린샷 2026-10-29 20 12 14" src="https://github.com/user-attachments/assets/7986526b-60c5-41ea-9898-460f96908bdc" />




- Atoms
    - Button.tsx, CustomTitle.tsx, LogoImage.tsx 등 가장 작은 단위의 UI 컴포넌트들이 포함되어 있다. 예를 들어 버튼을 별도의 컴포넌트로 만들어 두면 다른 페이지에서도 동일한 버튼을 재사용할 수 있다.


- Molecules
    - DesktopNavigation.tsx, LogoItem.tsx 등이 포함되어 있다. Atoms 단계에서 만든 컴포넌트들을 조합하여 하나의 기능을 수행하도록 구성하는 단계이다. 

- Organisms
    - GlobalNavigation.tsx, HeroSwiperBanner.tsx 등이 포함되어 있다. 여러 Molecules와 Atoms를 조합하여 내비게이션이나 메인 배너와 같은 복잡한 UI 영역을 구성할 수 있다.

- Templates
    - Header.tsx, HeroSection.tsx, AboutSection.tsx 등이 포함되어 있다. 이러한 컴포넌트를 이용하여 페이지의 각 영역을 구성하고 레이아웃을 정의할 수 있다.

- Pages
  - Next.js의 app/(main)/page.tsx 파일에서 실제 페이지를 구성할 수 있다. Next.js는 파일 기반 라우팅을 사용하기 때문에 page.tsx가 특정 URL에 대응하는 페이지 역할을 한다.


## 어려웠던 점 & 해결 과정 
 - Atoms, Molecules, Organisms의 차이를 명확하게 구분하기 어려웠다. 특히 Molecules와 Organisms 모두 여러 컴포넌트를 조합한다는 점에서 어떤 기준으로 나누어야 하는지 헷갈렸다. 프로젝트의 폴더 구조를 통해 각 단계의 역할을 조금 더 이해할 수 있었다. 단순히 컴포넌트의 크기가 아니라 어떤 기능과 역할을 담당하는지에 따라 구분해야 한다는 것을 알게 되었다.

## 내일 계획 & 아직 모르는 것
 - Atomic Design의 개념은 대략적으로 이해했지만, 실제로 컴포넌트를 설계할 때 어느 단계로 분류해야 하는지는 아직 감이 잡히지 않는다. 또한, 실제 컴포넌트 코드를 살펴보면서 props를 통해 데이터를 전달하고 컴포넌트를 조합하는 과정에 대해 공부가 필요해 보인다.

   
