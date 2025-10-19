# Memory Management & Performance
<!-- File: interview-agent/technologies/csharp/questions/memory-management.md -->

## Topic Overview
Memory allocation, garbage collection, performance optimization, and resource management.

**Weight**: 1.1

---

## Questions

### What is Garbage Collection?
Garbage collector automatically manages memory by:
- Allocating memory for objects
- Identifying and reclaiming memory from unused objects
- Organizing objects into three generations (0, 1, 2) based on their lifecycle

### How does .NET's generational garbage collector work?
Three generations:
- **Generation 0**: Short-lived objects
- **Generation 1**: Mid-lifetime objects
- **Generation 2**: Long-lived objects

### Difference between Finalize() and Dispose()
- **Finalize()**: Called by garbage collector, non-deterministic
- **Dispose()**: Manually called to release resources, deterministic

### What's a WeakReference?
A reference that doesn't prevent the garbage collector from reclaiming the object.

### Difference between value-type and reference-type
- **Value types**: Stored on stack, contains actual data
- **Reference types**: Stored on heap, contains reference to data

### Boxing and Unboxing
- **Boxing**: Converting value type to reference type (object)
- **Unboxing**: Converting reference type back to value type
- Performance overhead consideration

### What is a PID (Process ID)?
Unique identifier for a running process in the operating system.

### Describe the difference between a Thread and a Process
- **Process**: Independent execution environment with own memory space
- **Thread**: Lightweight execution unit within a process, shares memory

### Maximum memory for a single Windows process
Depends on architecture (32-bit vs 64-bit) and OS version.
