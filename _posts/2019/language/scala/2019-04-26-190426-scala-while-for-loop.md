---
title: "스칼라 foreach, for문과 while문"
excerpt: "스칼라의 반복문 foreach, for문과 while문에 대해 살펴봅니다. 함수형 프로그래밍에서의 반복문 사용방법을 알 수 있습니다."
search: true
categories: 
  - Language
  - Scala
tags: 
  - Scala
  - 스칼라
last_modified_at: 2019-04-26T22:55:00+09:00
toc: true
toc_sticky: true
comments: true
header:
    teaser: /assets/images/thumbnail/2019/190426-scala-while-for-loop.png
---

## while

`while`문은 **자바와 거의 동일**합니다. 간단하게 예제를 살펴보겠습니다.

```scala
var i = 0
val list = List("Hello", ", ", "Scala!", "\n")
while (i < list.length) {
    print(list(i))
    i += 1 // i++ 사용 불가
}
```

스칼라에서는 자바처럼 `i++` 또는 `++i`와 같은 **증감 연산자를 사용할 수 없습니다.** 그렇기 때문에 `i += 1` 또는 `i = i + 1`과 같이 작성을 해야 합니다. 예제를 보면 알 수 있듯이 자바와 크게 다른점은 없습니다.


## foreach

사실 위 `while`문 예제는 명령형(`imperative`) 스타일의 프로그래밍 작성 방법입니다. **함수형 프로그래밍**에서는 위와 같이 작성하는 방식은 올바르지 않습니다. (함수형 프로그래밍 방식이 좋다는 뜻이 아닙니다. 함수형 프로그래밍 방식과는 거리가 있다는 뜻입니다.)

<i class="fas fa-feather-alt"></i> **함수형 프로그래밍** 프로그래밍 스타일 방식에는 명령형 프로그래밍, 함수형 프로그래밍이 있습니다. 함수형 프로그래밍은 어떻게(`How`)보단 무엇(`What`)을 표현하는 방식의 프로그래밍입니다. 반대로 명령형 프로그래밍은 무엇(`What`)보단 어떻게(`How`)를 표현하는 방식의 프로그래밍입니다.  
명령형 프로그래밍과 같은 경우는 절차지향, 객체지향 프로그래밍으로 `C`, `C++`, `Java` 등이 있습니다. 함수형 프로그래밍에는 클로저, 하스켈, 리스프와 같은 언어가 있습니다. 자세한 내용은 아래 링크를 참고하세요.  
<a href="/programming/190323-functional-programming/" target="_blank">함수형 프로그래밍</a>
{: .notice--info}

문자열을 담고 있는 리스트에서 원소 하나씩 꺼내, 출력하는 코드를 작성할때 `foreach`를 사용하게되면 매우 편리합니다. 아래 예제를 보면,

```scala
val list = List("Hello", ", ", "Scala!", "\n")
list.foreach(item => print(item))
```

`item`에는 리스트의 원소가 들어갑니다. 그리고, `print(item)`을 배열 원소의 개수만큼 반복하여 실행합니다.  

그리고, 여기에는 한가지 더 숨겨진 내용이 있는데, `item`에 대한 타입이 명시되어 있지 않습니다. 하지만, 스칼라 컴파일러는 **타입추론**을 통해 `item`이 문자열 `String`이라고 추론합니다. 굳이 타입을 명시하여 코드를 작성한다면 아래와 같습니다.

```scala
list.foreach((item: String) => print(item))
```

실행하는 과정을 하나씩 살펴보면 아래 테이블과 같습니다.  

|반복횟수|설명|
|:---|:---|
|1|`print("Hello")`|
|2|`print(", ")`|
|3|`print("Scala!")`|
|4|`print("\n")`|

그리고, 위 코드는 아래와 같이 더 **축약하여 작성이 가능**합니다. 

```scala
list.foreach(print)
```

인자를 하나만 받는 문장의 경우는 해당 인자에 이름을 붙일 필요없이 사용이 가능합니다.  

코드 내부 알고리즘은 신경 쓰지 않고, 마치 대화하는 듯이 코드를 작성하게 되는데... 이렇게 코드를 작성하는 방식이 **함수형 프로그래밍**방식이라고 할 수 있습니다.  

- `list`: 리스트를
- `foreach`: 반복해서
- `print`: 출력해라

> 리스트를 반복해서 출력해라!

## for

`for`문의 경우는 자바와 비슷하긴 하지만 조금 다릅니다. 예제를 살펴보면

```scala
val list = List("Hello", ", ", "Scala!", "\n")
for (item <- list)
    print(item)
```

`Python`을 알고 계신분은 `Python`과 비슷하다고 생각할 것 같습니다.  

여기서 `<-` 기호는 스칼라에서 하나의 문자로 인식을 합니다. 그렇기 때문에 꼭 **스페이스(공백) 없이 붙여서 사용**해야 합니다.  

착각할 수 있는 부분이 `item`에 원소 값이 들어가면서 반복하여 실행하기 때문에 `var` 타입의 변수라고 생각할 수 있습니다. 하지만, `val` 타입의 변수이기 때문에 `for`문 내부에서 `item`에 값을 재할당하려고하면 오류가 발생합니다.  


<i class="far fa-laugh-wink"></i> **마지막으로,** 본 글은 스칼라 공부를 하면서 작성한 글입니다. 잘못된 내용이 있거나 추가적인 내용이 필요한 경우, 댓글이나 이메일로 알려주세요. 해당 글을 가져가실 때는 출처를 남겨주시면 감사하겠습니다. :)
{: .notice--success}