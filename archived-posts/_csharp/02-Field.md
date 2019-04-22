---
title: "필드(Field)"
excerpt: "필드에 대해서 알아봅니다."
last_modified_at: 2017-06-24 11:45:40
mathjax: true
---

{% include toc %}

필드란 우리가 어떤 데이터를 메모리에 저장하고 이를 접근할 수 있게 해주는 것을 말한다. 따라서 필드는 다른 말로 핸들러라고도 할 수 있다.

## 데이터 형식(Types of data)

모든 데이터는 그에 맞는 형식(Type)을 갖는다. 모든 형식은 크게 두가지로 `참조형식(Reference type)`과 `값형식(Value type)`으로 나눌 수 있다.

**참조형식 Reference type**

객체를 포인터로 전달한다.
클래스로 정의된 형식. **null** 값이 될 수 있다.

**값형식 Value type**

객체를 값으로 전달한다.
구조체로 정의한 형식. **null** 값이 될 수 없다.

C#에서는 참조형식과 값형식을 명확히 구분하고 있다. 이 둘의 가장 큰 차이점은 메서드(Method)에 매개변수(Parameter)로 전달할 때 참조형식의 경우 메서드 내부에서 객체의 값을 변화시킬 수 있지만 값형식의 경우 전달 받은 매개변수를 바꿀 수 없다. 실질적인 원인은 값형식의 경우 스택(Stack)에 할당되고 참조형식의 경우 힙(Heap)에 할당 되기 때문이다.

이를 기반으로 다음의 기본 데이터 형식을 알아보자.

|키워드|클래스명|크기(bit)|참조형식|데이터|범위|
|:---:|:---:|:---:|:---:|:---:|:---:|
|byte|System.Byte|8|값|정수|0 ~ 255|
|int|System.Int32|32|값|정수|$\pm$20억|
|float|System.Single|32|값|실수|3.4e38|
|bool|System.Boolean|8|값|논리|true, false|
|string|System.String|-|참조|문자열|-|
|object|System.Object|-|참조|객체|-|

이상이 자주 사용하는 Primitive Type 들이다.

{: .notice--warning}
**Note:** string의 경우 참조형식이지만 행동은 값형식처럼 한다.

## 상수 (Constant)

수학적으로는 변하지 않는 수를 의미한다. 이는 프로그래밍 상에서도 마찬가지이지만 정확히 표현하자면 읽기 전용의 정적 변수를 의미한다. 따라서 키워드 `const = static + readonly`의 공식이 성립한다. 선언은 다음과 같이 한다.

```cs
// 상수 선언
public const float PI = 3.141592f;

// 다음은 위의 선언과 동일한 선언법이다.
public static readonly float PI = 3.141592f;
```

## 열거형 (Enumeration)

값을 의미가 있는 단어로 표현하여 사용하는 자료형태이다. 기본적으로 프로그램이 상에서 실수를 줄이기 위한 장치이며, 상수의 집합이다.

```cs
public enum EColor
{
	Green,	// defaults to 0
	Orange,	// defaults to 1
	Red,	// defaults to 2
	Blue 	// defaults to 3
}
```

### Enum 클래스

System 네임스페이스에 있는 Enum 클래스는 열거형에 관한 다양한 유틸리티를 제공한다.

```cs
Enum.GetNames(typeof(EColor));			// 열거형의 이름들을 가져온다.
Enum.ToObject(typeof(EColor), 0);		// 입력된 오브젝트를 파싱하여 해당 열거형의 오브젝트형을 반환한다.
Enum.TryParse<EColor>("Red", out EColor color); // 파싱
```

이외에도 많은 유틸리티 함수들이 존재한다.

{: .notice--info }
**Note:** [MSDN - Enum class](https://msdn.microsoft.com/library/system.enum(v=vs.110).aspx)

## 형변환

지금까지 프로그래밍에서 변수로 사용할 수 있는 다양한 형식에 대해서 알아보았다. 프로그래밍에서 데이터는 단순한 바이트덩어리이고 어떤 타입인가에 따라서 그 바이트 덩어리를 해석하는 방법이 나뉜다. 가령 0x00의 헥사데시멀(HexaDecimal) 자료가 있다고 한다면 이를 논리값으로 표현하면 거짓일 것이고 정수형으로 표현한다면 0일 것이다. 실제로 이러한 형변환이 가능하지는 않다.

데이터를 담는 그릇을 형식(Type)이라 하고 어떤 형식을 다른 형식에게 값을 전달해주는 과정을 형변환(Cast)이라 한다. 간단하게 실수형 데이터를 정수형으로 표현하는 방법에 대해서 알아보자.

```csharp
float f = 3.2f;
int a;

a = (int)f; // a = 3
f = a; // f = 3
```

3번 줄에서 괄호와 함께 형변환을 해줄 타입을 지정해주는 것을 `명시적 형변환(Explicit cast)`이라고 한다. 이와는 다르게 4번줄과 같이 타입의 지정없이 형변환이 일어나는 것을 `암시적 형변환(Implicit cast)`이라고 한다.

### as 와 is 키워드

안전한 형변환을 위해서 사용할 수 있는 키워드이다.

```csharp
using System;

namespace SimpleTest
{
    class Program
    {
        public class Parent { }
        public class Child : Parent { }
        
        static void Main(string[] args)
        {
            var parent = new Parent();
            var child = new Child();

            if (parent is Parent)
            {
                Console.WriteLine("parent is Parent");
            }

            if (parent is Child)
            {
                Console.WriteLine("parent is Child");
            }

            if (child is Parent)
            {
                Console.WriteLine("child is Parent");
            }

            if (child is Child)
            {
                Console.WriteLine("child is Child");
            }
        }
    }
}

// output
parent is Parent
child is Parent
child is Child
```

`is` 키워드는 해당 객체가 해당 형식으로 형변환이 가능한지 여부를 알려준다.


## Boxing & Unboxing

MSDN에 따르면,

>Boxing은 값 형식을 참조 형식으로 변환하는 프로세스를 가리킵니다. 변수를 boxing하면 힙의 새 복사본을 가리키는 참조 변수가 만들어집니다. 참조 변수는 개체이므로 모든 개체가 상속하는 모든 메서드(예: ToString())를 사용할 수 있습니다.

라고 설명하고 있다. 값형식을 참조 형식으로 변환하는 프로세스란 `object`형 포인터로 새 복사본을 가르킨다는 의미이다.

## ref 와 out 키워드

Boxing 과 Unboxing의 수행과정에서 Heap으로의 할당이 발생한다. 이는 명백한 오버헤드(Overhead)이고 성능에 영향을 끼칠 우려가 있다. 메서드에 값인자를 전달할 때 ref 와 out 키워드를 활용할 수 있다. 이는 C에서 함수 인자로 포인터를 직접 전달하는 것과 같은 의미를 지닌다. 따라서 Boxing & Unboxing으로 인한 불필요한 할당을 줄일 수 있게 해준다. ref 와 out 키워드의 경우 비슷하지만 out 키워드는 초기화가 안된 인자를 받을 수 있다는 점이 다르다.

```csharp
int i;
if (int.TryParse("3", out i))
{
     Console.WriteLine(i); // i = 3
}
```

## 연산자(operator)

연산자란 특정 명령을 하는 기호를 말합니다. 

|연산자|내용|
|:---:|:---:|
|RHS = LHS| RHS 에 LHS를 할당합니다.|
|RHS + LHS| RHS에 LHS를 더한 결과를 반환합니다.|
|RHS - LHS| RHS에서 LHS를 뺀 결과를 반환합니다.|
|RHS * LHS| RHS에 LHS를 곱한 결과를 반환합니다.|
|RHS / LHS| RHS를 LHS로 나눈 몫을 반환합니다.|
|RHS % LHS| RHS에서 LHS로 나눈 나머지를 반환합니다.|
|RHS += LHS| RHS에서 LHS를 더한 결과를 RHS에 할당합니다.|
|RHS -= LHS| RHS에서 LHS를 뺀 결과를 RHS에 할당합니다.|
|RHS *= LHS| RHS에서 LHS를 곱한 결과를 RHS에 할당합니다.|
|RHS /= LHS| RHS에서 LHS를 나눈 몫을 RHS에 할당합니다.|
|RHS %= LHS| RHS에서 LHS를 나눈 나머지를 RHS에 할당합니다.|
|RHS++| RHS를 1만큼 증가시킵니다.|
|RHS--| RHS를 1만큼 감소시킵니다.|
|([Type])RHS| RHS를 [Type]으로 형변환합니다.|

보편적인 수학적 기호와 별반 차이가 없지만 위의 연산자들은 숫자형에 국한되어 있지 않고 새로운 기능을 추가할 수도 있습니다. 이러한 것을 **연산자 오버로딩(Operator Overloading)**이라 합니다.

## References

-	[MSDN - 값형식과 참조형식](https://msdn.microsoft.com/ko-kr/library/4d43ts61(v=vs.90).aspx)