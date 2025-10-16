# .NET & C# Interview Questions - Clustered by Topic
<!-- File: interview-agent/technologies/csharp/questions.md -->

## 📚 Table of Contents
- [C# Language Fundamentals](#c-language-fundamentals)
- [Object-Oriented Programming (OOP)](#object-oriented-programming-oop)
- [Memory Management & Performance](#memory-management--performance)
- [Collections & Data Structures](#collections--data-structures)
- [Threading & Concurrency](#threading--concurrency)
- [.NET Framework & CLR](#net-framework--clr)
- [ASP.NET & Web Development](#aspnet--web-development)
- [ASP.NET Core](#aspnet-core)
- [Data Access](#data-access)
- [XML & Configuration](#xml--configuration)
- [Advanced Topics](#advanced-topics)
- [Coding Exercises](#coding-exercises)

---

## C# Language Fundamentals

### What is C# and how does it differ from C?
- C# is object-oriented
- Supports automatic garbage collection
- Requires .NET framework
- More type-safe compared to C

### Strong-typing vs Weak-typing
Understanding type safety and type systems in programming languages.

### What does the "readonly" keyword mean?
Fields that can only be assigned during declaration or in constructor.

### What does the "volatile" keyword mean?
Indicates that a field might be modified by multiple threads concurrently.

### Explain "ref" and "out" parameters
- **ref**: Passes argument by reference, must be initialized before passing
- **out**: Passes argument by reference, must be assigned within the method

### Difference between override vs new
- **override**: Overrides base class virtual method
- **new**: Hides base class method

### Explain virtual, sealed, override, and abstract keywords
- **virtual**: Allows method to be overridden
- **sealed**: Prevents inheritance or overriding
- **override**: Provides new implementation of virtual method
- **abstract**: Defines method signature without implementation

### What are short-circuited operators?
Logical operators (&& and ||) that stop evaluation once result is determined.

### Access Modifiers
- **public**: Accessible from anywhere
- **protected**: Accessible within class and derived classes
- **private**: Accessible only within the class
- **internal**: Accessible within same assembly

### Difference between typeof(foo) and myFoo.GetType()
- **typeof()**: Compile-time type evaluation
- **GetType()**: Runtime type evaluation

---

## Object-Oriented Programming (OOP)

### What is Inheritance?
Inheritance represents the relationship between two classes where one type derives functionality from a second type and extends it by adding new methods, properties, events, fields, and constants.

### Does C# support multiple inheritance?
- C# doesn't support multiple inheritance of classes
- Can use interfaces to inherit properties from multiple sources
- Supports single inheritance

### What's the difference between an abstract class and interface?
Key differences in implementation, multiple inheritance support, and use cases.

### Interface-oriented vs Object-oriented vs Aspect-oriented programming
Different programming paradigms and their applications.

### What are Events and Delegates?
- **Event**: A message sent by a control to notify the occurrence of an action
- **Delegate**: A type-safe function pointer that acts as an intermediary between sender and receiver objects
- Delegates allow passing methods of one class to objects of other classes

### What are Extension Methods?
- Add new methods to existing classes
- Static methods
- Can extend functionality without modifying original class

### What is Reflection?
The ability to find information about types contained in an assembly at runtime. Allows inspecting objects and application details at run-time.

### Use of Reflection
- Detect class attributes
- Inspect metadata
- Dynamically invoke methods
- Load assemblies at runtime

### What are Partial Classes?
Classes split across multiple files, allowing separation of auto-generated and custom code.

---

## Memory Management & Performance

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

---

## Collections & Data Structures

### What is an Array?
A collection of related instances (either value or reference types). C# supports single, multi-dimensional, and jagged arrays.

### Array vs ArrayList
- **Arrays**: Fixed size, type-safe, System.Array namespace
- **ArrayList**: Dynamic size, can contain mixed data types, System.Collections namespace

### What are Generics?
- Allow type-safe code reuse
- Defined inside angular brackets <>
- Reduce boxing/unboxing overhead
- Enable creating type-safe collections

### String vs StringBuilder
- **String**: Immutable, creates new object on modification
- **StringBuilder**: Mutable, efficient for multiple string manipulations

### Properties and Indexers
Enable controlled access to class members and collection-like access patterns.

---

## Threading & Concurrency

### What is a lock statement in C#?
Ensures that one thread does not enter a critical section of code while another thread is in the critical section.

### What is the use of Monitor in C#?
Provides a mechanism that synchronizes access to objects. Controls access by granting a lock for an object to a single thread.

### How to create a critical section with lock()
Use lock statement to ensure thread-safe access to shared resources.

### How many processes can listen on a single TCP/IP port?
Only one process can listen on a specific port at a time (per IP address).

---

## .NET Framework & CLR

### Why .NET Framework?
Benefits include:
- No COM specifications
- Language integration
- Base Class Library wrapper over API calls
- Common Runtime Engine
- Single framework for Windows/Web apps

### What is BCL (Base Class Library)?
Encapsulates a large number of common functionalities available to all .NET languages, including I/O operations, data access, and hardware interfaces.

### What is CLR (Common Language Runtime)?
CLR is responsible for:
- Converting code to Common Intermediate Language (CIL)
- Memory Management
- Application Execution
- Thread Management
- Security checks
- Loading assemblies

### What is the GAC (Global Assembly Cache)?
Central repository for storing .NET assemblies shared across multiple applications.

### Difference between EXE and DLL
- **EXE**: Executable file, entry point, runs in own process
- **DLL**: Dynamic Link Library, no entry point, loaded by other programs

### What are PDBs (Program Database Files)?
Symbol files containing debugging information for assemblies.

### Understanding assembly version strings
Format: Major.Minor.Build.Revision - controls versioning and binding policies.

### Assembly loading methods
- **Static loading**: Assembly referenced at compile time
- **Dynamic loading**: Assembly loaded at runtime using reflection

### What is FullTrust?
Code access security permission set granting unrestricted access to all resources.

### Early-binding vs Late-binding
- **Early-binding**: Type checking at compile time, better performance
- **Late-binding**: Type checking at runtime, more flexible

### Difference between XML Web Services and .NET Remoting
Different distributed computing technologies in .NET Framework.

---

## ASP.NET & Web Development

### State Management in ASP.NET
**Two types:** Client-side and Server-side

**Client-side includes:**
- View State
- Control State
- Hidden Fields
- Cookies
- Query Strings

**Server-side includes:**
- Application State
- Cache Object
- Session State

### What are Cookies?
- Small data files created by server on client browser
- Two types: Session cookies (temporary) and Persistent cookies (long-lasting)
- Can store string values
- **Disadvantages**: Browser-dependent, not secure, limited data storage

### Session Object
- Stores user-specific information on server memory
- **Advantages**: Stores user state, easy to implement, secure
- **Disadvantages**: Performance overhead, serialization complexity

### What is ViewState?
Client-side state management storing page and control values between postbacks.

### What is a PostBack?
Process of submitting an ASP.NET page back to the server for processing.

### How does a browser form POST become a server-side event?
ASP.NET event model translates HTTP POST into server-side event handlers.

### HTTP Verbs: GET and POST
- **GET**: Retrieve data, parameters in URL, idempotent
- **POST**: Submit data, parameters in body, not idempotent

### HTTP Status Codes
- 2xx: Success
- 3xx: Redirection
- 4xx: Client errors
- 5xx: Server errors

### Master Pages
- Template for consistent page layout across website
- Uses ContentPlaceHolder control to define customizable regions
- Changes in master page reflect across all content pages

### Navigation Methods
- Client-side navigation
- Cross-page posting
- Client-side browser redirect
- Server-side transfer

### Authentication Types
- Windows Authentication
- Forms Authentication
- Passport Authentication

### Validation Controls
- RequiredFieldValidator
- CompareValidator
- RangeValidator
- RegularExpressionValidator
- CustomValidator
- ValidationSummary

### How does output caching work?
Stores rendered page output for reuse, improving performance.

---

## ASP.NET Core

### What is .NET Core?
A newer version of .NET, which is cross-platform, supporting Windows, MacOS and Linux, and can be used in device, cloud, and embedded/IoT scenarios.

### What is ASP.NET Core?
An open source and cross-platform framework suitable for building cloud-based internet-connected applications like web apps, IoT apps, and mobile apps.

### Why Use ASP.NET Core?
Key benefits include:
- Faster than traditional ASP.NET
- Cross-platform support
- Flexible deployment
- Built-in dependency injection
- Cloud-ready architecture
- Support for JavaScript frameworks
- Unified development models
- Built-in logging support
- Middleware for request processing

### What is Kestrel?
A cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.

### What is a Host in ASP.NET Core?
Responsible for application startup and lifetime management. Ensures the application's services and server are available and properly configured.

### What is Razor Pages?
A new feature introduced in ASP.NET Core 2.0, consisting of simple pages or views without controllers, focused on page-specific scenarios with minimal logic.

### What's new in ASP.NET Core 6.0?
- Removed Startup.cs by default
- Introduced Minimal API
- Uses C# 10 features like top-level statements
- Simplified API development

---

## Data Access

### Difference between DataTable and DataReader
- **DataTable**: In-memory representation, disconnected, supports random access
- **DataReader**: Forward-only, read-only, connected, better performance for large datasets

### How to loop through all rows of a DataTable?

**ForEach loop:**
```csharp
foreach (DataRow row in dTable.Rows)
{
    yourvariable = row["ColumnName"].ToString();
}
```

**For loop:**
```csharp
for (int j = 0; j < dTable.Rows.Count; j++)
{
    yourvariable = dTable.Rows[j]["ColumnName"].ToString();
}
```

---

## XML & Configuration

### Purpose of XML Namespaces
Avoid naming conflicts and organize XML elements.

### When to use DOM (Document Object Model)
When need to navigate, modify, or perform multiple operations on XML document.

### Difference between Well-Formed and Valid XML
- **Well-Formed**: Follows XML syntax rules
- **Valid**: Follows XML syntax AND conforms to a schema (DTD/XSD)

### XML validation in .NET
Using XmlReader, XmlDocument with schemas, or LINQ to XML.

### Difference between XPathDocument and XmlDocument
- **XPathDocument**: Read-only, optimized for XPath queries
- **XmlDocument**: Read/write, DOM-based manipulation

### Load and select XML nodes
Using XmlDocument, XDocument, or XPath expressions.

### Write a regex to remove HTML tags
Pattern matching to strip HTML markup from strings.

---

## Advanced Topics

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
