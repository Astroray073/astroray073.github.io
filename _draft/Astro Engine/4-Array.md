---
title				: First contianer, Array
excerpt				: "Templated fixed size array class development"
last_modified_at	: 2019-05-13

toc 				: true
toc_sticky			: true

categories:
 - Astro
 - Engine
---

The first container to develop is Array. It is very basic and also useful container.
There are 2 kinds of array. One is static array and the other is dynamic array.
First we gonna make static array. Static arrary is the built-in array. But working with C++ built-in array is painful.
So we gonna make it easier to use.

## Requirements

- Consturction of array happens at compile time.
- Have information about its size.
- Can access element via index.
- Supports ranged-for loop.
- Templated for various types.

## Implementation details

**Consturct**

- Default : constructs array given size N with uninitialized values.
- Aggregate : Initialieze from initializer list.
- Copy : Deep copy elements from other array.
- Move : Not movable.