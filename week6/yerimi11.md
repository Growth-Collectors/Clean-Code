Clean-Code_week6_yerimi11 (~p.285)  
  

### 15. JUnit 들여다보기   

![image](https://github.com/Growth-Collectors/Clean-Code/assets/93559998/5b01fdf3-27d8-4598-bc28-a80af1fe966b)  
- 의도를 명확히 표현하려면 조건문을 캡슐화해야 한다. 즉, 조건문을 메서드로 뽑아내 적절한 이름을 붙인다.
  
![image](https://github.com/Growth-Collectors/Clean-Code/assets/93559998/85f4d523-31c2-4eae-80fa-2af2509cf473)  

- if문은 긍정으로 만들어 조건문을 반전한다.
- 불필요한 if문을 제거한다.
- 코드를 리팩터링 하다보면 원래 했던 변경을 되돌리는 경우가 흔하다. 리팩터링은 코드가 어느 수준에 이를 때까지 수많은 시행착오를 반복하는 작업이기 때문이다.

=> 리팩토링 시 위의 내용들을 기억하면 좋을 것 같다. 또한 현재 업무 중 내가 개발한 코드를 리팩토링하는 과정에 있는데, 이전으로 돌아가는 경우가 잘못된 과정이 아님을 알고 여러 시도를 해봐야 겠는 생각이 든다.  

---  

  
### 16. SerialDAte 리팩터링  

- 코드를 고칠 때마다 단위 테스트를 실행했다.
- 변수명은 늘 명확하게. getYYY -> getYear
- 테스트케이스 외에 호출되지 않는 메서드라면 해당 메서드와 관련 테스트 케이스는 전부 삭제하자.

=> 리팩토링하는 과정이군..!  

---  

  
### 17. 냄새와 휴리스틱 (~G23)  
  
**전부 지양해야 할 사항들**  
  
[주석]  
- C1: 부적절한 정보
- C2: 쓸모 없는 주석
- C3: 중복된 주석
  - 코드만으로 충분한데 구구절절 설명하는 중복이 중복된 주석이다.
  - 함수 서명만 달랑 기술하는 Javadoc의 케이스도 중복된 주석이다.  
- C4: 성의없는 주석
- C5: 주석 처리된 코드
  - github을 믿고 즉각 지워라.

[환경]  
- E1: 여러 단계로 빌드
- E2: 여러 단계로 테스트

[함수]  
- F1: 너무 많은 인수
  - 함수에서 인수 개수는 작을수록 좋다. 넷 이상은 최대한 피한다.
- F2: 출력 인수
- F3: 플래그 인수
  - boolean 인수는 함수가 여러 기능을 수행한다는 먕백한 증거다. 플래그 인수는 흔란을 초래하므로 피해야 마땅하다.
- F4: 죽은 함수
  - 아무도 호출하지 않는 함수는 삭제한다.

[일반]  
- G1: 한 소스 파일에 여러 언어를 사용한다
- G2: 당연한 동작을 구현하지 않는다
  - 함수나 클래스는 읽었을 때 당연하게 여길만한 동작과 기능을 제공해야 한다.
- G3: 경계를 올바로 처리하지 않는다
  - 흔히 개발자들은 머릿속에서 코드를 돌려보고 끝낸다.  
  - 부지런함을 대신할 지름길은 없다.
  - 스스로의 직관에 의존하지 마라. 모든 경계 조건을 찾아내고, 모든 경계 조건을 테스트 하는 테스트 케이스를 작성하라.
- G4: 안전 절차 무시
- G5: 중복
  - 중복된 코드를 하위 루틴이나 다른 클래스로 분리하라.
  - 여러 모듈에서 일련의 switch/case나 if/else 문으로 똑같은 조건을 거듭 확인하는 중복 -> 다형성(polymorphism)으로 대체해야한다.
  - 알고리즘이 유사하나 코드가 서로 다른 중복 -> TEMPLATE METHOD 패턴이나 STRATEGY 패턴으로 제거한다.
- G6: 추상화 수준이 올바르지 못하다
  - 세부 구현과 관련한 상수, 변수, 유틸리티 함수는 기초 클래스에 넣으면 안된다.
- G7: 기초 클래스가 파생 클래스에 의존한다  
- G8: 과도한 정보  
  - 클래스가 제공하는 메서드 수는 작을수록 좋다. 함수가 아는 변수 수도 작을수록 좋다. 클래스에 들어있는 인스턴스 변수 수도 작을수록 좋다.
  - 자료를 숨겨라. 유틸리티 함수를 숨겨라. 상수와 임시 변수를 숨겨라 메서드나 인스턴스 변수가 넘쳐나는 클래스는 피하라.
  - 하위 클래스에서 필요하다는 이유로 protected 변수나 함수를 마구 생성하지 마라. 인터페이스를 매우 작게 그리고 매우 깐깐하게 만들어라. 정보를 제한해 결합도를 낮춰라.
- G9: 죽은 코드
  - 죽은 코드란 실행 되지 않는 코드
  - 불가능한 조건을 확인하는 if 문과 throw 문이 없는 try 문에서의 catch 블록
  - 아무도 호출하지 않는 유틸리티 함수와 switch/case문에서 불가능한 case 조건
- G10: 수직 분리
  - 지역변수는 처음으로 사용하기 직전에 선언하며 수직으로 가까운 곳에 위치해야 한다
  - 비공개 함수는 처음으로 호출한 직후에 정의
  - 정의하는 위치와 호출하는 위치를 가깝게 유지
- G11: 일관성 부족
  - 다른 함수에서도 일관성 있게 동일한 변수 이름을 사용한다.
- G13: 인위적 결합
  - 서로 무관한 개념을 인위적으로 결합하지 않는다.
- G18: 부적절한 static 함수
  - 일반적으로 static 함수보다 인스턴스 함수가 더 좋다. 조금이라도 의심스럽다면 인스턴스 함수로 정의한다.  
- **G21: *알고리즘을 이해하라***
  - 잠시 멈추고 실제 알고리즘을 고민해라
  - 알고리즘을 안다고 생각하지만 실제는 코드가 ‘돌아갈’ 때까지 이리저리 찔러보고 굴려본다. ‘돌아간다’는 사실은 어떻게 아느냐고? 생각할 수 있는 테스트 케이스를 모두 통과하니까.
  - 구현이 끝났다고 선언하기 전에 함수가 돌아가는 방식을 확실히 이해히는지 확인하라. 테스트 케이스를 모두 통과한다는 사실만으로 부족하다. 작성자가 알고리즘이 올바르다는 사실을 알아야 한다.
  - 코드가 돌아간다는 사실을 아는 것과 돌아가기 위한 알고리즘이 올바르다는 사실을 아는 것은 다르다. 흔히 개발 자들은 알고리즘이 올바르다고 확산하지 못한다. 게으름의 소치라 하겠다.
- G22: 논리적 의존성은 물리적으로 드러내라
  - 의존하는 모든 정보를 명시적으로 요청하는 편이 좋다.
  ![image](https://github.com/Growth-Collectors/Clean-Code/assets/93559998/977badbe-2975-413c-b3d3-1d680dcc3bc8)
  - PAGE_SIZE를 HourlyReporter 클래스에 선언한 실수는 잘못 지운 책임(G17)에 해당한다.   
    HourlyRepoter 클래스는 HourlyReportFormatter가 페이지 크기를 알거라고 가정한다. 바로 이 가정이 논리적 의존성이다.   
    HourlyRepoter 클래스는 HourlyReportFormatter 클래스가 페이지 크기 55를 처리할 줄 안다는 사실에 의존한다.   
    만약 HourlyReportFormatter 구현 중 하나가 페이지 크기 55를 제대로 처리하지 못한다면 오류가 생긴다.  
    HourlyReportFormatter에 getMaxPageSize()라는 메서드를 추가하면 논리적인 의존성이 물리적인 의존성으로 변한다.   
    HourlyRepoter 클래스는 PAGE_ SIZE 상수를 사용하는 대신 getMaxPageSize() 함수를 호출하면 된다.    
- G23: If/Else 혹은 Switch/Case 문보다 다형성을 사용하라  
  -  ‘switch 문 하나’ 규칙을 따른다. 즉， 선택 유형 하나에는 switch 문을 한 번만 사용한다.  


  
