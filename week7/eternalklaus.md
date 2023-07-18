
- 매직 숫자는 명명된 상수로 교체하라
- 조건을 캡슐화해라
<img width="801" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/f064cdb3-941e-4e5d-b9ac-16c52632c959">

- 일종의 연결소자를 생성해 시간적인 결합을 노출해라.
  - 함수가 복잡해진게 아니라, 의도적으로 추가한 구문적인 복잡성이 원래 있던 시간적인 복잡성을 드러낸 셈이다
<img width="810" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/2836bf76-5ff2-43d0-ad7d-590897693f60">

- 경계조건을 캡슐화해라
  - 플젝뿐만이 아니라 알고리즘 풀때도 필요한 스킬이라고 생각
<img width="810" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/ed2af97e-2c81-4188-839d-2f1f5802b4fa">

- 상수는 상속하지 말아라.
  - "참으로 끔찍한 광행이다! 상수를 상속 계층 맨 위에 숨겨놨다. 우엑!"
- 표준 명명법을 사용해라
  - Decorator 패턴을 활용한다면 클래스 이름에 Decorator를 붙여라
- 커버리지 도구를 사용해라
  - 대다수 IDE는 테스트커버리지를 시각적으로 표현한다. 테스트되는 행은 녹색으로, 테스트되지 않는 행은 붉은색으로 표시한다(써보신분...?)


### 동시성 II
- 시간도 테스트 가능하다는 점...
<img width="810" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/2958eb2c-a144-4418-9480-2a1c343e204c">

- I/O연산에 시간을 보낸다면 동시성이 성능으로 높여주기도 한다. 시스템 한쪽이 I/O를 기다리는 동안에 다른쪽이 뭔가를 처리해 노는 CPU를 효과적으로 활용할 수 있다.
- 4바이트 Integer할당 연산 = 원자적. 그러나 "JVM 명세에 따르면 64비트 값을 할당하는 연산은 32비트 값을 할당하는 연산 두 개로 나눠진다. 그러니까 첫 32비트 값을 할당한 직후에 그리고 둘째 32비트 값을 할당하기 직전에 다른 스레드가 끼어들어 두 32비트 값 중 하나를 변경할 수 있다는 의미다.
<img width="810" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/1b99057d-4e91-4e9e-8bbf-287294816b38">

- "1971년 그 추웠던 시카고 겨울에 나는 중요한 교훈을 배웠다. 클라이언트 기반 잠금 매커니즘은 진짜 사람이 할 짓이 아니다."
  - 대신 서버 기반 잠금을 사용
  - 서버코드에 손대지 못한다면? Adapter 패턴을 사용해 API를 변경한 후 잠금을 추가한다. 
