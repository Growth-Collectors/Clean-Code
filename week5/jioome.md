###  유틸리티 Args

프로그램을 짜다 보면 종종 명령행 인수의 구문을 분석할 필요가 생긴다. 

편리한 유틸리티가 없으면 main 함수로 넘어오는 문자열 배열을 직접 분석하게 된다. 새로 짤 유틸리티를 Args라고 부른다. 

###  Args 사용법

```java
public static void main(String[] args) {
  try {
    Args arg = new Args("l,p#,d*", args);
    boolean logging = arg.getBoolean('l');
    int port = arg.getInt('p');
    String directory = arg.getString('d');
    executeApplication(logging, port, directory);
  } catch (ArgsException e) {
    System.out.print("Argument error: %s\n", e.errorMessage());
  }
}
```

확장성이 부족했던 모듈을 소개하고, 모듈을 개선하고 정리하는 단계를 살펴볼 예정

Args는 사용법이 간단하다. 매개변수 두개로 Args 클래스 사용방법이 들어간다. 

구체적인 오류를 알아내려면 예외가 제공하는 errorMessage 메소드를 사용한다. 


###  Args 구현

깨끗한 코드를 짜려면 지저분한 코드를 짠 후에 정리해야 한다. 

**소프트웨어 설계는 분할만 잘해도 품질이 크게 높아진다. 적절한 장소를 만들어 코드만 분리해도 설계가 좋아진다. 관심사를 분리하면 코드를 이해하고 보수하기 훨씬 더 쉬워진다.**

### 정리

- 돌아가는 코드만으로는 부족하다. 돌아가는 코드가 심하게 망가지는 사례는 흔하다.
- 나쁜 코드보다 더 오랫동안 심각하게 개발 프로젝트에 악영향을 미치는 요인도 없다.
- 나쁜 코드도 깨끗한 코드로 개선할 수 있다. 하지만 비용이 엄청나게 많이 든다.
- 반면 처음부터 코드를 깨끗하게 유지하기란 상대적으로 쉽다.
- 코드는 언제나 최대한 깔끔하고 단순하게 정리하자.
