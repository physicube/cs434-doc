# Summary of Clean Code
> by physicube(POSTECH CSE 17)

## Chapter 2 : Meaningful names
- 의도가 드러나는 이름
- 이름이 중복되지 않도록 조심(ex. 이름에 `List`가 들어갔는데, `List` class 사용안하는 경우)
- 변수이름에 `var`, 테이블에 `table` 등을 넣는 것은 중복
- 이름은 발음/검색등이 쉽도록 작성한다(범위가 넓을수록 긴 것이 좋을 수 있다.)
- 변수이름에 type, 또는 멤버변수등의 정보를 넣을 필요가 없다
    - 차라리 멤버변수, type등을 highlight시켜주는 IDE를 쓰자.
- class/object 이름은 명사를 사용, method는 동사를 사용
    - class : `Customer`, `Account`등/ `Manager`, `Data`, `Info` 등은 피한다.
    - method : `postPayment`, `deletePage`등 / `get`, `set`, `is` 함수인지 볼것
- Constructor overload시에는 static factory method가 좋다.
    - `Complex.FromRealNumber(23.0)` 가 `new Complex(23.0)` 보다 낫다
- 개념 1개당 1개의 단어를 사용하자
    - 값을 가져옴 -> `get` / `controller`, `manager`등 -> `manager`와 같이 1개씩만 고르기
    - `add`를 +로 사용했으면 원소 추가는 `append` 등으로 
    - 특정 design pattern을 사용했으면 영역에 따라 그 패턴의 용어들을 가져다 쓰는 것도 좋다
- class 이름을 정할때 프로젝트이름 등을 붙이는 것은 좋지 않다.
    - `Address`, `PostalAddress`, `MAC` 등과 같이 명료하게 의도가 드러나게 적으면 된다.
    - 길이가 가능한 짧으면 좋고, 의도를 드러내기 위해서라면 길게 해도 괜찮다.
- 전반적으로 드는 느낌은, 의도를 알 수 있는 한도내에서 가장짧고 겹치지 않는 이름을 고르면 된다.

## Chapter 3 : Functions
- 함수를 작게 만드는 것이 좋다.
    - if/else/while 문에 들어가는 블록은 1줄 이내로 짜는 것이 좋다.
    - 함수는 1가지 일만 해야하고, 들여쓰기는 1,2단을 넘어서지 않아야한다.
    - 함수안에서 하는 일들을 meaningful한 name으로 추출이 가능하다면 2개 이상의 일을 하는 것.
    - 함수는 추상화 수준을 1개로 유지해야한다.
- [SRP(single responsibility principle)](https://en.wikipedia.org/wiki/Single-responsibility_principle) 원칙
    - class는 1개의 책임을 가져야한다.
    - 변경하려는데는 단 1개의 이유만을 가져야한다.
- [OCP(Open-Closed Principle)](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle) 원칙
    - 소프트웨어 개체(class, function 등)은 확장은 가능하도록, 이를 위해 수정은 안해도 되도록 만든다.
- 함수의 입력인수는 작을수록 좋다.
    - 인수가 1개인 경우는 인수를 변환하여 반환하거나 인수를 체크하는 형식이 좋다.
    - bool 인수는 피하자
    - 인수가 여러개면 인수로 class를 만드는 것을 고려할 필요도 있다
    - 인수로 출력(ex outputBuffer가 인수인 경우)은 피하자
- 오류 코드 대신 exception을 사용하라
    - try, catch는 별도 함수로 뽑는게 좋다.
- 함수를 짜고 test를 통과하는 범위 내에서 계속 다듬어야 한다.