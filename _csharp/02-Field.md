---
title: "핃드(Field)"
excerpt: "필드에 대해서 알아봅니다."
last_modified_at: 2017-05-18 10:52:34
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
|int|System.Int32|32|값|정수|20억|
|float|System.Single|32|값|실수|3.4e38|
|bool|System.Boolean|8|값|논리|true, false|
|string|System.String|-|참조|문자열|-|
|object|System.Object|-|참조|객체|-|

이상이 자주 사용하는 Primitive Type 들이다.

{: .notice--warning}
**Note:** string의 경우 참조형식이지만 행동은 값형식처럼 한다.

{: .notice--info }
**Note:** 본 포스트는 완성되지 않은 작업중인 포스트입니다.