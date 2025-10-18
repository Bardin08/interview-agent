# Generate Interview Report Task
<!-- File: interview-agent/tasks/generate-interview-report.md -->

## Purpose

Generate a comprehensive, actionable feedback report that helps candidates understand their performance and provides clear path to improvement.

## Configuration

```yaml
elicit: false
output_file: true
template: interview-report-tmpl.md
language: from_session
format: markdown
```

## Report Generation Workflow

### 1. Load Session Data

**Input:** `.session-state.yaml` from completed interview

**Extract:**
```yaml
session_data:
  metadata:
    candidate_name
    experience_level
    language
    start_time
    end_time
    total_duration

  performance:
    questions_asked
    questions_answered
    questions_skipped
    total_hints_used
    overall_score

  topic_breakdown:
    - topic_name
    - questions_count
    - average_score
    - hints_used
    - classification

  question_history:
    - [all question records]

  identified_areas:
    strengths: []
    needs_improvement: []
    critical_gaps: []
```

### 2. Calculate Overall Metrics

**Performance Distribution:**

```python
def calculate_distribution(questions):
    excellent = count_where(score == 5)
    very_good = count_where(score == 4)
    good = count_where(score == 3)
    partial = count_where(score == 2)
    weak = count_where(score == 1)
    no_answer = count_where(score == 0)

    return {
        'excellent': (excellent, percentage),
        'very_good': (very_good, percentage),
        'good': (good, percentage),
        'partial': (partial, percentage),
        'weak': (weak, percentage),
        'no_answer': (no_answer, percentage)
    }
```

**Overall Assessment:**

```python
def overall_assessment(average_score):
    if average_score >= 4.25:
        return "Excellent - Interview Ready"
    elif average_score >= 3.75:
        return "Good - Minor improvements needed"
    elif average_score >= 3.0:
        return "Competent - Focused study recommended"
    elif average_score >= 2.5:
        return "Developing - Significant preparation needed"
    else:
        return "Foundational - Extensive study required"
```

### 3. Classify Topics

**For Each Topic:**

```python
def classify_topic(topic_score, hints_used):
    classification = {
        'score': topic_score,
        'hints': hints_used,
        'level': None,
        'priority': None
    }

    if topic_score >= 4.25 and hints_used < 2:
        classification['level'] = 'Mastered'
        classification['priority'] = 4  # Low priority
    elif topic_score >= 3.5:
        classification['level'] = 'Competent'
        classification['priority'] = 3
    elif topic_score >= 2.5:
        classification['level'] = 'Needs Improvement'
        classification['priority'] = 2
    else:
        classification['level'] = 'Critical Gap'
        classification['priority'] = 1  # High priority

    return classification
```

### 4. Identify Patterns

**Cross-Topic Analysis:**

```python
def identify_patterns(topic_data):
    patterns = {
        'related_weaknesses': [],
        'foundation_issues': [],
        'advanced_strengths': [],
        'practical_vs_theoretical': {}
    }

    # Example: If weak in "OOP" and "Inheritance"
    # Pattern: Object-oriented concepts need reinforcement

    # Example: Strong in theory but weak in scenarios
    # Pattern: Needs more practical application

    return patterns
```

### 5. Generate Report Sections

#### Executive Summary

```markdown
# Technical Interview Feedback Report
## {Candidate Name} - {Date}

**Interviewer:** Alex (Senior Technical Interviewer)
**Interview Duration:** {duration}
**Experience Level:** {level}

---

## 🎯 Executive Summary

**Overall Performance:** {score}/5 - {assessment}

**Interview Readiness:** {readiness_assessment}

**Key Takeaways:**
- ✅ Strengths: {primary_strengths}
- 📚 Focus Areas: {primary_weaknesses}
- ⏱️ Estimated Study Time: {hours} hours over {weeks} weeks

**Quick Stats:**
```
Total Questions: {count}
Answered Correctly: {count} ({percentage}%)
Needed Hints: {count} questions
Skipped: {count}

Performance Distribution:
██████████████████ Excellent: {percentage}%
████████████░░░░░░ Good: {percentage}%
████░░░░░░░░░░░░░░ Partial: {percentage}%
██░░░░░░░░░░░░░░░░ Weak: {percentage}%
```

---
```

#### Performance Overview

```markdown
## 📊 Performance Overview

### By Topic Category

| Topic | Questions | Score | Level | Priority |
|-------|-----------|-------|-------|----------|
| {topic} | {count} | {score}/5 | {level} | {priority} |
...

### Performance Chart

```
C# Fundamentals    ████████████████░░ 4.0/5  🟢
OOP Concepts       ███████████░░░░░░░ 3.25/5 🟡
Collections        ████████████████░░ 3.9/5  🟢
Threading          ████░░░░░░░░░░░░░░ 1.75/5 🔴
.NET Framework     ██████████████░░░░ 3.6/5  🟡
ASP.NET Core       ██████████████████ 4.5/5  🟢
Data Access        ███████░░░░░░░░░░░ 2.9/5  🟡
```

**Legend:**
- 🟢 Strong (≥4.0/5) - Mastered
- 🟡 Adequate (3.0-3.9/5) - Competent
- 🔴 Needs Work (<3.0/5) - Requires Focus

---
```

#### Strengths Analysis

```markdown
## 💪 Strengths Analysis

You demonstrated solid understanding in these areas:

### 1. {Strength Topic #1} - {score}/5

**What You Did Well:**
- {specific_capability_1}
- {specific_capability_2}

**Standout Response:**
> **Q:** {question}
> **Your Answer:** {summary}
> **Why It Impressed:** {reason}

**Recommendation:** {how_to_leverage_or_deepen}

---

### 2. {Strength Topic #2} - {score}/5

[Similar structure...]

---

**Overall Strength Pattern:**
{identified_pattern_across_strengths}

---
```

#### Weaknesses Analysis

```markdown
## 📚 Areas for Improvement

These topics require focused attention:

### PRIORITY 1: Critical Gaps

#### {Critical Topic #1} - {score}/5

**📍 Why This Matters:**
{practical_importance}

**🔍 Gaps Identified:**
- [ ] {specific_gap_1}
- [ ] {specific_gap_2}
- [ ] {specific_gap_3}

**❓ Example from Interview:**

**Q:** {question_text}

**Your Answer:**
{candidate_response}

**Expected Answer:**
{correct_answer_with_key_points}

**What You Missed:**
- {missed_point_1}
- {missed_point_2}

**💡 Quick Explanation:**
{clear_explanation_of_concept}

**📖 Immediate Action:**
1. {specific_study_step_1}
2. {specific_study_step_2}
3. {practice_exercise}

---

#### {Critical Topic #2}

[Similar structure...]

---

### PRIORITY 2: Needs Improvement

[Similar format for less critical gaps...]

---

**Weakness Pattern Analysis:**
{identified_patterns_across_weaknesses}

{if_foundation_issues_detected}
⚠️ **Foundation Alert:** Your difficulties in {topics} suggest a gap in {fundamental_concept}. Strengthening this foundation will improve multiple areas simultaneously.

---
```

#### Question-by-Question Review

```markdown
## 📝 Detailed Question Review

Complete breakdown of all questions asked:

---

### Q1: {Question Text}
**Topic:** {topic} | **Difficulty:** {level} | **Score:** {score}/5

**Your Answer:**
{candidate_response_summary}

**Evaluation:** {evaluation_comment}

{if_score_less_than_3}
**Complete Answer:**
{full_correct_answer_with_explanation}

**Key Concepts:**
- {concept_1}
- {concept_2}

{if_hints_given}
**Hints Provided:**
1. {hint_1}
2. {hint_2}

---

[Repeat for all questions...]

---
```

#### Personalized Study Plan

```markdown
## 🎓 Personalized Study Plan

Based on your interview performance, here's your path to mastery:

**Your Profile:**
- Current Level: {experience_level}
- Target Level: {target_based_on_performance}
- Gap Analysis: {assessment}
- Estimated Total Study Time: {hours} hours over {weeks} weeks
- Study Intensity: {hours/week} hours per week

---

### 📅 PHASE 1: Critical Foundations ({duration_weeks} weeks)

**Goal:** Address fundamental gaps that block further progress

#### Week 1-2: {Critical_Topic_1}

**🎯 Learning Objectives:**
- [ ] {specific_objective_1}
- [ ] {specific_objective_2}
- [ ] {specific_objective_3}

**📚 Study Resources:**

*Primary:*
- [ ] [Microsoft Docs: {topic}](link) - Read sections: {specific_sections}
- [ ] [Book: {title}](link) - Chapter {number}: {title}

*Supplementary:*
- [ ] [Video: {title}](link) - {duration} - Focus on {specific_part}
- [ ] [Article: {title}](link) - {key_takeaway}

**💻 Hands-On Practice:**

*Exercise 1: {title}*
```csharp
// Create a simple program that demonstrates {concept}
// Requirements:
// - {requirement_1}
// - {requirement_2}
```

*Exercise 2: {title}*
{exercise_description}

**✅ Self-Check Questions:**
1. {question_to_test_understanding}
2. {question_to_test_understanding}
3. {question_to_test_understanding}

*If you can answer these confidently, you're ready to move on!*

**⏱️ Time Allocation:**
- Theory: {hours} hours
- Practice: {hours} hours
- Review: {hours} hours
- **Total: {hours} hours**

---

#### Week 3-4: {Critical_Topic_2}

[Similar detailed structure...]

---

### 📅 PHASE 2: Skill Enhancement ({duration_weeks} weeks)

**Goal:** Build competence in areas with partial understanding

[Similar structure for "Needs Improvement" topics, but less detailed...]

---

### 📅 PHASE 3: Advanced Mastery ({duration_weeks} weeks)

**Goal:** Deepen strengths and explore advanced topics

**Topics to Explore:**
- {advanced_topic_related_to_strengths}
- {advanced_topic_for_career_growth}

**Activities:**
- Deep-dive into {specific_advanced_area}
- Build comprehensive project incorporating {multiple_topics}
- Contribute to open-source {type_of_project}
- Prepare for {certification_or_goal}

---

### 🚀 Hands-On Projects

Real-world projects to consolidate learning:

#### Project 1: {Title}
**Topics Practiced:** {topic_list}

**Description:**
{what_to_build}

**Requirements:**
- {requirement_1}
- {requirement_2}
- {requirement_3}

**Learning Goals:**
- {goal_1}
- {goal_2}

**Estimated Time:** {hours} hours

**Bonus Challenges:**
- {advanced_feature_1}
- {advanced_feature_2}

---

#### Project 2: {Title}

[Similar structure...]

---

### 📊 Progress Tracking

**Weekly Checklist:**

Week 1:
- [ ] Completed {topic} readings
- [ ] Finished {count} exercises
- [ ] Answered self-check questions
- [ ] Built mini-project

[Repeat for all weeks...]

**Milestone Checkpoints:**

✓ End of Week 2: Can explain {concepts} clearly
✓ End of Week 4: Completed Phase 1 projects
✓ End of Week 6: Scoring 80%+ on practice questions
✓ End of Week 8: Ready for re-interview

---
```

#### Recommended Resources

```markdown
## 📖 Curated Learning Resources

Resources specifically selected for your identified gaps:

### Official Documentation
- [Microsoft C# Documentation](link) - Essential reading for {topics}
- [.NET API Reference](link) - For {specific_apis}
- [ASP.NET Core Docs](link) - Focus on {specific_areas}

### Books

**For Foundation Building:**
- 📘 {Book Title} by {Author}
  - *Why:* {reason_for_recommendation}
  - *Focus Chapters:* {chapters}
  - *Your Gaps Covered:* {topics}

**For Practical Application:**
- 📗 {Book Title} by {Author}
  - *Why:* {reason}
  - *Project Ideas:* {suggestions}

### Online Courses

**Priority:**
- 🎓 [{Course Name}]({link}) - {Platform}
  - Duration: {hours} hours
  - Covers: {your_gap_topics}
  - Cost: {price}
  - Certificate: {yes/no}

**Supplementary:**
- 🎓 [{Course Name}]({link}) - {Platform}

### Video Tutorials

**For Visual Learners:**
- 🎥 [{Series Name}]({link}) - {Channel}
  - Focus on episodes: {numbers}
  - Addresses your gaps in: {topics}

### Practice Platforms

**Coding Practice:**
- 💻 [LeetCode](link) - Problem sets:
  - {category}: {specific_problems}
  - Focus on: {difficulty_range}

- 💻 [HackerRank](link) - Challenges:
  - {domain} track
  - {specific_skills}

- 💻 [Exercism.io](link) - C# Track
  - Mentored practice
  - Focus on {exercises}

**Interview Prep:**
- 🎯 [Platform Name](link)
  - Mock interviews
  - {specific_topic} questions

### Communities & Support

**Get Help:**
- 💬 [Stack Overflow](link) - Tag: {relevant_tags}
- 💬 [r/dotnet](link) - Reddit community
- 💬 [C# Discord](link) - Real-time help

**Stay Updated:**
- 📰 [.NET Blog](link)
- 📰 [{Influential Developer} Blog](link)
- 🐦 Twitter: {recommended_follows}

### Tools & IDEs

**Essential Tools:**
- Visual Studio 2022 - {specific_features_to_use}
- VS Code with extensions: {extension_list}
- LINQPad - For practicing LINQ queries
- {Tool relevant to gaps}

---
```

#### Next Steps

```markdown
## 🎯 Your Next Steps

### Immediate Actions (This Week)

1. **📅 Set Your Schedule**
   - Block {hours} hours/week for focused study
   - Best times: {recommendation_based_on_interview_time}
   - Use calendar/reminder app

2. **⚡ Start with Priority 1**
   - Begin with {highest_priority_topic}
   - Complete Week 1 objectives
   - Goal: {specific_milestone}

3. **💻 Set Up Practice Environment**
   - Install {tools}
   - Clone starter projects from {repos}
   - Bookmark resources

4. **📝 Track Your Progress**
   - Use study plan checklist
   - Note: questions as they arise
   - Celebrate small wins!

### Short-Term Goals (2-4 Weeks)

- ✅ Complete Phase 1 of study plan
- ✅ Build {project_1}
- ✅ Score 80%+ on {topic} practice questions
- ✅ Revisit self-check questions from this interview

### Medium-Term Goals (1-2 Months)

- ✅ Complete Phases 1 & 2
- ✅ Build {comprehensive_project}
- ✅ Contribute to open-source project
- ✅ Schedule follow-up interview

### Long-Term Goals (3-6 Months)

- ✅ Master all identified gap areas
- ✅ Complete {certification} (optional)
- ✅ Build portfolio project
- ✅ Ready for {target_role} interviews

---

### 🔄 Progress Checkpoints

**2 Weeks:** Self-assess with questions from Phase 1
**4 Weeks:** Build mini-project covering Phase 1 & 2 topics
**8 Weeks:** Request follow-up interview to measure improvement

**I'm here to help! Use *begin to start another session anytime.**

---

## 💪 Final Thoughts

{personalized_encouragement}

**Remember:**
- 🎯 Focus beats breadth - tackle one topic at a time
- 💻 Code every day - even 30 minutes helps
- 📚 Understand "why", not just "how"
- 🤝 Join communities - learning together is faster
- 🔄 Review regularly - spaced repetition works
- ❓ Ask questions - there are no stupid questions

**Your Strengths:**
You showed real understanding in {strength_topics}. These are valuable skills that many struggle with. Build on this foundation!

**Your Opportunity:**
The gaps we identified are common and absolutely fixable. With the structured plan above and {hours} hours of focused effort, you'll see significant improvement.

**You've got this!** 🚀

The fact that you completed this interview shows you're serious about growth. That mindset matters more than current knowledge level.

---

## 📧 Follow-Up

- Questions about this report? [Contact info]
- Ready for re-interview? Use `*begin` command
- Want to focus on specific topic? Use `*focus {topic}`

---

**Report Generated:** {timestamp}
**Interview Session ID:** {session_id}
**Interviewer:** Alex - Senior Technical Interviewer

*Keep this report handy as your study guide. Good luck!* ✨

---
```

### 6. Language Adaptation

**Critical:** Generate entire report in session language

**Implementation:**
- Translate all section headers
- Translate explanatory text
- Keep technical terms in English with translations where helpful
- Keep code examples as-is
- Translate resource descriptions

**Example (Russian):**
```markdown
## 💪 Области Сильных Сторон

Вы продемонстрировали отличное понимание в этих областях:

### 1. ASP.NET Core - 90%

**Что Вы Сделали Хорошо:**
- Четкое объяснение Dependency Injection
- Понимание middleware pipeline
...
```

### 7. File Operations

**Generate Report File:**

```python
filename = f"interview-report-{candidate_name}-{date}.md"
filepath = f"reports/{filename}"

# Ensure directory exists
create_directory_if_not_exists("reports/")

# Write report
write_file(filepath, report_content)

# Also save session data
session_filepath = f"reports/.session-{candidate_name}-{date}.yaml"
write_file(session_filepath, session_data_yaml)
```

### 8. Display Summary

**After Report Generated:**

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Your Interview Report is Ready!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Quick Summary:
   Overall Score: {percentage}% - {assessment}
   Topics Mastered: {count}
   Focus Areas: {count}
   Study Plan Duration: {weeks} weeks ({hours} total hours)

📄 Report Location: {filepath}

🎯 Top Priority:
   Start with {highest_priority_topic} this week
   Estimated time: {hours} hours
   First resource: {primary_resource}

📚 What's Inside:
   ✓ Detailed performance analysis
   ✓ Every question reviewed
   ✓ Week-by-week study plan
   ✓ Curated resources
   ✓ Hands-on projects
   ✓ Progress tracking checklist

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Next Steps:
   1. Read the full report carefully
   2. Set up your study schedule
   3. Start with Phase 1, Week 1
   4. Track your progress using the checklist

Good luck with your learning journey! 🚀

Would you like me to:
1. Explain any part of the report
2. Suggest additional resources for specific topics
3. Schedule a follow-up interview
4. Start a new interview session
```

## Quality Assurance

**Before Finalizing Report:**

### Completeness Check
- [ ] All questions reviewed with evaluations
- [ ] All topics analyzed and classified
- [ ] Study plan covers all identified gaps
- [ ] Resources are relevant and accessible
- [ ] Timeline estimates are realistic
- [ ] Encouragement is personalized to candidate

### Accuracy Check
- [ ] Scores calculated correctly
- [ ] Topic classifications match performance
- [ ] No mathematical errors
- [ ] Resource links are valid (if possible to verify)
- [ ] Technical explanations are correct

### Tone Check
- [ ] Constructive, not critical
- [ ] Encouraging, not patronizing
- [ ] Professional, not overly casual
- [ ] Specific, not vague
- [ ] Actionable, not just descriptive
- [ ] Balanced (acknowledges strengths AND weaknesses)

### Language Check
- [ ] Consistent with candidate's language
- [ ] Technical accuracy maintained across translations
- [ ] Clear and easy to understand
- [ ] Free of grammatical errors
- [ ] Formatting is consistent

## Task Completion

**Task completes when:**
1. ✅ Report file successfully created
2. ✅ Session data archived
3. ✅ Summary displayed to candidate
4. ✅ Follow-up options presented

**Final State:**
- Report saved in `/reports/`
- Session data saved for future reference
- Agent ready for follow-up or new session
