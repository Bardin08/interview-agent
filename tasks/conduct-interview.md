# Conduct Technical Interview Task
<!-- File: interview-agent/tasks/conduct-interview.md -->

## Purpose

Conduct a structured, adaptive technical interview session that assesses candidate's knowledge, identifies gaps, provides guidance, and tracks progress for comprehensive reporting.

## Configuration

```yaml
elicit: true
interactive: true
requires_user_input: true
adaptive_flow: true
auto_save: true
```

## Pre-Interview Setup

### 1. Initial Greeting & Language Detection

```text
Hello! I'm Alex, your Senior Technical Interviewer for today's .NET/C# interview session. 👋

I'll conduct this interview in your preferred language. Please introduce yourself briefly, and I'll adapt to your language automatically.

Before we begin, let me explain the format:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 Interview Format:
   • Questions from various .NET/C# topics
   • Use *hint if you get stuck
   • We'll identify areas for improvement together
   • Detailed feedback report at the end

⏱️  Duration: 45-90 minutes (depending on level)
🎯 Goal: Help you discover and strengthen weak spots
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Please tell me:
1. Your name
2. Your experience level:
   1️⃣  Fresher (0-1 years)
   2️⃣  Junior (1-2 years)
   3️⃣  Mid-level (2-5 years)
   4️⃣  Senior (5+ years)
   5️⃣  Architect (7+ years)
```

**Actions:**
1. Detect language from candidate's response
2. Extract name and experience level
3. Store in session state
4. Initialize session tracking

### 2. Session Initialization

Create session state:

```yaml
session:
  candidate_name: "{name}"
  experience_level: "{level}"
  language: "{detected_language}"
  start_time: "{ISO8601_timestamp}"

  configuration:
    question_count_target: "{from_level_config}"
    topics: ["{from_level_config}"]
    hint_threshold: "{from_level_config}"
    complexity_range: ["{min}", "{max}"]

  progress:
    current_phase: warmup
    questions_asked: 0
    topics_covered: []
    time_elapsed: 0

  performance:
    total_questions: 0
    correct: 0
    partial: 0
    incorrect: 0
    skipped: 0
    hints_used: 0

  topic_performance: {}
  question_history: []

  identified_strengths: []
  identified_weaknesses: []
  identified_critical_gaps: []
```

### 3. Confirm Start

```text
Great to meet you, {name}! 🎯

Based on your {level} level experience, I've prepared {count} questions covering:
{list topics}

Ready to begin? Type 'yes' or 'ready' to start, or ask any questions first.

💡 Remember: You can use *hint, *skip, or *pause at any time.
```

## Interview Execution

### Phase 1: Warm-Up (2-3 questions)

**Purpose:** Build confidence, establish baseline

**Question Selection:**
- Topic: C# Language Fundamentals
- Difficulty: Easy
- Count: 2-3 questions

**Example Questions:**
```yaml
q1:
  text: "What's the difference between value types and reference types in C#?"
  topic: C# Fundamentals
  difficulty: easy
  key_points:
    - Value types store actual data
    - Reference types store memory reference
    - Value types on stack, reference on heap
    - Examples of each

q2:
  text: "Can you explain what a static constructor is and when it's called?"
  topic: C# Fundamentals
  difficulty: easy
  key_points:
    - Initializes static members
    - Called automatically before first use
    - No parameters or access modifiers
    - Called only once

q3:
  text: "What does the 'readonly' keyword do?"
  topic: C# Fundamentals
  difficulty: easy
  key_points:
    - Makes field immutable after initialization
    - Can be set in declaration or constructor
    - Different from const
```

**Presentation Format:**

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📝 Question {number}/{total}
Topic: {topic_name}

{question_text}

[Wait for answer]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Response Evaluation:**

For each answer:

1. **Analyze candidate's response**
   - Check for key points mentioned
   - Assess depth of understanding
   - Note any misconceptions
   - Detect confidence level

2. **Score the response**
   ```yaml
   scoring:
     100: All key points + deep understanding
     75: Most key points + good understanding
     50: Some key points + partial understanding
     25: Few key points + misunderstandings
     0: Incorrect or no answer
   ```

3. **Provide feedback**

   **If Excellent (≥85):**
   ```text
   ✅ Excellent! You clearly understand {concept}.
   {optional: specific_strength_noted}

   Let's move to the next question.
   ```

   **If Good (70-84):**
   ```text
   ✅ Good answer!

   To complete your understanding: {additional_point}

   Moving on...
   ```

   **If Partial (50-69):**
   ```text
   🟡 You're on the right track with {what_was_correct}.

   However, {what_was_missed}.

   This is an important concept because {why_it_matters}.

   Let's continue.
   ```

   **If Weak (<50):**
   ```text
   🔴 I see this is challenging. Let me help clarify:

   {brief_explanation}

   We'll come back to related concepts. This is noted for your study plan.
   ```

4. **Record to session**
   ```yaml
   question_record:
     number: {n}
     topic: "{topic}"
     question: "{text}"
     candidate_answer: "{summary}"
     score: {0-100}
     hints_given: {count}
     evaluation: "{analysis}"
     timestamp: "{ISO8601}"
   ```

5. **Update metrics**
   - Increment question count
   - Update topic performance
   - Track time spent
   - Adjust difficulty if needed

### Phase 2: Core Assessment

**Topic Selection Logic:**

```python
def select_next_topic(session):
    covered = session.topics_covered
    available = session.configuration.topics - covered
    performance = session.average_score_last_3

    if performance < 50:
        # Struggling - easier topics
        return select_fundamental_topic(available)
    elif performance > 85:
        # Excelling - advanced topics
        return select_advanced_topic(available)
    else:
        # Balanced - follow curriculum
        return next_topic_in_sequence(available)
```

**Question Flow:**

For each topic:

1. **Announce Topic**
   ```text
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   📚 Next Topic: {topic_name}

   I'll ask you {count} questions about this area.
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
   ```

2. **Ask Conceptual Question**
   - Focus on understanding
   - "What is..." or "Explain..."

3. **Evaluate Response**

4. **Ask Practical Question**
   - Focus on application
   - "When would you use..."
   - "How would you implement..."

5. **Evaluate Response**

6. **Adapt Based on Performance**

   **If struggling:**
   - Provide simpler follow-up
   - Offer more hints
   - Explain concepts clearly

   **If excelling:**
   - Ask about edge cases
   - Request code example
   - Probe deeper understanding

7. **Topic Wrap-up**
   ```text
   {topic_name} completed. ✓

   {brief_performance_comment}
   ```

**Real-Time Adaptation:**

Monitor signals:
- **Multiple hints needed** → Reduce difficulty
- **Quick, confident answers** → Increase difficulty
- **Confusion or hesitation** → Provide encouragement
- **Strong performance** → Note as strength
- **Weak performance** → Note as gap

### Phase 3: Deep Dive (Conditional)

**Triggered When:**
- Candidate shows exceptional strength in area
- Fundamental gap needs exploration
- Time permits deeper assessment

**For Strength Areas:**

```text
I notice you have strong knowledge in {topic}! 💪

Let me explore this further with an advanced scenario:

{scenario_based_question}
```

**For Weak Areas:**

```text
Let's take a moment to strengthen your understanding of {topic}.

{clear_explanation_with_examples}

Now, let me ask a simpler question to reinforce this:

{easier_follow_up_question}
```

### Hint System Implementation

**When candidate uses `*hint`:**

1. **Determine current hint level**
   - Check hints given for current question
   - Increment level (1-5)

2. **Provide appropriate hint**

**Level 1 - Gentle Nudge:**
```text
💡 Hint #1: Think about how {concept_A} relates to {concept_B}.
```

**Level 2 - Direction:**
```text
💡 Hint #2: Consider the key difference between {X} and {Y}.
Which characteristic applies here?
```

**Level 3 - Example:**
```text
💡 Hint #3: Let me give you a concrete example:

{code_example_or_scenario}

Now, can you see how to approach the original question?
```

**Level 4 - Partial Answer:**
```text
💡 Hint #4: The main point is that {partial_answer}.

Can you explain why this is the case?
```

**Level 5 - Full Explanation:**
```text
💡 Full Explanation:

{complete_answer_with_reasoning}

This is an important concept to master. I've noted this for your study plan.

Let's move to the next question.
```

3. **Record hint usage**
4. **If level 5 reached, move to next question**

### Skip Command Handling

**When candidate uses `*skip`:**

```text
⏭️  Question skipped.

This will be marked as "needs review" in your report.

Moving to next question...
```

**Actions:**
- Record as skipped (score: 0)
- Add to "needs review" list
- Note topic for study plan
- Continue interview

### Pause/Resume Handling

**When candidate uses `*pause`:**

```text
⏸️  Interview paused.

Your progress has been saved. Use *resume when ready to continue.

Current progress: {answered}/{total} questions
```

**Actions:**
- Save complete session state to .session-state.yaml
- Display progress summary
- Wait for *resume command

**When candidate uses `*resume`:**

```text
▶️  Resuming interview...

Welcome back, {name}!

Progress: {answered}/{total} questions
Last topic: {topic}

Ready to continue? I'll pick up where we left off.
```

**Actions:**
- Load session state from file
- Restore context
- Continue from next question

### Analyze Command

**When candidate uses `*analyze`:**

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 Real-Time Performance Analysis
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Progress: {answered}/{total} questions ({percentage}%)
Time Elapsed: {duration}

Overall Score: {average_score}%
█████████░░░░░░░ {percentage}%

Topics Covered:
✅ {topic_1}: {score}% {indicator}
✅ {topic_2}: {score}% {indicator}
🔄 {current_topic}: In progress

Current Strengths:
💪 {strength_topic_1}
💪 {strength_topic_2}

Areas to Focus On:
📚 {weak_topic_1} - {brief_note}
📚 {weak_topic_2} - {brief_note}

Hints Used: {count}

{encouraging_message}
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Continue when ready!
```

**Indicators:**
- 🟢 Strong (≥80%)
- 🟡 Adequate (60-79%)
- 🔴 Needs Work (<60%)

## Session Conclusion

### When Target Questions Reached

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🎯 Interview Session Complete!
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Thank you for completing this interview, {name}!

Quick Summary:
✓ Questions Answered: {total}
✓ Time Spent: {duration}
✓ Topics Covered: {count}

Strong Areas:
💪 {topic_list}

Focus Areas:
📚 {topic_list}

Overall Performance: {score}% {indicator}

I'm now generating your comprehensive feedback report...

This report will include:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✓ Detailed performance analysis by topic
✓ Question-by-question review
✓ Specific areas for improvement
✓ Personalized study plan with timeline
✓ Curated learning resources
✓ Hands-on project recommendations
✓ Next steps for your development
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Generating report... ⏳
```

**Actions:**
1. Finalize session metrics
2. Classify all topics (mastered/competent/needs improvement/critical gap)
3. Identify patterns in weaknesses
4. Automatically execute generate-interview-report task
5. Display report summary
6. Save complete session data

## Error Handling

### Candidate Loses Focus

**Detect:**
- Very long pauses
- Incoherent answers
- Explicit fatigue signals

**Response:**
```text
I notice this might be getting tiring. Would you like to:

1. Take a 5-minute break (*pause)
2. Skip this question (*skip)
3. Get a hint (*hint)
4. End session early and get partial report (*exit)
5. Continue as is

What would you prefer?
```

### Connection Issues

**If session state corrupted:**
- Load from last auto-save
- Resume from checkpoint
- Inform candidate of data recovery

## Auto-Save Mechanism

**Trigger:** After every question answered

**Save Location:** `.session-state.yaml`

**Contents:**
- Complete session object
- All question history
- Current progress
- Performance metrics

**Format:**
```yaml
auto_save:
  timestamp: "{ISO8601}"
  candidate: "{name}"
  progress: "{percentage}"

session:
  # Complete session data
```

## Task Completion Criteria

Task completes when:
- ✅ Target questions reached OR
- ✅ Candidate uses *exit OR
- ✅ Time limit exceeded (if set) OR
- ✅ Critical error (with recovery attempted)

**Final Actions:**
1. Save final session state
2. Trigger report generation
3. Clean up temporary data
4. Return to agent ready state

## Notes for Implementation

**Critical Behaviors:**
- Maintain language consistency throughout
- Save state after every question
- Adapt difficulty dynamically
- Be genuinely encouraging
- Track everything for reporting
- Handle interruptions gracefully
- Provide clear navigation options

**Performance Tracking:**
- Update metrics in real-time
- Calculate running averages
- Identify trends across topics
- Flag patterns in difficulties

**User Experience:**
- Clear visual separators
- Progress indicators
- Encouraging messages
- Easy command access
- Transparent about what's happening
