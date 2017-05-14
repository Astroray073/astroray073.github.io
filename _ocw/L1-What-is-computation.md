---
title: "[L1] What is Computation?"
permalink: /ocw/L1
excerpt: "프로그래머에게 컴퓨터란 계산을 도와주는 도구이다. 컴퓨터는 1초에 엄청난 양의 계산을 수행할 수 있고, 정말 많은 것을 기억해낼 수 있다. 분명 이것이 우리가 컴퓨터를 활용하는 이유이다."
last_modified_at: 2017-05-15

header:
 video:
  id: ytpJdnlu9ug
  provider: youtube
---

### Lecture Materials

[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec1.pdf)

### 서론

프로그래머에게 컴퓨터란 계산을 도와주는 도구이다. 컴퓨터는 1초에 엄청난 양의 계산을 수행할 수 있고, 정말 많은 것을 기억해낼 수 있다. 분명 이것이 우리가 컴퓨터를 활용하는 이유이다.

다만 여기에서는 중요한 점이 하나 있다.

>컴퓨터는 오직 시킨 것만 수행 시킬 수 있다.

이것이 프로그래머의 존재 이유이다. 컴퓨터는 스스로 아무것도 하지 못한다. 현재에는 메타프로그래밍 기법이나 여러 인공지능 기법 또한 많이 개발되어 있어 컴퓨터 스스로 뭔가를 한다고 생각할 수도 있지만 이들 또한 누군가에 의해서 프로그래밍 되어 하드웨어에 이식된 것 뿐이다.

<!--more-->

### 지식의 종류 (Types of knowledge)

*	<a>선언된 지식(declarative knowledge)</a>[^1] : 사실
*	<a>명령적 지식(imperative knowledge)</a>[^2] : 방법 혹은 절차

Dr.Ana 는 여기서 직접 Python[^3]을 사용하여 난수를 뽑는 코드를 보여준다.

{% highlight python %}
import random
random.randint(16, 272)
{% endhighlight %}

$$y^2 = x$$ 같이 사실이 존재할 때, $$x$$의 루트를 구한다면,

1.	$$g$$를 추측.
2.	$$g^2$$이 $$x$$와 충분히 같다면, 그만하고 $$g$$를 해로 선택한다.
3.	충분히 같지 않다면, $$g$$ 와 $$x/g$$ 의 평균을 다음 추측값으로 사용한다.[^4]
4.	새로운 추측값을 사용하여 2번의 조건을 만족할 때까지 반복한다.

|g|$$g^2$$|$$x/g$$|$$(g + x/g)/2$$|
|---|---|---|---|
|3|9|16/3|4.17|
|4.17|17.36|3.837|4.0035|
|4.0035|16.0027|3.997|4.000002|

이러한 절차를 흔히 알고리즘이라고 한다.

위의 예시를 토대로 알고리즘에 대해서 간단하게 정의해보면,

*	단순한 일련의 행동을 나열하고
*	그것들의 행동 실행 순서의 흐름을 조정하여
*	언제 끝낼 지를 결정하는 것이다.

### Two diffrent types of computer

그렇다면 컴퓨터가 수행할 수 있는 것.
<a>즉 우리가 프로그래머로써 컴퓨터에게 시킬 수 있는 것</a>은 무엇인가?
`내장된 프로그램 언어`와 `프로그래머가 정의한 언어`를 수행할 수 있다.

Fixed program computer : only do one thing 

* A Simple Calculator

Stored program : seq. of instructions -> do a lot of tasks.

* Today's computer

### Basic machine architecture

<!-- {:.text-center img} -->
<!-- ![BMC]({{ site.urlimg }}6_0001/basic_machine_architecture.png "BMC") -->

<a>Memory</a> contains data & sequence of <ins>primitive</ins> instructions.

1. Program counter starts to execute the sequence of primitive instructions in order.
2. During the execution if some instruction has a task, then it passes the instruction to ALU.
3. When the seqeunce of instruction is finished, the computer emits the output.

>Turning suggested that only 6 instructions are enough to compute anything. Those are 'Move left', 'Move right', 'Read", 'Write", 'Scan' and 'Do nothing'

That results in that if something can be computed in a particular language then other languages can do the same thing.

### Aspects of languages

1.	<a>syntactically valid</a> : phases should be correctly.
2.	<a>static semantics</a> : phases should have meaningful expression.
3.	<a>unintentional error</a> : the error which is not intended by the programmer.

### Objects

*	<a>scalar (primities):</a> float, bool, int...
*	<a>non-scalar:</a> custom types which is has data structure.

~~~python
# How to know the type of an object
type(5)
int

# How to prints a value
print(3 + 2) 
5
~~~

### Operators

*	i + j : Summation
*	i - j : Substarct
*	i * j : Multiply
*	i / j : Division
*	i % j : Remainder
*	i ** j : Power
*	pi_approx = 22/7 : Assignment

### Changing bindings

~~~python
pi = 3.14
radius = 2.2
area = pi*(radius**2)  # Pointer moves
radius = radius+1      # We lose previous handle and replace the value as new.
~~~

### References

1.	[Lecture note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec1.pdf)

### Comments

[^1]: "강의에서는 강사가 학생들 중 누군가에게 구글 카드보드를 줄 것이다." 라는 것으로 표현.
[^2]: 일련의 방법을 설명하기 위해서 구글 카드보드를 무작위의 학생에게 주는 과정을 직접 보여줌.
[^3]: 프로그래밍 언어의 일종으로 주로 공학계열에서 많이 사용된다. 복잡한 수식 관련해서 표현법이나 연산이 매우 훌륭하기 때문이다.
[^4]: [뉴턴-랩슨법](http://darkpgmr.tistory.com/58)으로 증명 가능하다.

*[Dr.Ana]: 강사분이십니다.