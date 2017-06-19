---
title: "흐름제어(Flow control)"
excerpt: "프로그램의 흐름을 제어하는 방법에 대하여 알아봅니다."
last_modified_at: 2017-06-20 07:53:50
mathjax: true
---

{% include toc %}


프로그램이란 `일련의 과정을 제어하여 원하는 일을 수행하게 하는 것`을 말한다. 이것은 단순한 산수일수도 매우 복잡한 데이터의 처리일 수도 있다. 다만 프로그래머로써 해야 하는 일은 같다. 컴퓨터로 하여금 일련의 과정을 수행하게끔 하는 것.

아무런 지시가 없다면 프로그램은 주어진 명령들(Instructions)을 차례대로 수행한다. 코드 수행을 제어하는 것을 `흐름제어(Flow control)`이라 하며 이를 좀 더 광범위하게 제어하는 것을 `알고리즘(Algorithm)`이라 한다. 사실 흐름제어나 알고리즘이나 별반 다를 것은 없다.

여기에서는 C#에서 우리가 가진 흐름 제어의 툴들에 대해서 알아본다. 우리가 프로그래머로써 코드의 동작을 제어할 수 있는 방법이 무엇이 있는가? 를 공부해 보자.

## 조건문

### IF/ELSE IF/ELSE

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
**Ctrl + Shift + B :** 프로젝트 빌드 단축키.

```bash
~Your Directory>SimpleTest.exe 10 99
10 is smaller than or eqaul to 99

~Your Directory>SimpleTest.exe 10 2
10 is greather than 2
```

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

}
```

해당 구문이 `if`로 할 수 있는 모든 것이다. `if` 뒤에 다수의 `else if`가 올 수 있고 `else`가 있어도 되고 없어도 된다. **다만 `else if`의 경우 이 이전에 하나의 조건이라도 참이라 스코프 내의 코드가 실행되면 조건 검사에서 제외 된다.**

{: .notice--info }
**스코프(Scope):** 코드의 유효 범위를 나타낸다. 보통의 프로그램 언어들은 중괄호({ })로 표현한다. 파이썬은 들여쓰기(Indentation)으로 구분한다.

### Switch

```cs
switch(arg)
{	
	case testValue:
		break;
	default:
		break;
}
```

arg는 스위치 문에서 검사할 대상이고 case 옆에 값은 비교를 수행할 대상이다. `default` 키워드는 모든 검사에서 실패할시 자동으로 실행될 코드를 포함한다. 위의 구문을 `if`문으로 표현하면 다음과 같다.

```cs
if (arg == testValue)
{

}
else
{

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

이런 식으로 `return`을 사용하여 전체 프로세스를 끝낼 수도 있다. **스위치 문에서 유의할 점은 각 `case` 들에서 참이여도 `break`나 `return`키워드로 빠져나오지 않으면 아래의 `case`도 실행된 다는 점이다.**

## 반복문

작업 중입니다...