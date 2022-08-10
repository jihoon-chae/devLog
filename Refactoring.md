# 챕터 2

## 리팩토링이란

리팩토링 → 결과/행동 변경없이 코드 구조를 재조정

→ 소프트웨어 기능을 보존하면서 설계, 구조 및 구현을 개선

→ 복잡성감소, 가독성 향상, 유지보수성을 개선, 확장성을 높임

→ 단순 깔끔 표현력이 뛰어난 코드, 내부 아키택처

금지 → 기능 변경/추가, 버그수정(버그 발견해도 그대로 둬야함), 성능개선, 버전 업데이트

## 왜 리팩토링 할까 ?

 개발 초기 완벽한 코드, 시스템 설계는 어려움

프로그램의 요구사항은 꾸준히 변경됨

더럽고 복잡한 코드는 이해하기 어려움

예상치 못한 에러가 발생하기 쉬움

복잡한 코드 유지보스는 어려움

→ 소프트웨어 설계가 좋아짐

→ 소프트웨어 이해하기 쉬워짐

## 어떻게 리팩토링 할까

기존 프로그램 기능과 동작을 유지할 수 있도록 테스트 코드가 필요함!

→ 함수, 특정기능, UI, 성능, API 스펙 등을 고려해서 검증할 수 있는지 확인할 수 있는 테스트 코드를 미리 만들기

→ 코드의 나쁜 냄새에 따라 여러 리팩토링 기법을 점진적으로 적용하기 

## 언제 리팩토링 할까

→ 수시로 해야한다

**프로젝트 시작단계** 

 기능구현을 위한 코드 작성 → 첨부터 깔끔한 코드를 작성하는게 좋음 → 기능 구현을 위한 코드를 작성하고 테스트 코드를 작성(기능구현코드와 테스트코드 작성을 함께) 3의법칙 → 비슷한일을 3번이상하게되면 리팩토링한다. 

코드리뷰 → 받게 되는데 코드를 이해하기 쉽게 만들기 (좋은 문서화 ), 

기능추가 → 기능 추가할때 기능 쉽게 추가하게 만들기( 반복되는 코드 재사용성, 모듈성)

**프로젝트 유지보수 단계**

버그수정 → 버그 검증할 수 있는 테스트 코드 → 이럴때 버그생기는 구나 → 코드를 이해하기 쉽게 변경하기 쉽게 변경 

기능 추가 → 기존 기능들에 대한 테스트 확인 → 코드를 이해하기 쉽게 변경

**오래된 프로젝트**

레거시 코드 

버그수정 및 기능추가시에만 → 수정이 필요한 모듈/코드를 한정적으로 테스트추가 

리팩토링 → 코드수정 또는 기능 추가

정말 중요한 기능이냐, 수정이 급하냐 등을 따져서 리팩토링, 때론 새로운 코드를 작성하는 것이 깔끔 

## 리팩토링의 중요 포인트

기능보존 확신을 위해서 테스트 코드작성!

완벽한 클린코드 완벽한 설계는 존재하지 않는점을 인정할것

우선 코드 작성 → 테스트 코드 작성 → 기능 구현을 위한 코드 작성

필요 없는 기능에 집착해서 너무 미래지향적으로 설계하지 않도록! 지금 상황에 맞게 코드 작성하기

# 챕터 3 코드에서 나는 악취

## 나쁜 냄새(기본적인 악취)

`기이한 이름` → 코드이해력, 가독성 X (가장 나쁜 악취)

`중복 코드` → 비슷한 일을 하는 코드가 반복 → 실수와 에러 발생할 확률 올라감

`긴 함수` → 이해하기 어려움, 재사용성 ↓

`긴 매개변수 목록` → 사용하기 어려움, 잦은 실수 

`전역 데이터` → 정말 나쁜 악취 → 최악, 유령같은 버그 출몰

`가변데이터` → 변경이 가능한 데이터 → 예상치 못한 곳에서 데이터를 변경 → 예상치 못한 에러 출력

## 나쁜냄새2(고급레벨) - 모듈성에 관련된 악취

뒤엉킨 변경 → 함수 또는 클래스 모듈안에서 여러가지 일을 하게되면 → 다양한 이유로 수정해야함 → 한 곳에서 지나치게 많은 일을 하지 않도록 하는 것이 중요하다! 

산탄총 수술 → 한 모듈을 수정하면 이 모듈이 스파게티처럼 다른 모듈과 뒤엉킴.. 다른 곳과 연관되어서 여러 곳에서 수정을 해야함 

기능편애 → 내부적으로 끈끈하게 상호작용이 일어나지 않고 다른 모듈과 더 밀접하게 상호작용 → 기능편애 → 산탄총 수술이 일어 남

데이터 뭉치 → 여러곳에서 항상 함께 쓰임

기본형 집착 → 기본형에 집착하지 말고 관련된 데이터가 있다면 묶어 주는게 좋음 → 기본형 집착하면 관련된 코드가 여기저기 ..

반복되는 switch문 → 새로운 타입이 추가되면 여기저기 업데이트

## 나쁜냄새3(기타 냄새들)

반복문 → 절차형코드 → 부작용 발생할 수 있다. → 함수형 프로그래밍식의 반복 파이프라인을 사용

성의없는 요소 → 불필요한 함수, 클래스, 인터페이스

추측성 일반화 → 혹시 모르니, 미래를 위해서

임시필드 → 특정 상황에서만 사용됨, 이해도↓

메시지 체인 → 이거다음 이거하고 .. 내부로직이 노출됨 ..사용하는 곳마다 순차적으로 사용해야 함

중개자 → 함수를 호출만 하는 중개자 역할만 하는 코드가 있다면 필요한지 불필요한지 따져봐야함

내부자 거래 → 내 모듈내부 특정한 함수가 너무 외부 모듈을 참조, 호출하거나 너무 의존하면 모듈간 결합도가 높아져서 악취

거대한 클래스 → 중복코드↑, 뒤엉킨 변경↑ 

서로다른 인터페이스의 대안 클래스들 → 다른데 비슷한기능을 함 → 서로 대체성↓ 재사용성 ↓ → 공통된 인터페이스, 공통된 규격을 따를것

데이터 클래스 → 필요한 로직이 여기저기 .. 

상속포기 → 상속의 오용, 남용은 위험..

주석 → 필요없는 주석은 악 → 나쁜 코드를 덮기 위한 주석은 악취

# 챕터 4 테스트 구축하기

코드 수정, 변경할때 테스트 코드의 힘이 발휘됨

요구사항(함수, 특정기능, UI, 성능, API 스펙)을 만족하는지 확인하면서 개발하면서 기존의 기능에 문제가 없는것을 검증해줌

작성된 테스트를 주기적을 잘 작동하는지 확인하고 테스트를 자동화 해서 한번 동작하면 성공했는지 실패했는지 실패하면 어디서 실패했는지를 잘 나타낼 수 있어야한다. → 요즘은 자가 테스트가 다 들어있다. (좋은 테스트 툴이 있다) → 함수를 테스트하고 싶은지, 성능을 테스트하고 싶은지 …

테스트를 구축하는 것은 

## 챕터 6 기본적인 리팩토링

## 6.2 함수 포인트 정리

함수 → 특정한 일을 수행하는 코드의 집합 → 프로그램을 이루는 가장 기본적인 단위

1. 코드가 어떤일을 하는지 파악
2. 독립적인 함수로 추출하기
3. 목적에 맞는 이름 짓기

함수를 이용하는 것의 장점 → 재사용이 가능, 유지보수성 증가, 높은 가독성

## 6.8 이름짓기 포인트 정리

변수는 저장된 값을 잘 나타낼 수 있는 의미있는 이름 (구체적일수록 좋다)

변수는 무엇을 담고있는지 잘 나타낼 수 있어야함

함수는 동사로 많이 쓴다.

ex) `calculate`, `displayBanner`, `getTotalPrice` …

## 함수의 매개변수 포인트 정리

매개변수의 개수는 최대 3개를 넘지 않는것이 좋다.

→ 연관있는 데이터 구조 하나로 묶어주는게 좋다 ex) 자료구조, 클래스 …

## 6.12 매개변수 객체 만들기

## 6.13 캡슐화

내부 구현사항을 숨기고 외부에서 필요한 사항들만 공개

```jsx
let owner = {

name: '지훈';

};
```

→ 누구든 접근하여 name을 변경할 수 있다

→ 객체보다는 모듈, 클래스와 같은 형태로 캡슐화 해두자!

→ getName함수를 외부에 공개 해두고 다시 수정할 수 없도록 막아두자

→ 데이터를 변경하고, 사용하는 코드를 감시할 수 있음!