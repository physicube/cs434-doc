# Out of the Tar Pit Summary



## 1. Introduction

OOP, FP는 모두 장단점이 있어서 큰 시스템에 적용하기 어려웠는데, 이 둘과 관계형 database의 idea를 합치면,  큰 시스템을 간단하게 만들 수 있는 잠재력을 지니고 있다.

## 2. Complexity

Complexity는 현대 software에 있어서 많은 문제를 가지고 온다. Complexity는 large system을 이해하기 어렵게 만들기 때문에, 많은 자원을 유지보수에 사용하게 만든다. 

그리고 이 논문에서는 Complexity는 system의 복잡성을 나타내는 용어로 쓰일 것이다.

## 3. Approaches to Understanding

Complexity는 우리가 system을 이해하려고 시도하는데서 문제를 발생시킨다.

우리가 system을 이해하는 방법은 크게 testing, informal Reasoning 2가지가 있는데, 전자는 code를 black-box로 테스트해보는 것이고, 후자는 코드를 읽으면서 이해하려는 것을 말한다.

그 중에서 testing의 경우 bug의 존재를 알려줄 수 있지만, bug가 없는 것을 보장하지 않는다.

Testing과 informal reasoning 모두 필요없는 것은 아니지만, 이런 방식으로 system을 이해하려는 것에는 한계가 있다. 이는 system을 단순하게 설계하는 것이 더욱 중요하다는 것을 의미한다.

## 4. Causes of Complexity

### Complexity caused by State

Complexity의 원인 중 하나는 state인데, 이는 많은 프로그램들이 state를 다루면서 에러를 발생시키기 때문이다.

State는 다른 state가 어떻게 동작하는지 알려주지 않고, 특정 input에 대한 test는 다른 input들에 대한 test에 대해서 아무것도 말해주지 않는데, 이 두 문제가 결합되면 system은 매우 복잡해진다.

Informal reasoning을 할 때도, state가 많으면 복잡도가 exponential하게 증가하고, stateless한 모듈에서도 state가 있는 다른 모듈을 사용하면 똑같은 문제가 발생한다.

### Complexity caused by Control

Control은 일이 일어나는 순서를 의미하는데, 이는 Concurrent programming이 등장하면서 문제가 심각해졌다. Concurrency가 있으면 같은 state, 같은 input으로 test를 수행하더라도 그 결과가 다음 수행에서 나오는 결과에 대해 아무것도 보장하지 않게되고, 이는 Complexity를 더욱 증가시킨다.

### Complexity caused by Code Volume

마찬가지로 Code의 크기가 exponential하게 커지는 것도 문제가 되고 있다.

이 밖에도 여러 원인이 있는데, 이는 3가지 원인에 의한 것으로 간추릴 수 있다.

1. Complexity는 Complexity를 야기한다.
2. 간단하게 Code를 짜는 것이 힘들다.
3. 언어가 powerful하기 때문에 system을 이해하는 것이 힘들어 질 수 있다.

## Classical approaches to managing complexity

### 1. OOP

OOP는 여러 객체의 state를 만들고, 이 state간의 상호작용을 만드는 방식으로 프로그래밍 하는 패러다임을 말한다. 

OOP는 객체의 캡슐화를 이용해서 state의 변화 방식을 method로 제한시킬 수 있게 만드는 장점이 있다. 하지만 여러 객체간의 constraint는 표현하기 힘든 점 등이 단점이다.

Object는 attribute가 같아도 구분되는 특성이 있고, immutable한 object를 만들때도 이런 object들이 서로 구분되기 때문에, 이를 위해서 추가로 method를 정의해줘야하는 문제점도 있다. 이러한 문제점들은 OOP style system을 복잡하게 만드는 원인이 된다.

OOP는 State외에도  imperative programming과 마찬가지로 shared-state concurrency를 사용하기 때문에, 마찬가지로 complexity가 커지게 된다.

### 2. FP

FP는 untyped lambda calculus에서 기반한 프로그래밍 패러다임으로, state가 존재하지 않기 때문에 함수의 parameter가 같으면 항상 같은 결과를 기대할 수 있다. 이는 testing과 informal reasoning에 있어서 상당한 이점을 가지고 온다.

그리고 concurrency에 있어서도 loop보다 map과 같은 abstract한 방식을 사용하고, 함수들은 병렬로 계산되어도 안전하기 때문에 상당한 이점이 있다.

물론 state와 비슷하게 counter를 function으로 구현하는 "kind of state"와 같은 경우도 있지만, 이것 보다도 state가 없음에서 얻는 이점이 훨씬 많다.

그럼에도 불구하고 FP는 모듈화가 힘들다는 단점이 있기 때문에, FP로 개발을 하는데는 trade-off가 있다고 볼 수 있다.

### 3. LP

Logic programming은 Prolog와 같이 Axiom을 기반으로 결론을 도출하는 형태의 프로그래밍 패러다임을 말한다. 이도 pure한 경우 stateless이기 때문에 FP와 마찬가지의 장점을 가진다. Control 측면에 있어서도 암시적인 ordering대로 goal을 처리하기 때문에 장점을 가진다.

## 6. Accidents and Essence

Essential complexity는 system이 해결하려는 문제 그 자체이고, accidental complexity는 개발을 하면서 나오는 부차적인 complexity를 말한다. 이 논문에서는 accidental complexity를 다룰것이다.



## 7. Recommend General Approach

Ideal한 경우 state나 control에 의한 complexity를 최대한 피할 수 있지만, 현실 세계는 그렇지 않다.

따라서 complexity를 avoid, separate 하는 2가지 방식을 통해서 최소화 할 수 있다.

가능하면 accidental complexity를 피하도록 설계하도록 하고, 실용적인 목적 등으로 인해 피할 수 없는 경우는, 프로그램의 logic상 해당 essential한 파트와 accidental한 파트를 분리해서 설계를 하는 것이 좋다.