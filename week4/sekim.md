## `chapter` **11장 시스템**

---

- 책임이 둘이라는 말은 메서드가 작업을 두 가지 이상 수행한다는 의미다. 즉, 작게나마 단일 책임 원칙을 깬다는 말이다.
- 의존성 주입
제어 역전에서는 한 객체가 맡은 보조 책임을 새로운 객체에게 전적으로 떠넘긴다. 새로운 객체는 넘겨받은 책임만 맡으므로 단일 책임 원칙을 지키게 된다.
- 확장
성장할지 모른다는 기대로 자그만 마을에 6차선을 뚫는데 들어가는 비용을 정당화할 수 있을까? 아니, 어느 조그만 마을이 6차선을 반길까?
’처음부터 올바르게’ 시스템을 만들 수 있다는 믿음은 미신이다. 대신에 우리는 새로운 스토리에 맞춰 시스템을 조정하고 확장하면 된다. 이것이 반복적이고 점진적인 애자일 방식의 핵심이다. 테스트 주도 개발, 리팩터링 깨끗한 코드는 코드 수준에서 시스템을 조정하고 확장하기 쉽게 만든다.
- DTO에는 메서드가 없으며 사실상 구조체다. 즉, 동일한 정보를 저장하는 자료 유형이 두 개라는 의미다. 그래서 한 객체에서 다른 객체로 자료를 복상하는 반복적인 규격 코드가 필요하다.
- 좋은 API는 걸리적거리지 않아야 한다. 그래야 팀이 창의적인 노력을 사용자 스토리에 집중한다. 그리하지 않으면 아키텍처에 발이 묶여 고객에게 최적의 가치를 효율적으로 제공하지 못한다.
- 의사 결정을 최적화하라
우리는 때때로 가능한 마지막 순간까지 결정을 미루는 방법이 최선이라는 사실을 까먹곤 한다. 게으르거나 무책임해서가 아니다. 최대한 정보를 모아 최선의 결정을 내리기 위해서다. 성급한 결정은 불충분한 지식으로 내린 결정이다. 너무 일찍 결정하면 고객 피드백을 더 모으고, 프로젝트를 더 고민하고, 구현 방안을 더 탐험할 기회가 사라진다.
- 하지만 때로는 표준을 만드는 시간이 너무 오래 걸려 업계가 기다리지 못한다. 어떤 표준은 원래 표준을 제정한 목적을 잊어버리도 한다.
- 시스템을 설계하든 개별 모듈을 설계하든, 실제로 돌아가는 가장 단순한 수단을 사용해야 한다는 사실을 명심하자.

<aside>
💡 ‘처음부터 올바르게’ 만들기 위해, 상사분들에게 빠른 의사 결정을 요구했던 제 모습이 생각났습니다. 
그러다보니 이미 결정된 사항이 변경되면 스트레스를 받았는데, 이 글을 읽고 처음부터 제대로 만드는 것도 좋지만, 일단 만들어보고 조금씩 확장해보자!라고 생각이 바뀌었습니다. 결론은 TDD 배워보자 ^.ㅜ

</aside>

## `chapter` **12장 창발성(創發性)**

---

- 켄트 벡은 다음 규칙을 따르면 설계는 ‘단순하다’고 말한다.
- 모든 테스트를 실행한다.
- 중복을 없앤다.
- 프로그래머의 의도를 표현한다.
- 클래스와 메서드 수를 최소로 줄인다.
- 코드를 변경하면서 버그의 싹을 심지 않으려면 유지보수 개발자가 시스템을 제대로 이해해야 한다. 하지만 시스템이 점차 복잡해지면서 유지보수 개발자가 시스템을 이해하느라 보내는 시간은 점점 늘어나고 동시에 코드를 오해할 가능성도 점점 커진다. 그러므로 코드는 개발자의 의도를 분명히 표현해야 한다.
- 우선, 좋은 이름을 선택한다. 이름과 기능이 완전히 딴판인 클래스나 함수로 유지보수 담당자를 놀라게 해서는 안 된다.
- 하지만 나중에 코드를 읽을 사람은 바로 자신일 가능성이 높다는 사실을 명심하자.
- 함수를 여럿으로 나누고, 자신의 작품에 조금만 더 주의를 기울이자. 주의는 대단한 재능이다.

<aside>
💡 미래의 내가 고통받지 않는 방법 = 의도를 분명히 표현하자

</aside>

## `chapter` **13장 동시성**

---

- 동시성을 구현해도 설계는 변하지 않는다. 
단일 스레드 시스템과 다중 스레드 시스템은 설계가 판이하게 다르다. 일반적으로 무엇과 언제를 분리하면 시스템 구조가 크게 달라진다.
- 스레드 환경에 안전한 컬렉션
java.util.concurrent 패키지가 제공하는 클래스는 다중 스레드 환경에서 사용해도 안전하며, 성능도 좋다.
- 식사하는 철학자들
- 자바 언어는 개발 메서드를 synchronized라는 개념을 지원한다. 하지만 공유 클래스 하나에 동기화된 메서드가 여럿이라면 구현이 올바른지 다시 한 번 확인하기 바란다.
- 동기화하는 부분을 작게 만들어라
    
    자바에서 synchronized 키워드를 사용하면 락을 설정한다. 같은 락으로 감싼 모든 코드 영역은 한 번에 한 스레드만 실행이 가능하다. 락은 스레드를 지연시키고 부하를 가중시킨다. 그러므로 여기저기 synchronized문을 남발하는 코드는 바람직하지 않다. 반면, 임계영역은 반드시 보호해야 한다. 따라서 코드를 짤 때는 임계 영역 수를 최대한 줄여야 한다.
    

<aside>
💡 [자바의 정석 - Chapter 13. 쓰레드 정리한 링크](https://dev-seongeun.notion.site/Chapter-13-95103c98fca64867a51eb70cfaa6f622?pvs=4)를 공유해요. 
관심 있으신 분들은 13-30 쓰레드의 동기화(synchronization) 부분을 참고하면 좋을 거 같습니다.

</aside>