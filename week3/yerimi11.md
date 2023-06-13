Clean-Code_week3_yerimi11
(추가 중)

### 오류 처리  
[Try-Catch-Finally 문부터 작성하라]  
try-catch 구조로 범위를 정의한 후 TDD를 사용해 필요한 나머지 논리를 추가한다.
  
[미확인(unchecked) 예외를 사용하라]  
지금은 안정적인 소프트웨어를 제작하는 요소로 확인된(checked) 예외가 반드시 필요하지는 않다는 사실이 분명해졌다.  
C#와 C++, 파이썬, 루비는 확인된 예외를 지원하지 않는다. 그럼에도 불구하고 해당 언어들은 안정적인 소프트웨어를 구현하기에 무리가 없다.  
그러므로 확인된 오류가 치르는 비용에 상응하는 이익을 제공하는지 따져봐야 한다.  
  
- 확인된 예외는 OCP(Open Closed Principle)를 위반한다.  
  메서드에서 확인된 예외를 던졌는데 catch 블록이 세 단계 위에 있다면 그사이 메서드 모두가 선언부에 해당 예외를 정의해야 한다.  
  즉， 하위 단계에서 코드를 변경하면 상위 단계 메서드 선언부를 전부 고쳐야 한다.  
  모듈과 관련된 코드가 전혀 바뀌지 않았더라도 (선언부가 바뀌었으므로) 모률을 다시 빌드 한 다음 배포해야 한다.  
  
- 확인된 오류를 던진다면 함수는 선언부에 throws 절을 추가해야 한다.  
  그러면 변경한 함수를 호출하는 함수 모두가 1) catch 블록에서 새로운 예외를 처리하거나 2) 선언부에 throw 절을 추가해야 한다.  
  결과적으로 최하위 단계에서 최상위 단계까지 연쇄적인 수정이 일어난다.  
  throws 경로에 위치하는 모든 함수가 최하위 함수에서 던지는 예외를 알아야 하므로 캡슐화가 깨진다.  
  
- 때로는 확인된 예외도 유용하다. 아주 중요한 라이브러리를 작성한다면 모든 예외를 잡아야 한다. 
  하지만 일반적인 애플리케이션은 의존성이라는 비용이 이익보다 크다.  
  
[예외에 의미를 제공하라]  
예외를 던질 때는 전후 상황을 충분히 덧붙인다.  
오류 메시지에 정보를 담아 예외와 함께 던진다. 실패한 연산 이름과 실패 유형도 언급한다.  
애플리케이션이 로깅 기능을 시용한다면 catch 블록에서 오류를 기록하도록 충분한 정보를 넘겨준다.  
  
[호출자를 고려해 예외 클래스를 정의하라]  
- 오류를 형편없이 분류한 사례
```
ACME Port port =ne써 ACMEPort(12);
try { 
  port.open() ;
} catch (DeviceResponseException e) { 
  reportPortError(e);
  logger.log("Device response exception", e);
} catch (ATM1212UnlockedException e) { 
  reportPortError(e); 
    logger.log("Unlock exception", e);
} catch (GMXError e) {
  reportPortError(e);
  logger.log("Device response exception"); 
  } finally {
  ...
}
```
대다수 상황에서 우리가 오류를 처리하는 방식은 (오류를 일으킨 원인과 무관하게) 비교적 일정하다.  
1) 오류를 기록한다. 2) 프로그램을 계속 수행해도 좋은지 확인한다.  
위 코드는 중복이 심하지만 그리 놀랍지 않다. 예외에 대응하는 방식이 예외 유형과 무관하게 거의 동일하다. -> 호출하는 라이브러리 API를 감싸면서 예외 유형 하나를 반환하도록 고치면 된다.  
```
LocalPort port = new LocalPort(12); 
try {
  port.open();
} catch (PortDeviceFailure e) {
  reportError(e);
  logger.log(e.getMessage() , e); 
} finally {
  ...
}
```
여기서 LocalPort 클래스는 단순히 ACMEPort 클래스가 던지는 예외를 잡아 변환하는 감싸기 wrapper 클래스이다.  
```
public class LocalPort { 
  private ACMEPort innerPort;

  public LocalPort(int portNumber) { 
    innerPort ne씨 ACMEPort(portNumber);
  }

  public void open() { 
    try {
      innerPort.open();
    } catch (DeviceResponseException e) {
      throw new PortDeviceFailure(e);
    } catch (ATM1212UnlockedException e) {
      throw new PortDeviceFailure(e); 
    } catch (GMXError e) {
      throw new PortDeviceFailure(e);
    } 
  }
  ...
}
```
외부 API를 감싸면 외부 라이브러리와 프로그램 사이에서 의존성이 크게 줄어든다.  
나중에 다른 라이브러리로 갈아타도 비용이 적다.  
감싸기 클래스에서 외부 API를 호출하는 대신 테스트 코드를 넣어주는 방법으로 프로그램을 테스트하기도 쉬워진다.  
  
[정상 흐름을 정의하라]  
외부 API를 감싸 독자적인 예외를 던지고， 코드 위에 처리기를 정의해 중단된 계산을 처리한다. 대개는 멋진 처리 방식이지만， 때로는 중단이 적합하지 않은 때도 있다.  
```
MealExpenses expenses =expenseReportDAO.getMeals(employee.getID()); 
m_total += expenses.getTotal();
```
ExpenseReportDAO를 고쳐 언제나 MealExpense 객체를 반환한다. 청구한 식비가 없다면 일일 기본 식비를 반환하는 MealExpense 객체를 반환한다.  
```
public class PerDiemMealExpenses implements MealExpenses { 
  public int getTotal() {
  // 기본값으로 일일 기본 식비를 반환한다. 
  }
}
```
이를 **특수 사례 패턴 SPECIALCASEPATTERN**이라 부른다.  
클래스를 만들거나 객체를 조작해 특수 사례를 처리하는 방식이다. 그러면 클래스나 객체가 예외적인 상황을 캡슐화해서 처리하므로, 클라이언트 코드가 예외적인 상황을 처리할 필요가 없어진다.  
