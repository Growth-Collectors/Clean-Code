## `**chapter**` **4장 주석**

---

- 사실상 주석은 기껏해야 필요악이다. 프로그래밍 언어 자체가 표현력이 풍부하다면, 아니 우리에게 프로그래밍 언어를 치밀하게 사용해 의도를 표현할 능력이 있다면, 주석은 거의 필요하지 않으리라. 아니, 전혀 필요하지 않으리라
- 주석은 언제나 실패를 의미한다. 때때로 주석 없이는 자신을 표현할 방법을 찾지 못해 할 수 없이 주석을 사용한다. 그래서 주석은 반겨 맞을 손님이 아니다.
- 주석은 지나친 참견이라 개발자가 주석을 무시하는 습관에 빠진다. 코드를 읽으며 자동으로 주석을 건너뛴다. 결국은 코드가 바뀌면서 주석을 거짓말로 변한다.
- 있으나 마나 한 주석을 달려는 유혹에서 벗어나 코드를 정리하라. 더 낫고, 행복한 프로그래머가 되는 지름길이다.
- 주석으로 처리한 코드만큼 밉살스러운 관행도 드물다. 주석으로 처리된 코드는 다른 사람이 지우기를 주저한다. 이유가 있어 남겨놓았으리라고, 중요하니까 지우면 안 된다고 생각한다. 그래서 질 나쁜 와인병 바닥에 앙금이 쌓이듯 쓸모 없는 코드가 점차 쌓여간다.
- 짧고 한 가지만 수행하며 이름을 잘 붙인 함수가 주석으로 헤더를 추가한 함수보다 훨씬 좋다.

<aside>
💡 틀린 주석보다 아무것도 없는 코드가 더 낫다는 생각을 했습니다.
그리고 너무 구체적인 주석보다 적당히 추상적인 주석이 좋은 거 같아요.
그래서 바로 이번 주에 만든 쓸데 없는 주석은 제거하였습니다. ㅎㅎ

</aside>

## `**chapter**` 5**장 형식 맞추기**

---

- 프로그래머라면 형식을 깔끔하게 맞춰 코드를 짜야 한다. 코드 형식을 맞추기 위한 간단한 규칙을 정하고 그 규칙을 착실히 따라야 한다. 팀으로 일한다면 팀이 합의해 규칙을 정하고 모두가 그 규칙을 따라야 한다. 필요하다면 규칙을 자동으로 적용하는 도구를 활용한다.
- 표 5-1이 우리에게 무엇을 말하느냐고? 500줄을 넘지 않고 대부분 200줄 정도인 파일도 커다란 시스템을 구축할 수 있다는 사실이다. 반드시 지킬 엄격한 규칙은 아니지만 바람직한 규칙으로 삼았으면 좋겠다. 일반적으로 큰 파일보다 작은 파일이 이해하기 쉽다.
- 신문 기사 처럼 작성하라 - 첫 문단은 전체 기사 내용을 요약한다. 세세한 사실은 숨기고 커다란 그림을 보여준다. 쭉 읽으며 내려가면 세세한 사실이 조금씩 드러난다. 기타 세부사항이 나온다. 이름은 간단하면서도 설명이 가능하게 짓는다. 소스파일 첫 부분은 고차원 개념과 알고리즘을 설명한다. 아래로 내려갈수록 의도를 세세하게 묘사한다. 마지막에는 가장 저차원 함수와 세부 내역이 나온다.
- 가능하다면 호출하는 함수를 호출되는 함수보다 먼저 배치한다. 그러면 프로그램이 자연스럽게 읽힌다. 규칙을 일관적으로 적용한다면 독자는 방금 호출한 함수가 잠시 후에 정의되리라는 사실을 예측한다.
- 가로정렬 - 위와 같은 정렬이 별로 유용하지 못하다는 사실을 깨달았다. 코드가 엉뚱한 부분을 강조해 진짜 의도가 가려지기 때문이다. 정렬이 필요할 정도로 목록이 길다면 문제는 목록 길이지 정렬 부족이 아니다.
- 팀은 한 가지 규칙에 합의해야 한다. 그리고 모든 팀원은 그 규칙을 따라야 한다. 그래야 소프트웨어가 일관적인 스타일을 보인다. 개개인이 따로국밥처럼 맘대로 짜대는 코드는 피해야 한다.
- 좋은 소프트웨어 시스템은 읽기 쉬운 문서로 이뤄진다는 사실을 기억하기 바란다. 스타일은 일관적이고 매끄러워야 한다. 한 소스 파일에서 봤던 형식이 다른 소스파일에도 쓰이리라는 신뢰감을 독자에게 줘야 한다. 온갖 스타일을 뒤섞어 소스 코드를 필요 이상으로 복잡하게 만드는 실수는 반드시 피한다.

<aside>
💡 eslint나 프리티어등과 같은 코드 포매터가 생각 났습니다. 
프리티어는 구성원 모두 같은 규칙으로 적용하는 게 좋은 거 같아요. 
규칙이 서로 다르면 변경하지 않은 코드에도 자동으로 줄바꿈 적용 되어서 커밋 내역 확인이 어려웠어요.

</aside>

## `**chapter**` **6장 객체와 자료 구조**

---

- 자료를 세세하게 공개하기보다는 추상적인 개념으로 표현하는 편이 좋다. 인터페이스나 조회/설정 함수만으로는 추상화가 이뤄지지 않는다. 개발자는 객체가 포함하는 자료를 표현할 가장 좋은 방법을 심각하게 고민해야 한다. 아무 생각 없이 조회/설정 함수를 추가하는 방법이 가장 나쁘다.
- 객체는 추상화 뒤로 자료를 숨긴 채 자료를 다루는 함수만 공개한다. 자료 구조는 자료를 그대로 공개하며 별다른 함수는 제공하지 않는다.
- 객체와 자료 구조는 근본적으로 양분된다. (중략) 다시 말해, 객체 지향 코드에서 어려운 번경은 절차적인 코드에서 쉬우며, 절차적인 코드에서 어려운 변경은 객체 지향 코드에서 쉽다.
- 디미터 법칙은 잘 알려진 휴리스틱으로, 모듈은 자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙이다. 객체는 자료를 숨기고 함수를 공개하다. 즉, 객체는 조회 함수로 내부 구조를 공개하면 안 된다는 의미다. 다시 말해, 낯선 사람은 경계하고 친구랑만 놀라는 의미다.
- 자료 전달 객체 - 자료 구초제의 전형적인 형태는 공개 변수만 있고 함수가 없는 클래스다. 이런 자료 구조체를 때로는 자료 전달 객체라 한다.DTO는 굉장히 유용한 구초에다. 특히 데이터베이스와 통신하거나 소켓에서 받은 메시지의 구문을 분석할 때 우용하다. 흔히 DTO는 데이터페이스에서 저장된 가공되지 않은 정보를 애플리케이션 코드에서 사용할 객체로 변환하는 일련의 단계에서 가장 처음으로 사용하는 구초제다.
- (어떤) 시스템을 구현할 때, 새로운 자료 타입을 추가하는 유연성이 필요하면 객체가 더 적합하다. 다른 경우로 새로운 동작을 추가하는 유연성이 필요하면 자료 구조와 절차적인 코드가 더 적합하다. 우수한 소프트웨어 개발자는 편견없이 이 사실을 이해해 직면한 문제에 최적인 해결책을 선택한다.

<aside>
💡 자료 구조에 대한 정의를 찾아봤습니다. 
클래스에 필드만 정의되고 메서드는 정의되지 않는 것을 의미하는가 싶었는데 검색해보니 클래스 자체가 임의의 데이터형을 자유로이 조합하여 만들 수 있는 **자료구조**라고 하네요! 자료 구조라고 해서 List, Map, Set만 떠올렸는데 클래스 자체가 자료 구조인 걸 알게 되었어요.

</aside>