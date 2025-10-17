# Contributing to Interview Agent

Thank you for your interest in contributing to Interview Agent! This guide will help you add new technologies, improve existing content, or enhance the agent's capabilities.

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Adding a New Technology](#adding-a-new-technology)
- [Improving Existing Technologies](#improving-existing-technologies)
- [Contribution Workflow](#contribution-workflow)
- [Content Standards](#content-standards)
- [Testing Your Changes](#testing-your-changes)

## Ways to Contribute

- ✅ Add a new technology (Python, JavaScript, Java, etc.)
- ✅ Add more questions to existing technologies
- ✅ Improve technology configurations and resources
- ✅ Fix typos or improve documentation
- ✅ Suggest new features or improvements
- ✅ Report bugs or issues

## Adding a New Technology

### 1. Check Available Technologies

First, check `technologies.json` to see if your technology is already listed as "coming_soon".

### 2. Create Technology Directory Structure

```bash
technologies/
└── {tech-id}/
    ├── config.yaml       # Technology configuration
    └── questions.md      # Interview questions
```

**Technology ID naming convention:**
- Use lowercase
- Use hyphens for multi-word names
- Examples: `csharp`, `python`, `frontend-react`, `backend-java`

### 3. Create `config.yaml`

Use `technologies/csharp/config.yaml` as a template. Your config should include:

```yaml
technology:
  id: your-tech-id
  name: "Technology Display Name"
  icon: "🔷"  # Pick an appropriate emoji
  description: Brief technology description

topics:
  - Topic Category 1
  - Topic Category 2
  # 8-12 topics recommended

frameworks:
  - name: Framework Name
    description: Brief description
    versions: [version1, version2]

resources:
  official_docs:
    - name: Resource Name
      url: https://example.com
      description: Why this resource is valuable

  books:
    - title: Book Title
      author: Author Name
      level: beginner|intermediate|advanced
      url: https://example.com

  courses:
    - name: Course Name
      platform: Platform Name
      url: https://example.com
      level: beginner|intermediate|advanced

  practice:
    - name: Practice Platform
      url: https://example.com
      description: What to practice

common_pitfalls:
  - pitfall: Common mistake
    solution: How to avoid it

project_ideas:
  - name: Project Name
    description: What to build
    topics_covered: [Topic 1, Topic 2]
    difficulty: beginner|intermediate|advanced

experience_levels:
  fresher:
    years: 0-1
    question_count: 10-12
    focus_topics: [Topic 1, Topic 2]

  junior:
    years: 1-2
    question_count: 12-15
    focus_topics: [Topic 1, Topic 2, Topic 3]

  mid-level:
    years: 2-5
    question_count: 15-18
    focus_topics: [Topic 3, Topic 4, Topic 5]

  senior:
    years: 5+
    question_count: 18-22
    focus_topics: [Topic 5, Topic 6, Advanced Topics]

  architect:
    years: 7+
    question_count: 20-25
    focus_topics: [System Design, Best Practices, Architecture]
```

### 4. Create `questions.md`

Organize questions by topics defined in your config:

```markdown
# {Technology Name} Interview Questions

## Topic Category 1

### Question Title?

**Difficulty:** Beginner|Intermediate|Advanced
**Experience Level:** Fresher|Junior|Mid-Level|Senior|Architect

**Key Points to Cover:**
- Important concept 1
- Important concept 2
- Important concept 3

**Expected Answer:**
Detailed explanation of what a good answer should include...

**Common Mistakes:**
- Mistake candidates often make
- Another common mistake

**Follow-up Questions:**
- Related question 1?
- Related question 2?

---

### Next Question?

[Repeat format...]

## Topic Category 2

[More questions...]
```

**Question Guidelines:**
- Aim for 150-250 questions total
- Distribute across all experience levels
- Include a mix of theoretical and practical questions
- Add real-world scenarios and code examples where applicable
- Mark difficulty and target experience level clearly

### 5. Update `technologies.json`

Add your technology to the registry:

```json
{
  "id": "your-tech-id",
  "name": "Technology Name",
  "icon": "🔷",
  "status": "active",
  "description": "Brief technology description",
  "topics": [
    "Topic 1",
    "Topic 2"
  ],
  "experience_levels": [
    "fresher",
    "junior",
    "mid-level",
    "senior",
    "architect"
  ],
  "question_count": 200
}
```

Update metadata:
```json
"metadata": {
  "last_updated": "2025-10-17",
  "total_technologies": 6,
  "active_technologies": 2,
  "total_questions": 400
}
```

### 6. Update OpenAPI Schema (Optional)

If your technology ID differs from standard patterns, add it to the enum in `openapi-schema.yaml`:

```yaml
schema:
  type: string
  enum: [csharp, python, javascript, your-tech-id]
```

## Improving Existing Technologies

### Adding Questions

1. Follow the existing question format
2. Ensure questions align with the topic they're under
3. Set appropriate difficulty and experience levels
4. Update question count in `technologies.json`

### Improving Resources

1. Add valuable learning resources to `config.yaml`
2. Include official documentation, practical courses, or hands-on platforms
3. Provide brief descriptions of why each resource is valuable

### Updating Configuration

1. Keep topics focused and well-organized (8-12 topics ideal)
2. Update framework versions as needed
3. Add relevant project ideas

## Contribution Workflow

### 1. Fork the Repository

```bash
git clone https://github.com/bardin08/interview-agent.git
cd interview-agent
```

### 2. Create a Feature Branch

```bash
git checkout -b add-python-technology
# or
git checkout -b improve-csharp-questions
```

### 3. Make Your Changes

- Follow the standards outlined in this guide
- Use existing technologies as references
- Keep formatting consistent

### 4. Test Your Changes

See [Testing Your Changes](#testing-your-changes) section below.

### 5. Commit Your Changes

```bash
git add .
git commit -m "feat: add Python technology support"
# or
git commit -m "feat: add 50 advanced C# questions"
# or
git commit -m "docs: improve contributing guidelines"
```

**Commit message format:**
- `feat:` - New feature or technology
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `refactor:` - Code refactoring
- `test:` - Testing improvements

### 6. Push and Create Pull Request

```bash
git push origin add-python-technology
```

Then create a pull request on GitHub with:
- Clear title describing your contribution
- Description of what you added/changed
- Any testing you performed

## Content Standards

### Quality Guidelines

✅ **DO:**
- Write clear, concise questions
- Provide comprehensive expected answers
- Include practical, real-world scenarios
- Cite authoritative sources for resources
- Keep formatting consistent
- Use proper grammar and spelling

❌ **DON'T:**
- Copy questions from other sources without attribution
- Add overly trivial or "gotcha" questions
- Include outdated framework versions
- Use offensive or inappropriate content
- Add broken or spam resource links

### YAML Formatting

- Use 2 spaces for indentation
- Keep line length reasonable (< 120 characters)
- Use consistent key ordering
- Add comments for complex sections

### Markdown Formatting

- Use ATX-style headers (`#`, `##`, `###`)
- Include blank lines between sections
- Use code blocks with language specification
- Keep bullet lists consistent

## Testing Your Changes

### 1. Validate YAML Files

```bash
# If you have Python/PyYAML installed
python3 -c "import yaml; yaml.safe_load(open('technologies/your-tech/config.yaml'))"

# Or use online YAML validators
```

### 2. Validate JSON Files

```bash
# Use jq if available
jq empty technologies.json

# Or use online JSON validators
```

### 3. Check OpenAPI Schema

Use the ChatGPT Custom GPT Actions editor to validate the schema:
1. Copy `openapi-schema.yaml` content
2. Paste into ChatGPT Actions schema editor
3. Click "Format" to check for errors

### 4. Test with Custom GPT

1. Update your fork on GitHub
2. Update the server URL in `openapi-schema.yaml` to point to your fork
3. Configure a test Custom GPT with your schema
4. Test the interview flow with your new technology

### 5. Verify Links

- Check that all resource URLs are accessible
- Ensure documentation links are current
- Verify course/book links are valid

## Review Process

Once you submit a pull request:

1. **Automated Checks** - Basic validation runs automatically
2. **Content Review** - Maintainers review quality and accuracy
3. **Feedback** - You may receive requests for changes
4. **Approval** - Once approved, your contribution will be merged!

## Questions or Issues?

- **Questions:** Open a [GitHub Discussion](https://github.com/bardin08/interview-agent/discussions)
- **Bugs:** Open a [GitHub Issue](https://github.com/bardin08/interview-agent/issues)
- **Ideas:** Open a [Feature Request](https://github.com/bardin08/interview-agent/issues/new)

## Recognition

All contributors will be recognized in the repository. Thank you for helping make Interview Agent better!

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
