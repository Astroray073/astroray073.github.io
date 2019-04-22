---
title: "흐름제어(Flow control)"
excerpt: "프로그램의 흐름을 제어하는 방법에 대하여 알아봅니다."
last_modified_at: 2017-06-21 08:27:43
mathjax: true
---

{% include toc %}


프로그램이란 **일련의 과정을 제어하여 원하는 일을 수행하게 하는 것**을 말한다. 이것은 단순한 산수일수도 매우 복잡한 데이터의 처리일 수도 있다. 다만 프로그래머로써 해야 하는 일은 같다. 컴퓨터로 하여금 일련의 과정을 수행하게끔 하는 것.

아무런 지시가 없다면 프로그램은 주어진 명령들(Instructions)을 차례대로 수행한다. **코드 수행 순서를 제어하는 것을 흐름제어(Flow control)이라 하며 이를 어떠한 방법으로 할지에 대한 것을 알고리즘(Algorithm)이라 한다.** 사실 흐름제어나 알고리즘이나 별반 다를 것은 없다. 여기서 다루는 기초 문법에 의거하여 제어하는 것을 흐름제어라고 많이들 말하고 거시적 관점에서 방법론 적인 측면을 강조한 것을 알고리즘이라 말한다. 그러므로 알고리즘을 익히고 적용하기 위해서는 우리가 프로그래머로써 코드의 동작을 제어할 수 잇는 방법들에 대하여 알아야 한다. 거창하게 적어놓았지만 그저 맨 처음 코드를 배울때 필수적으로 배우는 조건문, 반복문 들에 대한 이야기이다. 여기에서는 그러한 방법에 대하여 알아보자.

## 조건문

### if - else if - else

**Syntax**
```cs
if ( condition )
{
	// condition is true...
}
else if ( condition2 )
{
	// condition is not true and condition2 is true
}
...
else
{
	// Execution code when all conditions above failed
}
```

해당 구문이 `if`로 할 수 있는 모든 것이다. `if` 뒤에 다수의 `else if`가 올 수 있고 `else`가 있어도 되고 없어도 된다. **다만 `else if`의 경우 이 이전에 하나의 조건이라도 참이라 스코프 내의 코드가 실행되면 조건 검사에서 제외 된다.**

{: .notice--info }
**스코프(Scope):** 코드의 유효 범위를 나타낸다. 보통의 프로그램 언어들은 중괄호({ })로 표현한다. 파이썬은 들여쓰기(Indentation)으로 구분한다.

다음의 코드를 실행해보자.

```cs
using System;

namespace SimpleTest
{
	class Program
	{
	    static void Main(string[] args)
	    {
	        var a = int.Parse(args[0]);
	        var b = int.Parse(args[1]);
	        if (a > b)
	        {
	            Console.WriteLine($"{a} is greater than {b}");
	        }
	        else
	        {
	            Console.WriteLine($"{a} is smaller than or equal to {b}");
	        }
	    }
	}
}
```

`args`에서 `a, b`를 받아 정수형으로 `파싱(Parsing)`하여 두 수의 크기를 비교하는 간단한 프로그램이다. `if (a > b)`의 부분을 조건문이라 한다. 조건문의 `()` 안에는 bool 형 값이 들어간다. `Command prompt`로 빌드된 프로그램을 실행해보자. 아마 프로젝트명으로 빌드된 exe(Executable) 파일이 해당 프로젝트 폴더의 `/bin/` 내에 `Debug` 혹은 `Release` 폴더 내에 파일이 생성되어 있을 것이다. `CMD`에 인자값으로 정수 2개를 넘겨주면서 프로그램을 실행해본다. 필자의 경우 프로젝트명을 SimpleTest로 했기에 SimpleTest.exe 파일이 생성되어 있다.

{: .notice--info}
**Note:** Main 함수는 모든 프로그램의 시작점이고 인자로 문자열 배열을 받을 수 있다. 해당 모듈을 실행할 때 인자값을 넘겨주면 args 배열 변수에 담겨져 프로그램이 시작된다.

{: .notice--info}
**Ctrl + Shift + B :** 프로젝트 빌드 단축키.

```bash
~Your Directory>SimpleTest.exe 10 99
10 is smaller than or eqaul to 99

~Your Directory>SimpleTest.exe 10 2
10 is greather than 2
```

### Switch

**Syntax**

```cs
switch([Argument])
{	
	case [TestValue]:
		break;
	default:
		break;
}
```

[Argument]는 스위치 문에서 검사할 대상이고 case 옆에 값은 비교를 수행할 대상이다. `default` 키워드는 모든 검사에서 실패할시 자동으로 실행될 코드를 포함한다. 위의 구문을 `if`문으로 표현하면 다음과 같다.

```cs
if (arg == testValue)
{
	// if arg equals to testValue
}
else
{
	// else...
}
```

스위치문의 경우 `if`문으로도 처리 가능하지만 `switch`문 특유의 유틸성이 독보일 때가 있어 사용하는 경우가 많다. `enum`을 사용할 때가 바로 그 때이다.

```cs
switch (color)
{
    case EColor.Red:
        break;
    case EColor.Green:
        break;
    case EColor.Blue:
        break;
    default:
        break;
}
```

앞서 만든 프로그램에 간단한 헬프문서를 추가해 보자.

```cs
switch (args[0])
{
    case "-h":
    case "--help":
        Console.WriteLine("This is the program comparing two intergers.");
        Console.WriteLine("Usage: SimpleTest.exe a b");
        Console.WriteLine("a : Interger");
        Console.WriteLine("b : Interger to compare");
        return;
    default:
        break;
}
```

```bash
~Your Directory>SimpleTest.exe --help
This is the program comparing two intergers.
Usage: SimpleTest.exe a b
a : Interger
b : Interger to compare
```

이런 식으로 `return`을 사용하여 전체 프로세스를 끝낼 수도 있다. **스위치 문에서 유의할 점은 각 `case` 들에서 참이여도 `break`나 `return`키워드로 빠져나오지 않으면 아래의 `case`도 실행된다는 점이다.**

## 반복문

반복문은 일정 횟수동안 동일한 코드 내용을 반복하여 코드의 양을 줄여주는 문법이다. 종류로는 `for`, `foreach`, `while`이 있다. 각각에 대하여 살펴보자.

### for

일정 횟수 동안 반복하는 반복문이다. 기준이 되는 카운터가 있고 이 카운터를 매 반복마다 검사한다. 검사값이 `false`일 경우 반복을 종료하고 스코프를 빠져나온다.

**Syntax**

```cs
for([Counter]; [Condition]; [CounterModification])
{
	[CodeBlock]
}
```

보통의 경우 카운터를 0으로 정하고 컨디션에서 반복하고 싶은 숫자 만큼 적어 구성한다.

```cs
for (int i = 0; i < 5; i++)
{
	Console.WriteLine($"Index : {i}");
}
// Output
// Index : 0
// Index : 1
// Index : 2
// Index : 3
// Index : 4
```

`for`문을 사용할 때, 가장 많이 사용하는 경우가 배열같이 목록형 자료구조에 해당 자료구조의 요소마다 무언가를 하려는 경우이다.

```cs
int[] myData = {3, 24, 8};
for (int i = 0; i < myData.Length; i++)
{
	Console.WriteLine($"MyData at {i} = {myData[i]}");
}
// Output
// MyData at 0 = 3
// MyData at 1 = 24
// MyData at 2 = 8
```

또한 대다수의 경우 자료를 조작하지 않고 읽어와 새로운 것을 하는 경우가 대부분인지라 (경험상으로도) `foreach`문이 등장한다.

{: .notice--info}
**Note:** `for`문의 카운터는 `int`형에 국한되지 않는다. `float`, `double`, 객체 등 다양하게 사용할 수 있다. 보편적으로는 `int`형의 카운터를 많이 사용한다.

### foreach

`foreach`문은 열거형 자료에 대하여 모든 요소에 대하여 읽기전용으로 값을 불러올 때 사용한다. `foreach`문이 `for`문에 대하여 지니는 장점으로는,

1.	반복 횟수의 지정이 필요없어 실수를 방지할 수 있다.
2.	읽기 전용이므로 값을 불러올때 의도치 않은 값의 변경을 막을 수 있다.

**Syntax**

```cs
foreach(var item in collection)
{
	[CodeBlock]
}
```

{: .notice--info}
**var:** 변수의 타입을 컴파일러가 유추하도록하는 키워드이다. 모든 경우에 되도록 `var`키워드를 사용하길 권장한다. 후에 코드 수정을 하기도 편하고 단어도 짧아 사용하기에도 좋다. 무엇보다도 타입명에 관한 실수를 줄여준다.

앞서 본 `for`문 예제를 `foreach`문으로 바꿔본다면 다음과 같다.

```cs
int[] myData = {3, 24, 8};
int i = 0;
foreach(var myDataItem in myData)
{
	Console.WriteLine($"MyData at {i++} = {myDataItem}");
}
// Output
// MyData at 0 = 3
// MyData at 1 = 24
// MyData at 2 = 8
```

인덱스가 필요하다면 따로 카운터를 만들어야하기때문에 인덱스정보가 필요하다면 `for`문을 사용하는 것을 추천하고 그 외의 모든 경우에 `foreach`문을 사용하기를 권장한다. `for`문이 일반적으로 속도도 빠르지만 `foreach`문이 가지는 장치적 안전성때문에 `foreach`문을 사용하는 것을 권장하는 편이다. 위의 `foreach`문 예제를 실제 구조는 다음과 같다.

```cs
int[] myData = { 3, 24, 8 };
int i = 0;
System.Collections.IEnumerator myIter = myData.GetEnumerator();
while (myIter.MoveNext())
{
	var myDataItem = myIter.Current;
    Console.WriteLine($"My Data at {i++} = {myDataItem}");
}
// Output
// MyData at 0 = 3
// MyData at 1 = 24
// MyData at 2 = 8
```

`foreach`문의 동작 구조에 대하여 설명하면 다음과 같다.

1.	`foreach`문이 시작되면서 `IEnumerable` 인터페이스에 있는 함수인 `GetEnumerator()`를 호출하여 `IEnumerator`를 가져온다. 이 때, 제네릭 형식이라면 `strong type`의 `IEnumerator<T>`를 가져온다.
2.	`IEnumerator` 인터페이스의 `MoveNext()`를 호출한다.
-	해당 값이 `true`라면, 3번으로 넘어간다.
-	해당 값이 `false`라면, 반복문을 종료한다.
3.	`IEnumerator` 인터페이스의 `Current` 프로퍼티를 가져와 지정된 변수명에 할당한다.
4.	해당 변수를 가지고 코드블록을 실행하고 2번으로 되돌아 간다.

`for`문의 경우 직접적으로 해당 포인터로 접근하지만 `foreach`문의 경우 부가적인 절차로 인한 `overhead`가 발생한다. 이러한 동작 구조때문에 `for`문 보다 느린 편이다. 그럼에도 코드 실수를 방지해주는 장치가 있는 `foreach`문의 사용을 권장한다.

{: .notice--info}
**strong typed:** Boxing & Unboxing 으로 구성되는 방법이 아닌 명확하게 타입을 지정하는 것을 말한다. C#의 제네릭, C++의 템플릿 모두 **strong typed data structure**이다. 왜나하면 제네릭이나 템플릿을 실제 사용하기 위해서는 타입변수가 필요하고 이 타입변수를 지정하는 순간 해당 구조는 **strong typed**가 된다. 더 자세한 내용은 `System.Collections` 네임스페이스와 `System.Collections.Generic` 네임스페이스를 비교해 보길 바란다.

{: .notice--info}
**Overhead:** 오버헤드란 어떠한 일을 수행할 때 부가적으로 소모되는 자원을 말한다. 위의 `foreach`문에서는 `GetEnumerator()`를 통한 `IEnumerator` 형식의 객체 생성, `MoveNext()`, `Current`를 통한 로컬 변수에 할당을 말한다.

갑자기 인터페이스가 나오고 제네릭이 나와 당황스러울 수 있지만 **"`foreach`문은 `IEnumerable` 인터페이스를 기반으로 동작한다."**라고 기억해두었으면 한다. 따라서 자신이 만든 클래스여도 `IEnumerable` 인터페이스를 구현한다면 `foreach`문을 사용할 수 있도록 만들 수 있다. `IEnumerable` 인터페이스는 C# 콜렉션에서 핵심적인 인터페이스로 추후에 만날일이 굉장히 많을 것이다.

{: .notice--info}
**Note:** `IEnumerable`, `IEnumerable<T>` 인터페이스는 LINQ(Language Integrated Query)를 사용하기 위해서라도 구현할 일이 꽤 있는 편이다. 다만 직접 구현할 일은 드물고 기존의 시스템 콜렉션을 이용하여 구현하는 편이다.


### while, do - while

`while`문은 아직 얼만큼의 반복을 할 지 모를 때 사용하는 반복문이다. 다시 말하면, 반복을 언제 끝낼 지는 알지만 그 정확한 횟수가 바로 구해지지 않거나 모른다면 해당 조건을 만족하는 동안 지속해서 반복하는 문법이다.

**Syntax**

```cs
while (condition)
{
	[CodeBlock]
}

do
{
	[CodeBlock]
} while (condition);
```

`while`문의 경우 조건 검사가 먼저 실행되기 때문에 시작과 동시에 조건을 만족하지 못하면 바로 빠져나오지만 `do-while`문의 경우에는 코드가 먼저 실행된다. 적어도 한번 이상 실행이 되게 하고 싶으면 `do-while`을 사용하고 그 외에는 `while`을 사용한다.

### break, continue

반복문 전체에 통용되는 추가적인 키워드들이 있다. `break`와 `continue`가 바로 그것들이다. `break`키워드는 해당 반복문을 바로 빠져나오게 하고, `continue`키워드는 해당 반복문의 이번 코드 실행에 대하여 그 이후 코드를 무시하고 다음으로 넘어가는 키워드이다.