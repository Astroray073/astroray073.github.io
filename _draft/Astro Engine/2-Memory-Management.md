---
title				: Memory Management
excerpt				: "How to develop custom memory management system."
last_modified_at	: 2019-04-29

toc 				: true
toc_sticky			: true

categories:
 - Astro
 - Engine
---

## Why we should care of memory managment?

We do not discuss about memory allocation occurance on [Stack]. It is just fine and we do not mess it up.
But on the other hand, the memory alloaction on heap cause some problems and drag the performance of the Engine.

**Why Heap allocation pull the performance down?**

1. When heap allocation occurs, program requests to the OS via malloc or new keyword.
2. When the OS handles the allocation, there is [Kernel Switch].
3. The [Kernel Switch] is expensive process.
4. This should not happen frequently.

To minimize [Kernel Switch], we allocate big memory chunk so that reduce the amount of call of memory allocation.

## Memory pooling

The most important policy is

1. We allocate large amount of memory for future use.
2. When allocation requested, we simply create block for the object.
3. When deallocation occurs, we clean up the block and save the storage for furture use of allocation.
4. Of course, if we do not have enough space of Pool, then allocate more Pool.

The benefit of this approach is that we can reduce the memory allocation call to OS by reusing allocated memory pool.

Memory pooling consists of Memery pools and blocks.
Pools are the allocated memory and blocks are the imaginary segments of our object stored in the Pool.

## Memory fragmentation

There is one more problem left called [Memory Fragementation].
Memory fragmentation happens when various size of objects are allocated and deallocated.
Because we alloacte objects with various size in random order.
When this happens, the fragemented memories are not used thus we lose memory that we can utilize.
To defragment memories, we keep track memory blocks by the header of memory block.
The overhead of the header will be memory location, size, next free store and so on.

## Then what features that memory manager should have?

1. Minimize [Kernel Switch] -> Can be done by allocate large memory chunk.
2. Keep headers small to store more data we need.
3. Can serach free memory as fast as possible -> This conflicts [2].
4. Defragmentation.

## What makes memory manager development so hard?

It is because that we cannot use any built-in data structures.
For example, suppose that we want to use std::map to store pointers representing each memory blocks.
But wait. How the std::map contains data? To the memory!
We simply cannot use a memory manager to build a memory manager.
That makes the development hard.

## Implementation details

**Memory Manager**

- List of memory pools
- Allocate memory pool
- Deallocate memory ppol
- Accept allocation request and handle it through Memory Pool.
- Accept deallocation request and handle it trought Memory Pool.

**Memory Pool**

- Header
    - Address of Pool start
    - Size of Pool
    - Available size of block

**Memory Block**

- Header
    - Address of Block start
    - Size of Block
    - Flag : Whether this block is fragmented?
- Object data