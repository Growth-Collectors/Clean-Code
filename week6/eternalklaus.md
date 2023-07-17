### JUnit 들여다보기
- 의도를 명확히 드러내려면 조건문을 캡슐화해라
  - `if (shouldNotCompact())`
- 부정문은 긍정문보다 이해하기 약간 더 어렵다. 그러므로 if를 긍정으로 만들어 조건을 반전한다.
- 숨겨진 시간적인 결합hidden temporal coupling이 존재한다. 시간 결합을 노출하려면 파라미터로 넘겨라.
<img width="810" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/b348871e-8b46-4a3f-9bc5-7939f968e659">

### SerialDate 리팩터링
- SerialDate라는 이름은 구현을 암시하는데 실상은 추상 클래스다. 구현을 암시할 필요가 전혀 없다. 그냥 Date가 좋다.
- 두 번째 getMonths를 호출하는 메서드는 첫 번째 getMonths뿐이다. 그래서 두 메서드를 하나로 합쳐 아주 단순화했다.
- 명명
  - addDays(Days 객체를 변경한다고 받아들여짐)
  - plusDays(Days가 더해진 새로운 객체를 리턴함)
- 보이스카우트 규칙: 체크아웃한 코드보다 좀 더 깨끗한 코드를 체크인


### 냄새와 휴리스틱
주석
1. 부적절한 정보
2. 쓸모없는 주석 - 쓸모 없어진 주석은 재빨리 삭제하는 편이 가장 좋다
3. 중복된 주석 - 코드만으로 충분한데 구구절절 설명하는 주석
4. 주석 처리된 코드 - 코드는 그 자리에 남아 매일매일 낡아간다. 주석으로 처리된 코드를 발견하면 즉각 지워버려라

환경
1. 한 명령으로 빌드가 끝나야 함
2. 모든 단위 테스트는 한 명령으로 돌려야 함

함수
1. 너무 많은 인수 - 인수는 작을수록 좋다
2. 출력 인수는 없어야 한다. 뭔가 상태를 변경해야 한다면 (출력을 하지 말고)함수에서 객체자체를 바꿔라

일반
1. 경계 조건 - 모든 경계 조건을 테스트하는 테스트 케이스를 작성하라
2. 중복 - 코드에서 중복을 발견할 때마다 추상화할 기회로 간주하라. 중복된 코드를 하위 루틴이나 다른 클래스로 분리하라.
  - [미묘한 유형의 중복] switch/case, if/else로 똑같은 조건을 거듭 확인 -> **다형성**으로 대체하라
  - [미묘한 유형의 중복] 알고리즘이 유사하나 코드가 서로 다른 중복 -> **template method**패턴이나 **strategy패턴**으로 중복을 제거하라
3. 추상화 수준이 올바르지 못하다 - 모든 저차원 개념은 파생클래스에 넣고, 모든 고차원 개념은 기초클래스에 넣는다
  - 세부구현과 관련된 상수,변수는 파생클래스에 넣어라
4. 과도한 정보
  - 잘 정의된 모듈은 인터페이스가 아주 작, 많은 함수를 제공하지 않고, 결합도coupling이 낮다
5. 기능 욕심
  - 클래스는 자기 클래스의 변수와 함수에 관심을 가졍지 다른 클래스의 변수와 함수에 관심을 가져서는 안된다.
  - 메서드가 다른 객체의 참조자와 변경자를 사용해 그 객체 내용을 조작한다면, 메서드가 그 객체 클래스의 범위를 욕심내는 탓이다.