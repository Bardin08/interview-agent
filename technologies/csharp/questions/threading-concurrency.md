# Threading & Concurrency
<!-- File: interview-agent/technologies/csharp/questions/threading-concurrency.md -->

## Topic Overview
Multithreading, async/await, synchronization, parallel programming, and thread safety.

**Weight**: 1.2 (High importance for overall scoring)

---

## Questions

### What is a lock statement in C#?
Ensures that one thread does not enter a critical section of code while another thread is in the critical section.

### What is the use of Monitor in C#?
Provides a mechanism that synchronizes access to objects. Controls access by granting a lock for an object to a single thread.

### How to create a critical section with lock()
Use lock statement to ensure thread-safe access to shared resources.

### How many processes can listen on a single TCP/IP port?
Only one process can listen on a specific port at a time (per IP address).
