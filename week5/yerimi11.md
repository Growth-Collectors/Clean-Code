Clean-Code_week5_yerimi11  
  
### 점진적인 개선  
자바는 정적타입 언어라서 타입 시스템을 만족하려면 많은 단어가 필요하다.  
-> (14-7 에러코드) 정말 귀찮고 복잡해보이는데 실제로 정말 이렇게 줄줄 쓰는지  

대다수 신참 프로그래머는 이 충고를 충실히 따 르지 않는다. 그들은 무조건 돌아가는 프로그램을 목표로 잡는다. 일단 프로그램이 ‘돌아가면’ 다음 업무로 넘어간다. ‘돌아가는’ 프로그램은 그 상태가 어떻든 그대로 버려둔다. 경험이 풍부한 전문 프로그래머라면 이런 행동이 전문가로서 자살행위라는 사실을 잘 안다.  
-> 반성. 실제로 시간분배를 어떻게 해야할지.. 어떻게들 하고 계신지  
-> 단순히 돌아가는 코드에 만족하는 프로그래머는 전문가 정신이 부족하다. 설계와 구조를 개선할 시간이 없다고 변명할지 모르지만 나로서는 동의하기 어렵다. 나쁜 코드보다 더 오랫동안 더 심각하게 개발 프로젝트에 악영향을 미치는 요인도 없다. 나쁜 일정은 다시 짜면 된다. 나쁜 요구사항은 다시 정의하면 된다. 나쁜 팀 역학은 복구하면 된다. 하지만 나쁜 코드는 썩어 문드러진다.  
  
[점진적으로 개선하다]  
프로그램을 망치는 가장 좋은 방법 중 하나는 개선이라는 이름 아래 구조를 크게 뒤집는 행위다.    
어떤 프로그램은 그저 그런 ‘개선’에서 결코 회복하지 못한다. 개선 전과 똑같이 프로그램을 돌리기가 아주 어렵기 때문이다.  
그래서 아래 코드(14-7)까지 개선하는 과정에서 테스트 주도 개발(TDD) 기법을 사용했다. TDD는 언제 어느 때라도 시스템이 돌아가야 한다는 원칙을 따른다.  

리팩터링을 하다보면 코드를 넣었다 뺏다 하는 사례가 아주 흔하다.  

---  

14-7 ArgsException.java  

```java
import static com.objectmentor.utilities.args.ArgsException.ErrorCode.*;

public class ArgsException extends Exception { 
  private char errorArgumentId = '\0'; 
  private String errorParameter = null; 
  private ErrorCode errorCode = OK;
  
  public ArgsException() {}
  
  public ArgsException(String message) {super(message);}
  
  public ArgsException(ErrorCode errorCode) { 
    this.errorCode = errorCode;
  }
  
  public ArgsException(ErrorCode errorCode, String errorParameter) { 
    this.errorCode = errorCode;
    this.errorParameter = errorParameter;
  }
  
  public ArgsException(ErrorCode errorCode, char errorArgumentId, String errorParameter) {
    this.errorCode = errorCode; 
    this.errorParameter = errorParameter; 
    this.errorArgumentId = errorArgumentId;
  }
  
  public char getErrorArgumentId() { 
    return errorArgumentId;
  }
  
  public void setErrorArgumentId(char errorArgumentId) { 
    this.errorArgumentId = errorArgumentId;
  }
  
  public String getErrorParameter() { 
    return errorParameter;
  }
  
  public void setErrorParameter(String errorParameter) { 
    this.errorParameter = errorParameter;
  }
  
  public ErrorCode getErrorCode() { 
    return errorCode;
  }
  
  public void setErrorCode(ErrorCode errorCode) { 
    this.errorCode = errorCode;
  }
  
  public String errorMessage() { 
    switch (errorCode) {
      case OK:
        return "TILT: Should not get here.";
      case UNEXPECTED_ARGUMENT:
        return String.format("Argument -%c unexpected.", errorArgumentId);
      case MISSING_STRING:
        return String.format("Could not find string parameter for -%c.", errorArgumentId);
      case INVALID_INTEGER:
        return String.format("Argument -%c expects an integer but was '%s'.", errorArgumentId, errorParameter);
      case MISSING_INTEGER:
        return String.format("Could not find integer parameter for -%c.", errorArgumentId);
      case INVALID_DOUBLE:
        return String.format("Argument -%c expects a double but was '%s'.", errorArgumentId, errorParameter);
      case MISSING_DOUBLE:
        return String.format("Could not find double parameter for -%c.", errorArgumentId); 
      case INVALID_ARGUMENT_NAME:
        return String.format("'%c' is not a valid argument name.", errorArgumentId);
      case INVALID_ARGUMENT_FORMAT:
        return String.format("'%s' is not a valid argument format.", errorParameter);
    }
    return ""; 
  }
  
  public enum ErrorCode {
    OK, INVALID_ARGUMENT_FORMAT, UNEXPECTED_ARGUMENT, INVALID_ARGUMENT_NAME, 
    MISSING_STRING, MISSING_INTEGER, INVALID_INTEGER, MISSING_DOUBLE, INVALID_DOUBLE
  }
}
```
