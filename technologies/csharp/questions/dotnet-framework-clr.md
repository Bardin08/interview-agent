# .NET Framework & CLR
<!-- File: interview-agent/technologies/csharp/questions/dotnet-framework-clr.md -->

## Topic Overview
.NET runtime, CLR, assemblies, reflection, app domains, and framework internals.

**Weight**: 1.0

---

## Questions

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
