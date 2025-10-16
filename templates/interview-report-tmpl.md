# Technical Interview Feedback Report
<!-- File: interview-agent/templates/interview-report-tmpl.md -->
## {{candidate_name}} - {{date}}

**Interviewer:** Alex (Senior Technical Interviewer)
**Interview Duration:** {{duration}}
**Experience Level:** {{experience_level}}

---

## 🎯 Executive Summary

**Overall Performance:** {{overall_score}}% - {{assessment}}

**Interview Readiness:** {{readiness_assessment}}

**Key Takeaways:**
- ✅ Strengths: {{primary_strengths}}
- 📚 Focus Areas: {{primary_weaknesses}}
- ⏱️ Estimated Study Time: {{study_hours}} hours over {{study_weeks}} weeks

**Quick Stats:**
```
Total Questions: {{total_questions}}
Answered Correctly: {{correct_count}} ({{correct_percentage}}%)
Needed Hints: {{hints_count}} questions
Skipped: {{skipped_count}}

Performance Distribution:
{{performance_bar_excellent}} Excellent: {{excellent_percentage}}%
{{performance_bar_good}} Good: {{good_percentage}}%
{{performance_bar_partial}} Partial: {{partial_percentage}}%
{{performance_bar_weak}} Weak: {{weak_percentage}}%
```

---

## 📊 Performance Overview

### By Topic Category

| Topic | Questions | Score | Level | Priority |
|-------|-----------|-------|-------|----------|
{{#each topic_performance}}
| {{topic_name}} | {{question_count}} | {{score}}% | {{level}} | {{priority}} |
{{/each}}

### Performance Chart

```
{{#each topic_performance}}
{{topic_name_padded}} {{progress_bar}} {{score}}%  {{indicator}}
{{/each}}
```

**Legend:**
- 🟢 Strong (≥80%) - Mastered
- 🟡 Adequate (60-79%) - Competent
- 🔴 Needs Work (<60%) - Requires Focus

---

## 💪 Strengths Analysis

You demonstrated solid understanding in these areas:

{{#each strengths}}
### {{number}}. {{topic_name}} - {{score}}%

**What You Did Well:**
{{#each capabilities}}
- {{this}}
{{/each}}

**Standout Response:**
> **Q:** {{standout_question}}
> **Your Answer:** {{answer_summary}}
> **Why It Impressed:** {{impression_reason}}

**Recommendation:** {{recommendation}}

---
{{/each}}

**Overall Strength Pattern:**
{{strength_pattern}}

---

## 📚 Areas for Improvement

These topics require focused attention:

### PRIORITY 1: Critical Gaps

{{#each critical_gaps}}
#### {{topic_name}} - {{score}}%

**📍 Why This Matters:**
{{importance}}

**🔍 Gaps Identified:**
{{#each gaps}}
- [ ] {{this}}
{{/each}}

**❓ Example from Interview:**

**Q:** {{example_question}}

**Your Answer:**
{{candidate_answer}}

**Expected Answer:**
{{correct_answer}}

**What You Missed:**
{{#each missed_points}}
- {{this}}
{{/each}}

**💡 Quick Explanation:**
{{explanation}}

**📖 Immediate Action:**
{{#each action_steps}}
{{number}}. {{step}}
{{/each}}

---
{{/each}}

### PRIORITY 2: Needs Improvement

{{#each needs_improvement}}
[Similar structure as critical gaps, but briefer]
{{/each}}

---

**Weakness Pattern Analysis:**
{{weakness_pattern}}

{{#if foundation_issue}}
⚠️ **Foundation Alert:** {{foundation_issue_description}}
{{/if}}

---

## 📝 Detailed Question Review

Complete breakdown of all questions asked:

{{#each questions}}
---

### Q{{number}}: {{question_text}}
**Topic:** {{topic}} | **Difficulty:** {{difficulty}} | **Score:** {{score}}%

**Your Answer:**
{{candidate_answer}}

**Evaluation:** {{evaluation}}

{{#if score_below_70}}
**Complete Answer:**
{{correct_answer}}

**Key Concepts:**
{{#each key_concepts}}
- {{this}}
{{/each}}
{{/if}}

{{#if hints_given}}
**Hints Provided:**
{{#each hints}}
{{number}}. {{hint_text}}
{{/each}}
{{/if}}

{{/each}}

---

## 🎓 Personalized Study Plan

Based on your interview performance, here's your path to mastery:

**Your Profile:**
- Current Level: {{experience_level}}
- Target Level: {{target_level}}
- Gap Analysis: {{gap_assessment}}
- Estimated Total Study Time: {{total_study_hours}} hours over {{total_study_weeks}} weeks
- Study Intensity: {{hours_per_week}} hours per week

---

{{#each study_phases}}
### 📅 {{phase_name}} ({{duration_weeks}} weeks)

**Goal:** {{phase_goal}}

{{#each weeks}}
#### Week {{week_number}}: {{topic}}

**🎯 Learning Objectives:**
{{#each objectives}}
- [ ] {{this}}
{{/each}}

**📚 Study Resources:**

*Primary:*
{{#each primary_resources}}
- [ ] [{{title}}]({{link}}) - {{description}}
{{/each}}

*Supplementary:*
{{#each supplementary_resources}}
- [ ] [{{title}}]({{link}}) - {{description}}
{{/each}}

**💻 Hands-On Practice:**

{{#each exercises}}
*Exercise {{number}}: {{title}}*
{{description}}
```{{language}}
{{code_starter}}
```
{{/each}}

**✅ Self-Check Questions:**
{{#each self_check_questions}}
{{number}}. {{question}}
{{/each}}

*If you can answer these confidently, you're ready to move on!*

**⏱️ Time Allocation:**
- Theory: {{theory_hours}} hours
- Practice: {{practice_hours}} hours
- Review: {{review_hours}} hours
- **Total: {{total_hours}} hours**

---
{{/each}}
{{/each}}

### 🚀 Hands-On Projects

Real-world projects to consolidate learning:

{{#each projects}}
#### Project {{number}}: {{title}}
**Topics Practiced:** {{topics}}

**Description:**
{{description}}

**Requirements:**
{{#each requirements}}
- {{this}}
{{/each}}

**Learning Goals:**
{{#each learning_goals}}
- {{this}}
{{/each}}

**Estimated Time:** {{hours}} hours

**Bonus Challenges:**
{{#each bonus_challenges}}
- {{this}}
{{/each}}

---
{{/each}}

### 📊 Progress Tracking

**Weekly Checklist:**

{{#each weeks}}
Week {{number}}:
- [ ] Completed {{topic}} readings
- [ ] Finished {{exercise_count}} exercises
- [ ] Answered self-check questions
- [ ] Built mini-project

{{/each}}

**Milestone Checkpoints:**

{{#each milestones}}
✓ {{milestone}}
{{/each}}

---

## 📖 Curated Learning Resources

Resources specifically selected for your identified gaps:

### Official Documentation
{{#each official_docs}}
- [{{title}}]({{link}}) - {{description}}
{{/each}}

### Books

{{#each books}}
**{{category}}:**
- 📘 {{title}} by {{author}}
  - *Why:* {{reason}}
  - *Focus Chapters:* {{chapters}}
  - *Your Gaps Covered:* {{topics}}

{{/each}}

### Online Courses

{{#each courses}}
**{{priority_level}}:**
- 🎓 [{{title}}]({{link}}) - {{platform}}
  - Duration: {{duration}} hours
  - Covers: {{topics}}
  - Cost: {{cost}}
  - Certificate: {{certificate}}

{{/each}}

### Video Tutorials

{{#each video_tutorials}}
- 🎥 [{{title}}]({{link}}) - {{channel}}
  - Focus on episodes: {{episodes}}
  - Addresses your gaps in: {{topics}}

{{/each}}

### Practice Platforms

{{#each practice_platforms}}
**{{category}}:**
- 💻 [{{name}}]({{link}})
  {{#each details}}
  - {{this}}
  {{/each}}

{{/each}}

### Communities & Support

{{#each communities}}
**{{category}}:**
{{#each items}}
- {{icon}} [{{name}}]({{link}}) - {{description}}
{{/each}}

{{/each}}

### Tools & IDEs

**Essential Tools:**
{{#each tools}}
- {{name}} - {{purpose}}
{{/each}}

---

## 🎯 Your Next Steps

### Immediate Actions (This Week)

{{#each immediate_actions}}
{{number}}. **{{title}}**
   {{#each details}}
   - {{this}}
   {{/each}}

{{/each}}

### Short-Term Goals (2-4 Weeks)

{{#each short_term_goals}}
- ✅ {{goal}}
{{/each}}

### Medium-Term Goals (1-2 Months)

{{#each medium_term_goals}}
- ✅ {{goal}}
{{/each}}

### Long-Term Goals (3-6 Months)

{{#each long_term_goals}}
- ✅ {{goal}}
{{/each}}

---

### 🔄 Progress Checkpoints

{{#each checkpoints}}
**{{timeframe}}:** {{checkpoint}}
{{/each}}

**I'm here to help! Use `*begin` to start another session anytime.**

---

## 💪 Final Thoughts

{{personalized_encouragement}}

**Remember:**
- 🎯 Focus beats breadth - tackle one topic at a time
- 💻 Code every day - even 30 minutes helps
- 📚 Understand "why", not just "how"
- 🤝 Join communities - learning together is faster
- 🔄 Review regularly - spaced repetition works
- ❓ Ask questions - there are no stupid questions

**Your Strengths:**
{{strength_summary}}

**Your Opportunity:**
{{opportunity_summary}}

**You've got this!** 🚀

{{final_encouragement}}

---

## 📧 Follow-Up

- Questions about this report? {{contact_info}}
- Ready for re-interview? Use `*begin` command
- Want to focus on specific topic? Use `*focus {topic}`

---

**Report Generated:** {{generation_timestamp}}
**Interview Session ID:** {{session_id}}
**Interviewer:** Alex - Senior Technical Interviewer

*Keep this report handy as your study guide. Good luck!* ✨

---
