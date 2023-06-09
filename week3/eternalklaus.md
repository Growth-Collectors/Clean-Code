### 7. 오류 처리

- Try-Catch-Finally 문부터 작성하라
- unchecked 예외를 사용하라 
  - checked 예외는 반드시 예외처리를 해줘야 함
  - a -> b, b -> c를 부르는데 c가 checked 예외를 던지면 a, b 전부 예외를 잡기 위해 throws를 붙혀줘야 함
  - OCP 위반
- null을 반환하거나 null을 전달하지 마라

### 8. 경계 
- 경계 = 외부 코드를 내 코드에서 호출하는 부분
- "통제가 불가능한 외부 코드에 바로 의존하지 말고 중간에 경계 클래스를 두어 그 클래스에 의존하자."
- ex) 외부 라이브러리에서 준 Map을 그대로 사용한다면? Map의 스펙이 바뀔경우 우리 소스를 다 바꿔야 할지도 모른다. 
    - 경계 클래스를 만들어 외부 코드에서 리턴하는 값을 한번 안전하게 포맷팅(?)해주도록 한다
### 9. 단위 테스트
- FIRST 원칙
  -  Fast : 테스트는 빨라야 한다.
  -  **Independent** : 각 테스트는 서로 의존하면 안 된다. 의존 되어있으면 테스트가 연달아 실패하기 때문에 원인을 진단하기 어렵다.
  -  Repeatable : 어떤 환경에서든 반복가능해야 한다. local, QA, Staging, 운영 환경 어디서든 테스트가 돌아가야 한다
  -  Self-validating : 테스트는 bool 값으로 결과를 내야 한다. 성공 or 실패
  -  Timely : 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전(=적시)에 구현한다.
- 테스트 당 1개의 assert문을 사용
  - 이 테스트에서 어떤 걸 검증하려고 하는지 한눈에 파악하기 위함

### 10. 클래스
- 아래와 같은 순서로 코드 작성한다
  - 1) static 변수 : public -> protected -> package -> private
  - 2) instance 변수 : public -> protected -> package -> private
  - 3) 생성자
  - 4) 메서드 : (public -> private -> private) -> (public -> private -> private)...

- 클래스는 작아야 한다. 책임을 줄이자. 
  - SRP(단일 책임 원칙)
    - 클래스나 모듈을 변경할 이유가 하나 뿐이어야 한다는 원칙
  - 응집도를 낮게 유지하자
    - 응집도 = 모듈 내 요소들이 서로 관련되어 있는 정도
    - 모든 인스턴스 변수를 메서드마다 사용하는 클래스는 응집도가 가장 높다.
    - 모든 인스턴스 변수를 메서드마다 사용하는 클래스는 응집도가 가장 높다.
