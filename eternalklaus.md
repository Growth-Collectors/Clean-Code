### 주석
- 주석은 순수하게 선하지못하다
- 그러므로 주석이 필요한 상황에 곰곰이 생각하기 바란다. 주석대신 코드로 의도를 표현할 방법은 없을까?
  ```
  // 직원에게 복지혜택을 받을 자격이 있는지 검사한다
  if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
  ```
  ```
  if (employee.isEligibleForFullBenefilts())
  ```
- 괜찮은 주석
  - 의도를 설명하는 주석
  - <img width="758" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/fbd5e6e5-2f9e-49bb-911b-994ce3a6df3a">
  - 의미를 명료하게 밝히는 주석
  - <img width="565" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/3009943d-eb54-41e2-894e-9381a5286bc1">

### 형식 맞추기
- 세로 밀집도
  - 서로 밀접한 코드 행은 세로로 가까이 놓아야 한다
  - <img width="695" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/1360c9d4-0a6c-4084-8466-9178e283b5c2">
  - 서로 밀접한 개념은 한 파일에 속해야 한다. 이게 바로 protected변수를 피해야 하는 이유 중 하나다. 
- 변수 선언
  - 로컬 변수: 변수는 사용하는 위치에 최대한 가까이 선언한다
  - <img width="410" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/e95914ce-759e-4560-b0c7-c4a0b0f4554c">
  - 인스턴스 변수: 클래스 맨 처음에 선언한다. 잘 설계한 클래스는 클래스 메서드가 인스턴스 변수를 사용하기 때문이다. 
- 종속 함수
  - A가 B를 호출하면 A를 먼저 배치한다. (+두 함수는 세로로 가까이 배치한다.)
  - 그러면 소스 모듈이 고차원에서 저차원으로 자연스럽게 내려간다. 
- 가로 공백과 밀집도
  - 밀접한 개념과 느슨한 개념을 표현한다
  - <img width="473" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/2f68f5eb-8c8d-4411-9b21-c9f753aab94f">
- 변수가 너무 많다면? (= 클래스의 선언부가 너무 길다)
  - 클래스를 쪼개야 한다는 의미

### 객체와 자료구조
- 객체
  - 추상화 뒤로 자료를 숨기고, 자료를 다루는 함수만 공개함
  - 함수추가 어려움 (ex. 도형객체들에 함수 추가할땐 모든 객체에 추가해 줘야...)
- 자료구조
  - 자료를 그대로 투명하게 공개, 별다른 함수는 제공안함
  - 함수추가 쉬움 (자료구조 사용하는 **절차**만 수정하면됨)
- (참고) 객체는 함수추가가 어렵지만 Visitor 패턴, Durl-patch기법을 사용하면 쉽게 가능
  - Visitor패턴: 객체의 데이터와 함수를 분리시켜 함수를 수정하지 않고도 새로운 함수를 객체에 추가 가능함
  - Dual-patch: ?
- 디미터 법칙
  - "모듈은 자신이 조작하는 객체의 속사정을 몰라야 한다"
  - <img width="572" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/b73425df-6a88-45c8-96e9-b1c8adef93d2">
  - 디미터 법칙을 위반함 (객체라면) 너무 많은 객체를 탐색할 줄 안다는 것...
  - <img width="566" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/fe7ac428-794e-4b31-af01-2b5ddad03cd3">
  - 디미터 법칙을 위반하지 않음 (자료구조라면)
  - <img width="800" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/3395eea7-5bd2-4618-b1d0-c97de2109e05">
  - 디미터 법칙을 위반하지 않음 (목적을 파악하고 함수화함)
- 잡종 구조
  - 때때로 절반은 객체, 절반은 자료구조인 잡종 구조가 나온다
  - ex) 공개 조회/설정 함수가 잡종일 경우, 비공개 변수를 그대로 노출한다. 
