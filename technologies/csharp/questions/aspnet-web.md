# ASP.NET & Web Development
<!-- File: interview-agent/technologies/csharp/questions/aspnet-web.md -->

## Topic Overview
ASP.NET Framework (Web Forms, MVC, Web API), IIS, and HTTP fundamentals.

**Weight**: 0.9

---

## Questions

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
