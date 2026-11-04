[Day 07] LG CNS AM Inspire Camp 7기 TIL

작성일: 2026-11-04
과목: FE

## 오늘 학습한 주제
- NextAuth를 이용한 사용자 인증

- OAuth를 이용한 소셜 로그인


## 오늘 배운 것 
# NextAuth란?


- NextAuth는 Next.js에서 사용자 인증을 구현할 수 있도록 도와주는 라이브러리이다. 로그인과 로그아웃, 세션 관리 등의 기능을 제공한다.

- 오늘 수업에서는 전에 DB에 입력해 놓은 것(email과 비밀번호)와 kakao developers, google cloud를 이용한 OAuth로그인 방식을 학습하였다.

## OAuth 설정

- Kakao와 Google 소셜 로그인을 사용하기 위해서는 각 개발자 플랫폼에 가입하고 애플리케이션을 등록해야 한다.
- 애플리케이션을 등록하면 인증에 필요한 Client ID와 Client Secret 등을 발급받거나 확인할 수 있다. 또한 인증이 완료된 후 돌아올 Redirect URI를 등록해야 한다.


## OAuth 인증 과정

<img width="392" height="247" alt="image" src="https://github.com/user-attachments/assets/69e596a4-d608-4898-b79f-8c50bfe639c4" />



- 오늘 사용한 Google과 Kakao 로그인은 다음 과정을 거친다.

- 사용자가 소셜 로그인 버튼을 클릭하면 signIn("google") 또는 signIn("kakao")가 실행된다.

- 해당 서비스의 인증 페이지로 이동한다.

- 인증이 완료되면 NextAuth의 Callback URL로 돌아온다.

- NextAuth가 인가 코드를 토큰으로 교환하고 사용자 정보를 가져온다.

- jwt() Callback에서 토큰 정보를 저장한다.

## 어려웠던 점 

- 처음에는 JWT를 사용하기 때문에 크롬에서 로그인하면 사파리에서도 로그인 상태가 유지될 것이라고 생각했다. 하지만 NextAuth는
  JWT 기반 세션을 쿠키에 저장하고, 브라우저마다 쿠키를 별도로 관리하기 때문에 로그인 상태가 자동으로 공유되지 않는다는 것을 알게 되었다. 다만 동일한 계정으로 각각 로그인하는 것은 가능하며,
  카카오 자체의 로그인 세션이 유지되고 있다면 별도의 비밀번호 입력 없이 로그인할 수도 있다는 점을 알게 되었다.

## 내일 계획 

내일은 Next.js의 Fetch와 Cache에 대해 학습할 예정이다.
