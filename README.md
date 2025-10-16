# Interview Agent 🎯
<!-- File: interview-agent/README.md -->

An AI-powered multi-technology senior technical interviewer that helps candidates identify knowledge gaps and build personalized improvement plans.

🚀 **[Try Alex the Interviewer on ChatGPT](https://chatgpt.com/g/g-68f14f92f4208191ac335aba8b4baadf-alex-the-interviewer)** - Pre-configured Custom GPT ready to use!

## What It Does

This agent conducts structured technical interviews to:
- **Assess** your knowledge across multiple technologies (C#, Python, JavaScript, etc.)
- **Identify** specific weak spots and knowledge gaps
- **Adapt** difficulty based on your responses
- **Guide** you with progressive hints when stuck
- **Generate** comprehensive feedback reports with personalized study plans

## Key Features

- 🔧 **Multi-Technology** - C#, React, Angular, and more (extensible)
- 🌍 **Multilingual** - Choose your preferred interview language upfront
- 🎚️ **Adaptive** - Adjusts difficulty from fresher to architect level
- 💡 **Supportive** - 5-level progressive hint system
- 📊 **Comprehensive** - Detailed reports with study plans and resources
- 🎯 **Focused** - Identifies patterns in your knowledge gaps
- 🚀 **Actionable** - Week-by-week study plans with hands-on projects
- 🔌 **Dynamic** - Technologies loaded from GitHub via OpenAPI

## Quick Start

### Option 1: Use Pre-configured Custom GPT
🚀 **[Try Alex the Interviewer](https://chatgpt.com/g/g-68f14f92f4208191ac335aba8b4baadf-alex-the-interviewer)** - Ready to use on ChatGPT!

### Option 2: Use with Your Own Agent

**First Time Setup:**
1. Agent will ask: "What language would you like to conduct this interview in?"
2. Choose your preferred language (English, Ukrainian, Spanish, etc.)
3. All communication will be in your chosen language

**Available Commands:**
```bash
# List available technologies
*technologies

# Start interview (both level and technology are REQUIRED)
*begin mid-level csharp       # C# interview at mid-level
*begin senior csharp          # C# interview at senior level
*begin junior frontend-react  # React interview at junior level

# If you forget the technology, agent will show the list automatically

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
- **#️⃣ C# & .NET** - C# language fundamentals, .NET Framework/Core, ASP.NET Core, Entity Framework
  - 200+ questions across 10 topics
  - Topics: OOP, Memory Management, Threading, Collections, Web Development, Data Access, Advanced Patterns

### Coming Soon
- **🟦 Frontend/React** - JavaScript/TypeScript, React, Node.js
- **🅰️ Frontend/Angular** - JavaScript/TypeScript, Angular

Want to add your favorite technology? See [CONTRIBUTING.md](CONTRIBUTING.md)!

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

Want to add Python, Java, Go, or another technology? We'd love your contribution!

See [CONTRIBUTING.md](CONTRIBUTING.md) for a detailed guide on:
- Creating technology configurations
- Writing quality interview questions
- Adding learning resources
- Submitting your contribution

Reference implementation: `technologies/csharp/`

## Technology Configuration

Each technology has its own:
- **Topics** - Organized question clusters
- **Frameworks** - Specific versions and tools
- **Resources** - Official docs, books, courses, practice platforms
- **Common Pitfalls** - Frequent mistakes to watch for
- **Project Ideas** - Hands-on practice suggestions

## Integration

This agent can be integrated into:
- **ChatGPT Custom GPT** - [Alex the Interviewer](https://chatgpt.com/g/g-68f14f92f4208191ac335aba8b4baadf-alex-the-interviewer)
- LLM-based assistants (Claude, GPT, etc.)
- CLI applications
- Web interfaces
- Chat platforms

The OpenAPI schema (`openapi-schema.yaml`) enables dynamic content loading from GitHub.

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

Quick overview:
1. Fork the repository
2. Create technology folder with `config.yaml` and `questions.md`
3. Follow the format in `technologies/csharp/`
4. Update `technologies.json`
5. Submit a pull request

All contributors are recognized in the project!

## Privacy

This project does not collect any personal data. See [PRIVACY.md](PRIVACY.md) for details.

## Version History

- **v2.0.0** - Multi-technology support with dynamic loading, Custom GPT integration
- **v1.0.0** - Initial C#/.NET interview agent

## License

MIT License - see [LICENSE](LICENSE) for details.

Created by [Vladyslav Bardin](https://github.com/bardin08)
