# Advanced Topics
<!-- File: interview-agent/technologies/csharp/questions/advanced-topics.md -->

## Topic Overview
Advanced C# features including LINQ, delegates, events, generics, reflection, and metaprogramming.

**Weight**: 1.0

---

## Questions

### What is a static constructor?
Used to initialize static data members as soon as the class is referenced first time. A static constructor does not take access modifiers or have parameters.

### What is a Windows Service?
Background application that runs without user interface, typically starts with OS.

### Difference between static and non-static methods
- **Static methods**: Belong to class, called without instance
- **Non-static methods**: Belong to instance, require object

### Method Overloading
Multiple methods with same name but different parameters.

### Can DateTimes be null?
DateTime is a value type and cannot be null. Use Nullable<DateTime> or DateTime? for nullable dates.

### Issues with DateTime.Parse(myString)
- Culture-specific parsing
- Can throw exceptions
- Ambiguous date formats
- Prefer DateTime.TryParse() or DateTime.ParseExact()

### What is cyclomatic complexity?
Metric measuring the number of independent paths through code, indicating complexity.

### Contrast OOP and SOA (Service-Oriented Architecture)
Different architectural approaches to software design.

### Why is catch(Exception) almost always bad?
- Too broad, catches everything including system exceptions
- Hides bugs
- Makes debugging difficult
- Better to catch specific exceptions

### Create a custom event handler
Implementing custom events using delegates and event keyword.

### Write a function accepting another function as parameter
Using delegates, Func<>, Action<>, or lambda expressions.

---

## Coding Exercises

### Write a linked list class from scratch
Implement Node class and LinkedList with add, remove, find operations.

### Create a hashtable class without built-in classes
Implement hash function, collision handling, and key-value storage.

### Implement a binary tree class
Node structure with left/right children, insertion, traversal methods.

### Write a binary search method
Efficient search algorithm for sorted arrays with O(log n) complexity.

### Prime number detection
```csharp
bool IsPrime(int n)
{
    if (n <= 1) return false;
    for (int i = 2; i * i <= n; i++)
    {
        if (n % i == 0) return false;
    }
    return true;
}
```

### Palindrome checking
Check if string reads same forwards and backwards.

### String reversal techniques
Multiple approaches: array reversal, StringBuilder, LINQ.

### Substring extraction
Extract portions of strings based on position or patterns.

### Design a blog database schema
Tables for users, posts, comments, categories, tags with relationships.

---

## Interview Preparation Tips

### By Experience Level

**Freshers:**
- Focus on language fundamentals
- Understand basic OOP concepts
- Practice simple coding problems
- Know collections and basic data structures

**Mid-Level Developers:**
- Deep understanding of .NET Framework/Core
- Threading and concurrency
- Design patterns
- Performance optimization
- Database and data access

**Senior Developers/Architects:**
- Architectural patterns (SOA, Microservices)
- Security best practices
- Scalability and performance at scale
- Code quality metrics
- Advanced debugging techniques

### Study Resources
- Official Microsoft documentation
- Practice coding problems on platforms like LeetCode, HackerRank
- Build real projects
- Review open-source .NET projects
- Stay updated with latest .NET releases
