# JavaScript Project Architecture

## Layer

세 개의 레이어로 나눈다.

* Domain Layer 
* Data Layer 
* Presentation Layer 

### Doamin Layer

Business Logic이 있는 곳이다.

*   Use Cases

    Use Case들은 애플리케이션의 비즈니스 로직을 포함하고 목적(intents)이다. 
*   Entities

    기본 유형의 속성이 있는 단순하지만 유효성 검사가 수행된다. 실제 예에서는 엔티티 및 값 개체를 클래스로 정의하고 유효성 검사를 수행한다. 
*   Boundaries

    Boundaries는 adapter의 추상화이다. 어댑터와 통신하는 방법을 나타낸다. 도메인의 Use Case 레이어에 정의된다. 

### Data Layer

데이터 계층은 어댑터가 있는 곳이다. 어댑터는 도메인과 외부 시스템 간의 정보 변환을 담당한다.

### Presentation Layer

Presentation Layer의 어댑터는 React UI 또는 Vue 레이어를 연결하는 곳이다. 상태 관리는 이 계층에서 수행되면 React 또는 Vue에 의존하지 않는다.

## 프로젝트 구조

```
📂project_root
  📂vue
     📂assets
       📂js
         📂biz 
            📂demo
                📂presentation
                📂domain
                  📂usecase
                    📄DemoMemberUsecase.ts
                  📂entity  
                    📄DemoMember.ts
                  📂boundary
                    📄DemoMemberRepository.ts
                📂data           
                  📄DemoMemberRepositoryImpl.ts
```
