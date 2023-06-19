Clean-Code_week4_yerimi11
(수정 중)

관심사 분리를 하지 않고 런타임 로직과 객체 생성 로직이 섞이는 경우, 단일 책임 원칙(Single Responsibility Principle)이 깨질 수 있다.  
<img width="309" alt="image" src="https://github.com/Growth-Collectors/Clean-Code/assets/93559998/2ce1cf3f-599f-47e8-9081-435f7903a36b">

좋은 설계를 위해서는 객체 생성과 관련된 로직은 별도의 팩토리나 생성자 등의 메서드로 분리하여 단일 책임을 갖는 별도의 클래스로 위임하는 것이 좋다.  
이를 통해 코드의 응집도를 높이고 유지보수성을 향상시킬 수 있다.  

