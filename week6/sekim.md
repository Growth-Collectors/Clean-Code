## `**chapter**` **15장 JUnit 들여다보기**

---

- 디팩터링은 리팩터링의 반대 과정이다. 디팩터링 결과로 나온 코드는 구조적으로 어지럽고 취약하다.
- 의도를 명확히 하려면 조건문을 캡슐화해야 한다. 즉, 조거문을 메서드로, 뽑아내 적절한 이름을 붙인다.

변경 전

```java
public String compact(String message) {
    if (expected == null || actual == null || areStringsEqual())
    return Assert.format(message, expected, actual);

    findCommonPrefix();
    findCommonSuffix( ) ;

    String expected =compactString(this.expected); 
    String actual =compactString(this.actual);
    return Assert.format(message, expected, actual); 
}
```

변경 후

```java
public String compact(String message) { 
    if (shouldNotCompact())
        return Assert.format(message, expected, actual);
    findCommonPrefix();
    findCommonSuffix( );
    String expected =compactString(this.expected); 
    String actual =compactString(this.actual); return Assert.format(message, expected, actual);
}
private boolean shouldNotCompact() {   
    return expected == null || actual == null || areStringsEqual();
}
```

- 부정문은 긍정문보다 이해하기 약간 더 여럽다. 그러므로 첫 문장 If를 긍정으로 만들어 조건문을 반전한다.

```java
if (canBeCompacted()) {
	... 생략
}

private boolean canBeCompacted() {
	return expected != null && actual != null && !areStringsEqual();
}
```

- 코드를 리팩터링 하다 보면 원래 했던 변경을 되돌리는 경우가 흔하다. 리팩터링은 코드가 어느 수준에 이를때까지 수많은 시행착오를 반복하는 작업이기 때문이다.

## `**chapter**` **16장 SerialDate 리팩터링**

---

- MonthConstants 클래스는 달을 정의하는 static final 상수 모음에 불과하다. 상수 클래스를 상속하면 MonthConstants.Januray와 같은 표현을 사용할 필요가 없어진다. 옛날 자바 프로그래머들이 많이 쓰던 기교인데, 바람직하다고 보기는 어렵다. MonthConstants는 enum으로 정의해야 마땅하다.

변경 전

```java
public interface MonthConstants {
    /** 1월을 위한 상수 */
    public static final int JANURAY = 1;

    /** 2월을 위한 상수 */
    public static final int FEBRUARY = 2;

    /** 3월을 위한 상수 */
    public static final int MARCH = 3;
    
    ... 생략
 }
```

변경 후

```java
public abstract class DayDate implements Comparable, Serializable { 
    public static enum Month {
        JANUARY( 1), 
        FEBRUARY(2), 
        MARCH(3), 
        APRIL(4),
        MAY(5), 
        ... 생략
    Month(int index) { 
        this.index index;
    }
    public static Month make(int monthlndex) { 
        for (Month m Month.values()) {
            if (m.index == monthlndex) 
                return m;
        }
        throw new IllegalArgumentException("Invalid month index " + monthlndex); 
    }
    public final int index; 
    }
}
```

- 불필요한 주석은 거짓말과 잘못된 정보가 쌓이기 좋은 곳이다.
- 일반적으로 기반 클래스는 파생 클래스를 몰라야 바람직하다.
- 또한 인수와 변수 선언에서 final 키워드를 모두 없앴다. 실질적인 가치는 없으면서 코드만 복잡하게 만든다고 판단했기 때문이다. [G12]의 final을 제거하겠다는 결정은 일부 기존 관례에 어긋난다. 예를 들어, 로버트 시몬스는 “코드 전체에 fianl을 사용해라…”고 강력히 권장한다. 확실히 나와 다른 생각이다. 내가 보기에 final 키워드는 final 상수 등 몇 군데를 제하면 별다른 가치가 없으며 코드만 복잡하게 만든다. 어쩌면 내가 이렇게 느끼는 이유는 내가 짠 단위 테스트가 fianal 키워드로 잡아낼 오류를 모두 잡아내기 때문인지도 모르겠다.
- 다시 한 번 우리는 보이스카우트 규칙을 따랐다. 체크아웃한 코드보다 좀 더 깨끗한 코드를 체크인하게 되었다. 시간은 걸렸지만 가치 있는 작업이었다. 테스트 커버리지가 증가했으며, 버그 몇 개를 고쳤으며, 코드 크기가 줄었고, 코드가 명확해졌다. 다음은 우리보다 코드를 좀 더 쉽게 이해하리라. 그래서 우리보다 코드를 좀 더 쉽게 개선하리라

## `**chapter**` **17장 냄새와 휴리스틱**

---

- 프로그램을 수정할 때마다 나는 “왜?”라고 자문한 다음 그 답을 기록했다. 코드를 읽으면서 나쁜 냄새를 정리하다보니 목록이 상당히 길어졌다.

### 주석

- 주석은 코드와 설계에 기술적인 설명을 부여하는 수단이다.
- 오래된 주석, 엉뚱한 주석, 잘못된 주석은 더 이상 쓸모가 없다. 쓸모 없어질 주석은 아예 달지 않는 편이 가장 좋다. 코드와 무관하게 혼자서 따로 놀며 코드를 그릇된 방향으로 이끈다.
- 구구절절 설명하는 주석이 중복된 주석이다.
- 문법과 구두점을 올바로 사용한다. 주절대지 않는다. 당연한 소리를 반복하지 않는다. 간결하게 명료하게 작성한다.
- 주석으로 처리된 코드가 줄줄이 나오면 신경이 아주 거슬린다. 주석으로 처리된 코드를 발견하면 즉각 지워버려라! 소스코드 관리 시스템이 기억하니까. 누군가 정말로 필요하다면 이전 버전을 가져오면 되니까. 주석으로 처리된 코드를 내버려 두지 마라

### 환경

- 한 명령으로 전체를 체크아웃해서 한 명령으로 빌들할 수 있어야 한다
- 아무리 열악한 환경이라도 셸에서 명령 하나로 가능해야 한다. 모든 테스트를 한 번에 실행하는 능력은 아주 근본적이고 아주 중요하다. 따라서 그 방법이 빠르고, 쉽고, 명백해야 한다.

### 일반

- 소스 파일 하나에 언어 하나만 사용하는 방식이 가장 좋다.
- 최소 놀람의 원칙에 의거해 함수나 클래스는 다른 프로그래머가 당연하게 여길 만한 동작과 기능을 제공해야 한다.
- 부지런함을 대신할 지름길은 없다. 모든 경계 조건을 테스트하는 테스트 케이스를 작성하라
- 실패하는 테스트 케이스를 일단 제껴두고 나중으로 미루는 태도는 신용카드가 공짜 돈이라는 생각만큼 위험하다.
- 추상화는 소프트웨어 개발자에게 가장 어려운 작업 중 하나다. 잘못된 추상화를 임시변통으로 고치기는 불가능하다.
- 죽은 코드란 실행되지 않는 코드를 가리킨다. 불가능한 조건을 확인하는 if문과 throw 문이 없는 try문에서 catch블록이 좋은 예이다. 죽은 코드는 시간이 지나면 악취를 풍기기 시작한다. 죽은 지 오래될수록 악취는 강해진다. 죽은 코드는 설계가 변해도 제대로 수정되지 않기 때문이다. 컴파일은 되지만 새로운 규칙이나 표기법을 따르지 않는다. 죽은 코드를 발견하면 올바른 행동을 취하기 바란다. 적절한 장례식을 치뤄주라. 시스템에서 제거하라.

- 변수와 함수는 사용되는 위치에 가깝게 정의한다. 지역 변수는 처음으로 사용하기 직전에 선언하며 수직으로 가까운 곳에 위치해야 한다. 선언한 위치로부터 몇백 줄 아래에서 사용하면 안 된다.
- 클래스 메서드는 자기 클래스의 변수와 함수에 관심을 가져야지 다른 클래스의 변수와 함수에 관심을 가져셔는 안된다.