# Interview Agent 🎯
<!-- File: interview-agent/README.md -->

An AI-powered multi-technology senior technical interviewer that helps candidates identify knowledge gaps and build personalized improvement plans.

## What It Does

This agent conducts structured technical interviews to:
- **Assess** your knowledge across multiple technologies (C#, Python, JavaScript, etc.)
- **Identify** specific weak spots and knowledge gaps
- **Adapt** difficulty based on your responses
- **Guide** you with progressive hints when stuck
- **Generate** comprehensive feedback reports with personalized study plans

## Key Features

- 🔧 **Multi-Technology** - C#, Python, JavaScript, Java, Go, and more
- 🌍 **Multilingual** - Automatically detects and speaks your language
- 🎚️ **Adaptive** - Adjusts difficulty from fresher to architect level
- 💡 **Supportive** - 5-level progressive hint system
- 📊 **Comprehensive** - Detailed reports with study plans and resources
- 🎯 **Focused** - Identifies patterns in your knowledge gaps
- 🚀 **Actionable** - Week-by-week study plans with hands-on projects

## Quick Start

```bash
# List available technologies
*technologies

# Start interview (technology optional, defaults to csharp)
*begin mid-level              # C# interview at mid-level
*begin senior python          # Python interview at senior level
*begin junior javascript      # JavaScript interview at junior level

# During interview:
*hint            # Get a hint for current question
*skip            # Skip current question
*topics          # Show topics for current technology
*analyze         # See real-time performance
*pause           # Pause and save progress

# After interview:
*report          # Generate comprehensive feedback report
```

## Supported Technologies

### Currently Available
- **#️⃣ C# & .NET** - Language fundamentals, ASP.NET Core, Entity Framework
  - Topics: OOP, Memory Management, Threading, Web Development, Data Access

### Coming Soon
- **🐍 Python** - Django, Flask, FastAPI, Data Science
- **🟨 JavaScript/TypeScript** - React, Node.js, Angular, Vue
- **☕ Java** - Spring Boot, Microservices, Enterprise patterns
- **🔷 Go** - Cloud-native, Concurrency, Backend development

## Experience Levels

- **Fresher** (0-1 years) - 10-12 questions, fundamental topics
- **Junior** (1-2 years) - 12-15 questions, core concepts
- **Mid-Level** (2-5 years) - 15-18 questions, advanced topics
- **Senior** (5+ years) - 18-22 questions, architecture & patterns
- **Architect** (7+ years) - 20-25 questions, system design & best practices

## What You Get

After completing the interview, you receive:

✅ **Detailed Performance Analysis** - Score breakdown by topic
✅ **Question-by-Question Review** - Every question with correct answers
✅ **Personalized Study Plan** - Week-by-week learning roadmap
✅ **Technology-Specific Resources** - Books, courses, tutorials for your gaps
✅ **Hands-On Projects** - Real-world practice exercises
✅ **Progress Tracking** - Checklists and milestones

## Architecture

The agent uses a **dynamic technology loading system**:

```
interview-agent/
├── agent.yaml                 # Main configuration + technology registry
├── technologies/
│   ├── csharp/
│   │   ├── config.yaml       # C# metadata, topics, resources
│   │   └── questions.md      # C# interview questions
│   ├── python/               # (Coming soon)
│   ├── javascript/           # (Coming soon)
│   └── ...
├── tasks/                     # Technology-agnostic workflows
│   ├── conduct-interview.md
│   ├── generate-interview-report.md
│   └── analyze-performance.md
└── templates/                 # Reusable templates
    ├── interview-session-tmpl.yaml
    └── interview-report-tmpl.md
```

## Adding New Technologies

To add a new technology:

1. Create `technologies/{tech-id}/` directory
2. Add `config.yaml` with technology metadata, topics, and resources
3. Add `questions.md` with technology-specific interview questions
4. Register in `agent.yaml` technology registry

See `technologies/csharp/` as a reference implementation.

## Technology Configuration

Each technology has its own:
- **Topics** - Organized question clusters
- **Frameworks** - Specific versions and tools
- **Resources** - Official docs, books, courses, practice platforms
- **Common Pitfalls** - Frequent mistakes to watch for
- **Project Ideas** - Hands-on practice suggestions

## Integration

This agent can be integrated into:
- LLM-based assistants (Claude, GPT, etc.)
- CLI applications
- Web interfaces
- Chat platforms

## Contributing

Want to add a new technology? See the contribution guide:
1. Fork the repository
2. Create technology folder with config.yaml and questions.md
3. Follow the format in `technologies/csharp/`
4. Submit a pull request

## Version History

- **v2.0.0** - Multi-technology support with dynamic loading
- **v1.0.0** - Initial C#/.NET interview agent

## License

Created by Vladyslav Bardin as part of BMAD-inspired agent framework.
