---
title: "필드(Field)"
excerpt: "필드에 대해서 알아봅니다."
last_modified_at: 2017-05-18 10:52:34
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


## References

-	[MSDN - 값형식과 참조형식](https://msdn.microsoft.com/ko-kr/library/4d43ts61(v=vs.90).aspx)

{: .notice--info }
**Note:** 본 포스트는 완성되지 않은 작업중인 포스트입니다.