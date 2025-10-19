# Contributing to Interview Agent

Thank you for your interest in contributing! This guide will help you add new technologies, improve existing content, or enhance the agent's capabilities.

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Project Structure](#project-structure)
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
- ✅ Report bugs or suggest features

## Project Structure

```
interview-agent/
├── agent.yaml                          # Main agent configuration
├── technologies/
│   ├── index.yaml                      # Technology architecture metadata
│   ├── supported-technologies.yaml     # Technology registry
│   └── {tech-id}/
│       ├── config.yaml                 # Technology metadata & resources
│       ├── competency-matrix.yaml      # Skills assessment framework
│       └── questions/
│           ├── index.yaml              # Topic index with weights
│           └── {topic-id}.md           # Questions per topic
├── tasks/                              # Interview workflows
│   ├── conduct-interview.md
│   ├── generate-interview-report.md
│   └── analyze-performance.md
├── templates/                          # Report & session templates
├── config/                             # Framework configurations
└── openapi-schema.yaml                 # API schema for integrations
```

### Key Architecture Features

**Sharded Question Bank** - Questions are split by topic to reduce context usage by 70-80%:
- `questions/index.yaml` - Topic list with metadata
- `questions/{topic-id}.md` - Individual topic files
- Topics loaded on-demand during interviews

**Technology Registry** - All technologies listed in `technologies/supported-technologies.yaml` with:
- ID, name, icon, status (active/coming_soon)
- Topic list and question count
- Experience levels supported

## Adding a New Technology

### Step 1: Create Directory Structure

```bash
technologies/
└── {tech-id}/
    ├── config.yaml
    ├── competency-matrix.yaml
    └── questions/
        ├── index.yaml
        └── {topic-id}.md  (one per topic)
```

**Technology ID naming convention:**
- Use lowercase
- Use hyphens for multi-word names
- Examples: `csharp`, `python`, `frontend-react`, `backend-java`

### Step 2: Create `config.yaml`

Use `technologies/csharp/config.yaml` as reference:

```yaml
technology:
  id: your-tech-id
  name: "Technology Display Name"
  icon: "🔷"
  version: 1.0.0

  description: |
    Brief technology description and scope

  topics:
    - Topic Name 1
    - Topic Name 2
    # 8-12 topics recommended

  frameworks:
    - name: Framework Name
      versions: [version1, version2]

  key_concepts:
    category1:
      - Concept 1
      - Concept 2

  # Path to competency matrix file
  competency_matrix_path: technologies/your-tech-id/competency-matrix.yaml
  competency_matrix_description: |
    Competency matrix defining expectations for each experience level.
    Includes must_know, good_to_know, evaluation criteria, and scoring.

  # Path to question bank
  question_bank_path: technologies/your-tech-id/questions/
  question_bank_structure: sharded
  question_bank_description: |
    Topic-based sharded question repository for efficient context usage.
    Each topic is stored in a separate markdown file and loaded on-demand.
    Start by loading questions/index.yaml, then load individual topic files as needed.

  # Resources section
  resources:
    official_docs:
      - name: Documentation Name
        url: https://example.com
        focus: What it covers

    books:
      - title: Book Title
        author: Author Name
        level: [beginner, intermediate, advanced]
        focus: Key topics covered

    online_courses:
      - platform: Platform Name
        courses:
          - Course Name 1
          - Course Name 2

    practice_platforms:
      - name: Platform Name
        url: https://example.com
        focus: What to practice

    communities:
      - name: Community Name
        url: https://example.com
        type: Q&A|Community|Chat|Official

  # Common mistakes and solutions
  common_pitfalls:
    - topic: Topic Name
      issue: What the common mistake is
      impact: Why it matters

  # Interview preparation tips
  interview_tips:
    preparation:
      - Tip 1
      - Tip 2

    during_interview:
      - Tip 1
      - Tip 2

    common_questions_to_prepare:
      - Question topic 1
      - Question topic 2

  # Project suggestions by difficulty
  project_ideas:
    beginner:
      - Project idea 1
      - Project idea 2

    intermediate:
      - Project idea 1
      - Project idea 2

    advanced:
      - Project idea 1
      - Project idea 2

# Metadata section
metadata:
  last_updated: 2025-10-19
  version: 1.0.0
  question_count: 150+
  question_structure: topic-based sharded (10 topics)
  topics_count: 10
  maintainer: Your Name or Team
  contribution_guide: See CONTRIBUTING.md for adding new questions
```

### Step 3: Create `competency-matrix.yaml`

Define skill progression across experience levels. See `technologies/csharp/competency-matrix.yaml` for reference.

### Step 4: Create `questions/index.yaml`

```yaml
metadata:
  technology: Technology Name
  technology_id: your-tech-id
  version: 1.0.0
  question_format: markdown
  total_topics: 10
  last_updated: 2025-10-19

topics:
  - id: topic-id
    name: Topic Display Name
    file: topic-id.md
    description: Topic scope
    estimated_questions: 15
    weight: 1.2  # Importance multiplier (0.8-1.5)
```

**Weight Guidelines:**
- `1.3-1.5` - Critical topics (fundamental concepts, core skills)
- `1.0-1.2` - Important topics (commonly used features)
- `0.8-0.9` - Supplementary topics (less common but useful)

### Step 5: Create Question Files

Create `questions/{topic-id}.md` for each topic:

```markdown
# Topic Name
<!-- File: interview-agent/technologies/{tech-id}/questions/{topic-id}.md -->

## Topic Overview
Brief description of topic scope.

**Weight**: 1.2 (Importance level)

---

## Questions

### Question Title?
Concise answer covering key points.

### More Complex Question?
**Key Points:**
- Point 1
- Point 2

**Common Mistakes:**
- Mistake to avoid

**When to Use:**
- Use case scenario

---
```

**Question Guidelines:**
- Keep answers concise but complete
- Focus on practical knowledge
- Include common mistakes where relevant
- Use bullet points for clarity
- 10-20 questions per topic file
- Mix difficulty levels within topics

### Step 6: Update Technology Registry

Add your technology to `technologies/supported-technologies.yaml`:

```yaml
technologies:
  - id: your-tech-id
    name: "Technology Name"
    icon: "🔷"
    status: active
    description: Brief description
    topics:
      - Topic 1
      - Topic 2
    experience_levels:
      - fresher
      - junior
      - mid-level
      - senior
      - architect
    question_count: 150
```

Update metadata:
```yaml
metadata:
  last_updated: "2025-10-19"
  total_technologies: 4  # Increment
  active_technologies: 2  # Increment if active
  total_questions: 350    # Add your question count
```

## Improving Existing Technologies

### Adding Questions

1. Identify the appropriate topic file in `questions/`
2. Follow existing format and style
3. Keep answers concise and practical
4. Update `estimated_questions` in `questions/index.yaml`
5. Update `question_count` in `supported-technologies.yaml`

### Improving Resources

1. Add valuable resources to `config.yaml`
2. Include official docs, quality courses, practice platforms
3. Provide brief descriptions of value
4. Keep URLs current and accessible

### Updating Competency Matrix

1. Edit `competency-matrix.yaml`
2. Ensure progression across experience levels makes sense
3. Align with current industry standards

## Contribution Workflow

### 1. Fork & Clone

```bash
git clone https://github.com/YOUR-USERNAME/interview-agent.git
cd interview-agent
```

### 2. Create Feature Branch

```bash
git checkout -b add-python-technology
# or
git checkout -b improve-csharp-questions
```

### 3. Make Changes

- Follow structure outlined above
- Use existing technologies as reference (see `technologies/csharp/`)
- Keep formatting consistent

### 4. Test Your Changes

See [Testing Your Changes](#testing-your-changes) below.

### 5. Commit

```bash
git add .
git commit -m "feat: add Python technology support"
# or
git commit -m "feat: add 30 advanced C# OOP questions"
# or
git commit -m "docs: update contributing guide"
```

**Commit Prefixes:**
- `feat:` - New feature or technology
- `fix:` - Bug fix
- `docs:` - Documentation only
- `refactor:` - Code refactoring
- `test:` - Testing improvements

### 6. Push & Create PR

```bash
git push origin add-python-technology
```

Create pull request with:
- Clear title
- Description of changes
- Reference to any issues
- Testing performed

## Content Standards

### Quality Guidelines

✅ **DO:**
- Write clear, concise questions and answers
- Provide practical, real-world examples
- Use proper grammar and spelling
- Keep formatting consistent
- Cite authoritative sources
- Test YAML syntax validity

❌ **DON'T:**
- Copy content without attribution
- Add overly trivial or "gotcha" questions
- Include outdated information
- Use broken or spam links
- Leave incomplete configurations

### File Formatting

**YAML Files:**
- 2 spaces for indentation
- No tabs
- Consistent key ordering
- Comments for complex sections

**Markdown Files:**
- ATX-style headers (`#`, `##`, `###`)
- Blank lines between sections
- Code blocks with language tags
- Consistent bullet list style

## Testing Your Changes

### 1. Validate YAML Syntax

```bash
# Python with PyYAML
python3 -c "import yaml; yaml.safe_load(open('technologies/your-tech/config.yaml'))"

# Or use online validators like yamllint.com
```

### 2. Check File Structure

```bash
# Verify all referenced files exist
ls technologies/your-tech/questions/index.yaml
ls technologies/your-tech/questions/*.md
```

### 3. Verify Question Counts

Ensure `estimated_questions` in `questions/index.yaml` matches actual questions in topic files.

### 4. Test with Custom GPT (Optional)

1. Fork repository and push changes
2. Update `openapi-schema.yaml` server URL to your fork
3. Configure test Custom GPT
4. Test interview flow with new technology

### 5. Verify Links

- Check all resource URLs are accessible
- Ensure documentation links are current
- Test course/book links

## Review Process

1. **Automated Checks** - Basic validation runs automatically
2. **Content Review** - Maintainers review quality and accuracy
3. **Feedback** - You may receive change requests
4. **Approval** - Contribution merged once approved

## Questions or Issues?

- **Questions:** [GitHub Discussions](https://github.com/bardin08/interview-agent/discussions)
- **Bugs:** [GitHub Issues](https://github.com/bardin08/interview-agent/issues)
- **Ideas:** [Feature Requests](https://github.com/Bardin08/interview-agent/issues)

## Recognition

All contributors are recognized in the repository. Thank you for helping improve Interview Agent!

## License

By contributing, you agree that your contributions will be licensed under the MIT License.
