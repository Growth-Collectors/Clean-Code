# 점진적인 개선

### 초기 Args 클래스 
<img width="1252" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/ad3cedd7-be8c-4d30-92de-64e3db13c833">

- 인스턴스 변수 갯수가 너무 많음
- 'TILT'같은 희한한 문자열
- 지저분한 코드들: HashSets, TreeSets, try-catch-catch 블록
- 만약 String, Integer타입처리가 추가된다면 is*SchemaElement, is*Arg, is*, ... 가 동일수준에서 추가되어야 함
  - 새 인수 유형을 추가하려면 주요 지점 세 곳(parse, get, set)에다 코드를 추가해야 한다는 사실을 이미 깨달았다.
- errorMessage메서드: 명백히 SRP(Single Responsibility Principle)위반이다. Args클래스가 오류 메시지 형식까지 책임지기 때문

### ArgumentMarshaler 
- 그래서 나는 TDD라는 기법을 사용했다. TDD는 언제 어느 때라도 시스템이 돌아가야 한다는 원칙을 따른다.
- 마샬링 = 메모리 -> (저장/전송에 적합한)데이터 형식으로 변환 = 직렬화와 유사함
<img width="934" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/95a23cbc-0dc2-42c6-b482-033d869b5fa4">

- 구체적으로 Boolean 인수를 저장하는 HashMap -> ArgumentMarshaler유형을 저장하는 HashMap
- Args.java에서 예외데이터(Null)여부를 검사 -> ArgumentMarshaler에서 검사
  - 각 인수유형을 처리하는 코드를 모두 ArgumentMarshaler 클래스에 넣고 나서 ArgumentMarshaler 파생클래스를 만들어 코드를 분리

### 더미 변수
<img width="1011" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/128bee6b-1b3c-45de-a092-c880216822fa">

- 추상 set 함수는 String 인수를 받아들이나 BooleanArgumentMarshaler는 인수를 사용하지 않는다. 추상 set 함수에 인수를 정의한 이유는 String Argumen뼈arshaler와 IntegerArgumentMarshaler에서 필요하기 때문이다.
  - 오버로딩으로 여러함수 구현해서 복잡하게 만드느니 더미변수 사용하겠다~
- 예외 처리 코드를 넣은지 얼마나 되었다고 바로 빼버리다니! 리팩터링을 하다보면 코드를 넣었다 뺐다 하는 사례가 아주 흔하다. 리팩터링은 루빅 큐브 맞추기와 비슷하다. 큰 목표 하나를 이루기 위해 자잘한 단계를 수없이 거친다. 각 단계를 거쳐야 다음 단계가 가능하다.

### 익셉션 클래스 선언
<img width="1080" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/d76834af-c590-434c-ad5f-9bd38beef02b">

- 왜 에러코드를 정의만 해놓고 안쓰는거지...에러코드 Args클래스 안에서만 쓰는건가?
- 에러코드로 사용하는 Enum을 클래스안에 정의해둔게 신박하다
<img width="659" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/8848124/70f643d0-e2cd-4eaf-9bd3-924458b98726">

- [익셉션을 기대하는 테스트] 익셉션이 안나면 테스트가 fail()한다.

### 기타
- 코드가 썩어가며 모듈은 서로서로 얽히고설켜 뒤엉키고 숨겨진 의존성이 수도 없이 생긴다.
- 오래된 의존성을 찾아내 깨려면 상당한 시간과 인내심이 필요하다. 반면 처음부터 코드를 깨끗하게 유지하기란 상대적으로 쉽다.
