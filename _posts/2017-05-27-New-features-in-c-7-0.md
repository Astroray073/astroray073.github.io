---
title: "C# 7.0 새로운 기능"
excerpt: "C# 7.0의 새로운 기능들을 소개합니다."
last_modified_at: 2017-05-27 19:42:24

categories:
 - "C#"
---

{% include toc %}

Visual Studio 2017 릴리스와 함께 C# 7.0 버전이 발표되었습니다. [MSDN 블로그](https://blogs.msdn.microsoft.com/dotnet/2017/03/09/new-features-in-c-7-0/) 내용을 바탕으로 새로운 기능들에 대해서 소개합니다.

개인적으로 편한 기능들이 많이 추가된 것 같습니다. C#은 날이 갈수록 발전을 하네요. 점점 더 코딩하기 쉬워지는 환경이 되는 것 같아 만족스럽습니다.

## Out Variables

이전 버전의 방식:

```cs
public void PrintCoordinates(Point p)
{
    int x, y; // have to "predeclare"
    p.GetCoordinates(out x, out y);
    WriteLine($"({x}, {y})");
}
```

이제 `out` 파라매터를 가지는 함수에 바로 `out` 형식의 변수를 선언하고 사용 할 수 있습니다.
타입에는 `var` 키워드를 사용하여 컴파일러로부터 형식 유추를 수행하게 할 수도 있습니다.

```cs
public void PrintCoordinates(Point p)
{
    p.GetCoordinates(out int x, out int y);
    WriteLine($"({x}, {y})");
}
```

만약 복수의 `out` 파라매터 중 무시하고 싶은 파라매터가 있다면 `_` 를 사용하여 무시할 수 있습니다.

```cs
p.GetCoordinates(out var x, out _); // Only care about x
```

## Pattern matching

형식을 검사하는 동시에 해당하는 타입의 새로운 변수에 값을 복사하는 기능입니다.

### Is 키워드를 활용한 패턴 매칭

```cs
public void PrintStars(object o)
{
    if (o is null) return;     // constant pattern "null"
    if (!(o is int i)) return; // type pattern "int i"
    WriteLine(new string('*', i));
}
```

두번째 `if`를 이전 버전의 C#으로 다시 쓴다면

```cs
if (o is int)
{
	int i = (int)o;
	WriteLine(new string('*', i));
}
else
{
	return;
}
```

와 같습니다.

### Switch 구문에서의 패턴 매칭

`switch` 구문에서도 이제 단순한 상수만을 매칭할 수 있는 것이 아닌 패턴 매칭으로 여러 형식에 대해서 검사하고 바로 해당 타입으로 값을 복사하여 작업을 수행 할 수 있습니다.

```cs
switch(shape)
{
    case Circle c:
        WriteLine($"circle with radius {c.Radius}");
        break;
    case Rectangle s when (s.Length == s.Height):
        WriteLine($"{s.Length} x {s.Height} square");
        break;
    case Rectangle r:
        WriteLine($"{r.Length} x {r.Height} rectangle");
        break;
    default:
        WriteLine("<unknown shape>");
        break;
    case null:
        throw new ArgumentNullException(nameof(shape));
}
```

중요한 점은 이전과 같이 case 구문의 순서가 중요합니다. case 구문의 순서에 따라 순서대로 실행하여 매칭이 되면 해당 구문을 실행하고 `break`를 빠져나옵니다. `if-elseif`와 같다고 보시면 됩니다. 다만 `default`의 경우 항상 나중에 실행됩니다. 따라서 `case null`이 조건 검사에서 빠지지 않습니다.

## Tuples

매서드에서 1개 이상의 값을 리턴할 수 있는 기능입니다. 해당 기능은 이전 버전에서도 사용 가능하며 `System.ValueTuple`을 `NuGet`에서 받아서 설치하면 됩니다.

```cs
(string, string, string) LookupName(long id) // tuple return type
{
    ... // retrieve first, middle and last from data storage
    return (first, middle, last); // tuple literal
}
```

```cs
var names = LookupName(id);
WriteLine($"found {names.Item1} {names.Item3}.");
```

해당 변수들에게 이름을 정해주고 싶다면

```cs
// 1번 방법 : 함수 시그니처에 명시
(string first, string middle, string last) LookupName(long id)

// 2번 방법 : tuple 리턴 형에 명시
 return (first: first, middle: middle, last: last);
```

다음과 같이 변수명을 가지고 사용할 수 있습니다.

```cs
var names = LookupName(id);
WriteLine($"found {names.first} {names.last}.");
```

## Deconstruction

`Complex type`을 분해 할 수 있는 기능입니다. `Tuple`과 함께 사용할 수도 있고 `Deconstruct` 함수를 `instance` 나 `extension` 함수로 정의하면 어느 타입에서나 사용가능 합니다.

```cs
(string first, string middle, string last) = LookupName(id1); // deconstructing declaration
WriteLine($"found {first} {last}.");
```

```cs
class Point
{
    public int X { get; }
    public int Y { get; }

    public Point(int x, int y) { X = x; Y = y; }
    public void Deconstruct(out int x, out int y) { x = X; y = Y; }
}

(var myX, var myY) = GetPoint(); // Deconstruct(out myX, out myY)를 호출합니다.
```

## Local Functions

타입 안에 `nested type`을 작성하던 것과 같이 함수 안에 유틸리티 함수를 작성할 수 있습니다.

```cs
public int Fibonacci(int x)
{
    if (x < 0) throw new ArgumentException("Less negativity please!", nameof(x));
    return Fib(x).current;

    (int current, int previous) Fib(int i)
    {
        if (i == 0) return (1, 0);
        var (p, pp) = Fib(i - 1);
        return (p + pp, p);
    }
}
```

```cs
public IEnumerable<T> Filter<T>(IEnumerable<T> source, Func<T, bool> filter)
{
    if (source == null) throw new ArgumentNullException(nameof(source));
    if (filter == null) throw new ArgumentNullException(nameof(filter));

    return Iterator();

    IEnumerable<T> Iterator()
    {
        foreach (var element in source) 
        {
            if (filter(element)) { yield return element; }
        }
    }
}
```

## Literal improvements

숫자형 문자열 작성시 `_`를 구분자로 사용할 수 있습니다.

```cs
var d = 123_456;
var x = 0xAB_CD_EF;
var b = 0b1010_1011_1100_1101_1110_1111;
```

## Ref returns and locals

이제 리턴형에도 `ref`키워드를 사용할 수 있습니다.

```cs
public ref int Find(int number, int[] numbers)
{
    for (int i = 0; i < numbers.Length; i++)
    {
        if (numbers[i] == number) 
        {
            return ref numbers[i]; // return the storage location, not the value
        }
    }
    throw new IndexOutOfRangeException($"{nameof(number)} not found");
}

int[] array = { 1, 15, -39, 0, 7, 14, -12 };
ref int place = ref Find(7, array); // aliases 7's place in the array
place = 9; // replaces 7 with 9 in the array
WriteLine(array[4]); // prints 9
```

{: notice--info }
**Note:** 안정성 확보를 위해 `ref`로 반환된 로컬 변수 포인터가 다른 값을 가르키게 할 수는 없습니다. 

## More expression bodied members

이제 `accessors`[^1], `constructor`, `finalizers`에도 `expression body`를 사용할 수 있습니다.

```cs
class Person
{
    private static ConcurrentDictionary<int, string> names = new ConcurrentDictionary<int, string>();
    private int id = GetId();

    public Person(string name) => names.TryAdd(id, name); // constructors
    ~Person() => names.TryRemove(id, out _);              // finalizers
    public string Name
    {
        get => names[id];                                 // getters
        set => names[id] = value;                         // setters
    }
}
```

## Throw expressions

예외처리를 3항 연산자 및 `expression body`에서 사용 할 수 있습니다.

```cs
class Person
{
    public string Name { get; }
    public Person(string name) => Name = name ?? throw new ArgumentNullException(nameof(name));
    public string GetFirstName()
    {
        var parts = Name.Split(" ");
        return (parts.Length > 0) ? parts[0] : throw new InvalidOperationException("No name!");
    }
    public string GetLastName() => throw new NotImplementedException();
}
```

## References

-	[New Features in C# 7.0](https://blogs.msdn.microsoft.com/dotnet/2017/03/09/new-features-in-c-7-0/)

## Comments

[^1]: 프로퍼티의 `get`, `set`을 말합니다.
