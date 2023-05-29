Clean-Code_week1_yerimi11

[코드의 존재]  
앞으로 프로그래밍 언어에서 추상화 수준은 점차 높아지리라 예상된다.  
어떤 언어를 사용하든 코드는 기계가 이해하고 실행할 정도로 엄밀, 정확, 상세, 정형화 되어야 한다.  
제대로 명시한 요구사항은 코드만큼 정형적이며, 테스트 케이스로 사용해도 좋다.  
  
[재설계]  
일단 일정에 맞춰 급하게 짜고 나중에 리팩토링..? 나중은 결코 오지 않는다.  
새 시스템이 기존 시스템 기능을 100% 제공하지 않는 한 관리층은 기존 시스템을 대체하지 않을 것이다.  
-> 시간을 들여 클린코드를 만드는 노력이 비용 절감 뿐만 아니라 전문가로서 살아남는 길이다.  
  
[클린 코드?]  
의존성을 최대한 줄여야 유지보수가 쉬워진다. 오류는 명백한 전략에 의거해 철저히 처리한다.  
효율은 단순히 속도만을 뜻하지 않는다. CPU 자원을 낭비하는 코드도 우아하지 못하다.  
철저한 오류 처리? -> 메모리 누수, 경쟁 상태(race condition), 일관성 없는 명명법 등의 오류 처리에서 대충 넘어가면 안된다.  
  
설계자의 의도를 숨기지 않는다. 명쾌한 추상화, 단순한 제어문으로 가득하다.  
  
작성자가 아닌 사람도 읽고 고치기 쉬우며, 단위 테스트 케이스, 인수 테스트 케이스가 존재한다.  
의존성은 최소이며, 각 의존성을 명확히 정의한다. API는 명확하며 최소로 줄인다.  
읽기 쉬운 코드와 고치기 쉬운 코드는 다르다.  
테스트 케이스가 없는 코드는 클린 코드가 아니다.  
  
클린 코드는 주의 깊게 작성한 코드이며, 시간을 들여 깔끔하고 단정하게 정리한 코드다. 세세한 사항까지 꼼꼼하게 신경쓰고, 주의를 기울인 코드이다.  
  
단순한 코드 규칙으로 구현을 시작한다. (중요도 순)  
-> 모든 테스트를 통과한다 / 중복이 없다 / 시스템 내 모든 설계 아이디어를 표현한다 / 클래스, 메서드, 함수 등을 최대한 줄인다.  
중복: 같은 작업을 여러 차례 반복한다면 코드가 아이디어를 제대로 표현하지 못한다는 증거다. 중복을 피하라. 한 기능만 수행하라, 제대로 표현하라, 작게 추상화하라.  
집합에서 항목 찾기: 해시 맵 등, 추상 메서드나 추상 클래스를 만들어 실제 구현을 감싼다. (p.14)  
  
읽으면서 짐작한 대로 돌아가는 코드가 클린 코드다.  
  
[의미있는 구분]  
읽는 사람이 차이를 알도록 이름을 지어라.  
검색하기 쉬운 이름을 사용해라. ex) 숫자 7, 문자 e 등은 검색하기 어렵다. 변수명을 지어서 사용해라.  
  
[인코딩을 피하라]  
과거 윈도C API는 모든 변수가 정수 핸들, long 포인터, void 포인터 등 당시 컴파일러가 타입을 점검하지 않아 프로그래머에게 타입을 기억할 단서가 필요했다.  
요즘 나오는 프로그래밍 언어는 훨씬 많은 타입을 지원하고, 또한 컴파일러가 타입을 기억하고 강제한다.  
  
[작게 만들어라]  
함수를 만드는 첫번 째 규칙은 '작게', 두 번째 규칙은 '더 작게'이다.  
함수는 한 가지를 해야 한다. 그 한 가지를 잘 해야 한다. 그 한 가지만을 해야 한다.  
함수 당 추상화 수준은 하나로 한다.  
내려가기 규칙: 한 함수 다음에는 추상화 수준이 한 단계 낮은 함수가 오게 한다.  
  
[오류 코드보다 예외를 사용해라]  
Try/Catch 블록은 별도 함수로 뽑아내라  
오류를 처리하는 함수는 오류만 처리하게 한다.  
  
[함수를 짜는 방법]  
처음에는 길고 복잡한게 당연하다. 하지만 그 서투른 코드를 빠짐없이 테스트하는 단위 테스트 케이스를 만든다.  
그 다음 코드를 다듬고, 함수를 만들고, 이름을 바꾸고, 중복을 제거한다. 메서르를 줄이고 순서를 바꾼다. 전체 클래스를 쪼개기도 한다. 이 와중에도 코드는 항상 단위 테스트를 통과한다.  
  