
# 14장 - 점진적인 개선
프로그래밍은 과학보다 공예에 가깝고  
깨끗한 코드를 짜려면 1차 초안인 지저분한 코드를 짠 뒤에 초안을 고쳐나가면서  
최종안으로 정리해야 한다.

<br>

## 예제
- 유틸리티 Args  
Args 생성자에 (입력으로 들어온) 인수 문자열과 형식 문자열을 넘겨서  
Args 인스턴스를 생성하고 Args 인스턴스에다가 인수 값을 질의하는 클래스

- 사용법  
매개변수 두개로 Args 클래스의 인스턴스를 만든다.  
`Args arg = new Args("l,p#,d*", args);`  
1 매개변수 - 형식/스키마를 지정하고 명령행 인수를 정의함  
2 매개변수 - main으로 넘어온 명령행 인수 배열 자체

<br>

### Args의 초안
- 잘 돌아가지만 1차원적으로 단순하게 있는대로 선언/정의 하고 구현한 방식
- 많은 인스턴스 변수
- 특이한 상수 문자열
- 여러 자료구조(HasdhSEts, TreeSets)
- try-catch-catch 블록 등
- 기능에 따라 의존적인 코드들(ex- String, Integer 자료형이 추가되면 코드가 길어짐)  
타입유형 추가할 때마다 그 기능 수행하는 함수가 늘어남. 인터페이스식이 아니라서

<br>

### 리팩토링
- 인수 유형은 다양하지만 모두가 유사한 메서드를 제공하므로  
클래스 하나가 적합할 수 있다. => `ArgumentMarshaler` 클래스

- 테스트주도개발(TDD. Test-Driven Development)이 수반되면  
시스템에 변경을 가한 후에도 시스템이 변경 전과 동일하게 돌아간다.
즉, 시스템이 언제든 동일하게 돌아간다는 사실을 확인하려면 언제든 실행이 가능하고  
자동화된 테스트 슈트가 필요하다.

- 특정 자료형을 담는 xxxArgs의 Map의 값 타입을 ArgumentMarshaler 클래스로 지정해서 타입 의존성을 낮추고 값의 검증도 해당 클래스에서 진행할 수 있도록 수정

- ArgumentMarshaler 클래스에 논리를 다 구현하고 각각의 자료형에 해당되는 파생 클래스를 만들고 적용.

- 추상 set,get 함수를 추가하고 각 파생 클래스에다가도 추가해줌

- 특정 타입의 Map을 ArgumentMarshaler Map으로 바꾸고 관련 메서드를 변경한다.

- isXXX 메서드였던 것을 xxxxxArgumentMarshaler 타입인지 확인하는 인라인 코드로 변경

- setArgument에서 유형을 일일이 확인하는 코드를 args 배열을 list로 변환해서 Iterator를 set 함수로 전달하도록 변경.  
`List<String> argList;`  
`argsList = Arrays.asList<args);`  
`argsList.size()==0`  
`for( currentArgument = argsList.iterator(); currentArgument.hasNext(); )`  
`String arg = curretnArgument.next();`  
`currentArgument.next();`  

- 예외코드는 흉하고 사실상 ARgs 클래스에 속하지도 않으므로 모든 예외를 하나로 모아 ARgsException 클래스를 만든 후 독자 모듈로 옮긴다.

<br>

### 결론
- 소프트웨어 설계는 분할만 잘해도 품질이 크게 높아진다.
- 적절한 장소를 만들어 관심사 코드만 분리해도 설계가 좋아진다.  
=> 코드를 이해하고 보수하기 훨씬 쉬워진다.
- 너무 서두르다가 이후로 영원히 자신들의 운명을 지배할 악성 코드라는 굴레를 짊어진다.
- 코드가 썪어가며 모듈은 서로서로 얽히고 설켜 뒤엉키고 숨겨진 의존성이 수도 없이 생긴다.
- 오래된 의존성을 찾아내 깨려면 상당히 시간과 인내심이 필요하다.
