# Analyze Performance Task
<!-- File: interview-agent/tasks/analyze-performance.md -->

## Purpose

Provide real-time performance analysis during interview session to help candidate understand their current progress and adjust their approach.

## Configuration

```yaml
elicit: false
interactive: true
real_time: true
```

## Analysis Workflow

### 1. Load Current Session State

**Extract:**
```yaml
current_state:
  questions_answered: {count}
  questions_remaining: {count}
  time_elapsed: {duration}
  current_topic: {topic}

  metrics:
    overall_score: {score_0_to_5}
    topic_scores: {}
    hints_used: {count}

  performance_trend:
    - {recent_scores}
```

### 2. Calculate Real-Time Metrics

**Overall Performance:**
```python
average_score = sum(all_scores) / len(all_scores)
trend = analyze_trend(last_5_scores)
```

**Topic Performance:**
```python
for topic in covered_topics:
    topic_average = calculate_topic_average(topic)
    topic_classification = classify_performance(topic_average)
```

### 3. Generate Analysis Display

**Format:**

```text
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📊 Real-Time Performance Analysis
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⏱️  Session Progress
   Time Elapsed: {MM:SS}
   Questions: {answered}/{total} ({percentage}% complete)

📈 Overall Performance
   Current Score: {average}/5
   {visual_progress_bar}

   Performance Trend: {trend_indicator}
   {trend_explanation}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 Topics Covered

{for each completed topic:}
✅ {topic_name}
   Score: {score}/5 {indicator}
   Questions: {count}
   Status: {classification}

{if current topic in progress:}
🔄 {topic_name} (In Progress)
   Questions so far: {count}
   Current average: {score}/5

{for remaining topics:}
⏳ {topic_name} (Upcoming)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💪 Current Strengths

{for each strength identified:}
✓ {topic}: {score}/5 - {brief_comment}

📚 Areas to Focus On

{for each weakness identified:}
⚠️ {topic}: {score}/5 - {brief_comment}
   {actionable_tip}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

💡 Interview Tips

Hints Used: {count}
{if hints_high:}
💭 Tip: Take a moment to think through your answer before responding. If stuck, try to explain your thought process.

{if performance_declining:}
💭 Tip: Don't worry about recent questions. Stay focused and do your best!

{if performance_strong:}
💭 Tip: Great work! Challenge yourself to explain the "why" behind concepts.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

{encouraging_message_based_on_performance}

Continue when ready! 🚀

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### 4. Trend Analysis

**Detect Performance Trends:**

```python
def analyze_trend(recent_scores):
    if len(recent_scores) < 3:
        return "Establishing baseline"

    avg_first_half = average(recent_scores[:len//2])
    avg_second_half = average(recent_scores[len//2:])

    diff = avg_second_half - avg_first_half

    if diff > 10:
        return "📈 Improving - You're hitting your stride!"
    elif diff < -10:
        return "📉 Declining - Let's refocus. Take your time."
    else:
        return "➡️ Steady - Consistent performance"
```

### 5. Personalized Encouragement

**Based on Performance:**

```python
def generate_encouragement(average_score, trend):
    if average_score >= 4.0:
        messages = [
            "Excellent work! You're demonstrating strong knowledge.",
            "You're doing great! Keep up this level of understanding.",
            "Impressive performance! You clearly know your stuff."
        ]
    elif average_score >= 3.25:
        messages = [
            "Good progress! You're showing solid understanding.",
            "You're doing well! Some areas to strengthen, but overall positive.",
            "Nice work! You're on the right track."
        ]
    elif average_score >= 2.5:
        messages = [
            "Keep going! Everyone has knowledge gaps - we're identifying yours.",
            "You're learning! Each question helps us build your study plan.",
            "Don't be discouraged! This is about growth, not perfection."
        ]
    else:
        messages = [
            "Remember: this is a learning opportunity! We're finding areas to focus on.",
            "Every expert started somewhere! We're building your roadmap to mastery.",
            "Stay positive! Identifying gaps is the first step to improvement."
        ]

    # Add trend-specific message
    if trend == "improving":
        messages.append("And you're improving as we go - great sign!")

    return random.choice(messages)
```

### 6. Actionable Insights

**Provide Tips Based on Patterns:**

```python
insights = []

# If struggling with specific type
if weak_in_theoretical and strong_in_practical:
    insights.append(
        "💡 Pattern detected: Strong practical skills, theory needs review. "
        "Try connecting concepts to real-world use cases."
    )

# If using many hints
if hints_per_question > 1.5:
    insights.append(
        "💡 You're using hints frequently. Consider taking more time to "
        "think through answers before responding."
    )

# If skipping questions
if skipped_count > 2:
    insights.append(
        "💡 Several questions skipped. That's okay - we'll cover these "
        "thoroughly in your study plan."
    )

# If time pressure detected
if avg_response_time < 30:
    insights.append(
        "💡 You're answering quickly. Taking a moment to organize your "
        "thoughts can improve response quality."
    )
```

## Output Format

**Console Display:**
- Clear visual hierarchy
- Use Unicode box drawing characters
- Color indicators (if supported):
  - 🟢 Green for strengths
  - 🟡 Yellow for moderate
  - 🔴 Red for weaknesses
- Progress bars for visual clarity
- Emoji for quick scanning

**Return to Session:**
- Analysis doesn't interrupt flow
- Candidate can continue immediately
- State preserved

## Edge Cases

**If Called Too Early (< 3 questions):**
```text
📊 Performance Analysis

You've just started! Complete a few more questions for meaningful analysis.

Current progress: {answered}/{total} questions

Keep going! 💪
```

**If Session Complete:**
```text
📊 Final Performance Summary

The interview is complete! Your comprehensive report is being generated.

Use *report to view the full feedback.
```

## Notes for Implementation

**Key Behaviors:**
- Quick to generate (< 1 second)
- Non-disruptive to interview flow
- Provides actionable insights
- Encouraging tone regardless of performance
- Specific, not generic feedback
- Respects candidate's language

**Updates to Session State:**
- No modifications to session data
- Read-only analysis
- No side effects

## Task Completion

Completes after displaying analysis and returning control to interview session.
