# V.U.E, AI Failure Monsters & the AI Skill Preservation Checklist

This document captures the core ideas from the talk:

> **How Not to Lose Developer Skills in the Age of AI**

Use it as a reference, a discussion starter with your team, or a thing you shamelessly copy into your internal wiki.

---

## 1. The thesis

> **AI won’t replace developers.  
> AI will replace developers who stop thinking.**

AI compresses the value of *typing*.  
It does **not** compress the value of *deciding*.

That means:
- Code is cheaper to produce.
- Good questions, judgment, and taste become more valuable.

---

## 2. V.U.E — Your AI Shipping Rule

**V.U.E** is a tiny ritual you can run before you ship AI-assisted work:

> **We ship AI output only after it is:**  
> **V**erified • **U**nderstood • **E**xplainable

### 2.1. Verified

**Question:** Did I verify it?

Examples:
- Do tests pass — and cover the interesting edge cases?
- Does this API / method / flag actually exist in docs or code?
- Did I run at least one real call / spike against the system?

**If the only reason you trust it is “the model seemed confident,” it’s not verified.**

---

### 2.2. Understood

**Question:** Do I understand it?

Examples:
- Could I debug this at 2 a.m. without asking the model what it did?
- Do I understand the data flow and the likely failure modes?
- Do I know why this approach was chosen, not just that it “works”?

If you treat the model’s output as a magic spell, you don’t actually own the solution — you’re renting it.

---

### 2.3. Explainable

**Question:** Can I explain it?

Examples:
- Can I explain this to a teammate in 2–3 minutes?
- Can I justify why this design is a good trade-off for *our* system and *our* users?
- Would a future engineer reading this be able to reason about it?

Explainability is where understanding and verification meet.  
If you can’t explain it, you probably haven’t really verified or understood it.

---

## 3. The 4 AI Failure Monsters

Naming failure modes makes them easier to spot and easier to talk about in code review.

### 3.1. The Confident Liar

> *Hallucination with perfect posture.*

- Makes things up: APIs, flags, functions, even entire libraries.
- Sounds right, feels right… isn’t real.
- Very dangerous when you’re tired or under time pressure.

**Counter-move:**  
- Always verify against external reality: docs, tests, real environments.  
- Treat the model’s output as a **proposal**, not a fact.

---

### 3.2. The Overfit Intern

> *Great on common patterns, brittle off-road.*

- Does amazingly well on patterns that look like its training data.  
- Falls apart on unusual constraints, legacy weirdness, internal abstractions.
- “It worked great on the example, but not in *our* system.”

**Counter-move:**  
- Add rich context in your prompts (domain, constraints, tech stack).  
- Ask for multiple options + trade-offs, not a single “best” answer.  
- Expect to adjust more for anything that’s unique to your environment.

---

### 3.3. The Productivity Mirage

> *Fast output, slow learning.*

- You ship a lot of code quickly.  
- You feel productive.  
- But your ability to reason and debug erodes because you’re not doing the reps.

**Counter-move:**  
- Use **Manual Mode** deliberately (see below).  
- Treat AI like an **open-book exam** — try first, then ask.  
- Measure learning, not just throughput.

---

### 3.4. The Silent Security Leak

> *Capability + access without guardrails.*

- Models happily read whatever they can see: `.env` files, logs, database dumps.  
- If you pipe too much sensitive context into them, you increase blast radius.  
- Sometimes the “bug” is basically: *“We let the wrong thing read the wrong file.”*

**Counter-move:**  
- Least privilege: give tools only the access they truly need.  
- Redact secrets before sending context to external systems.  
- Log and audit what assistants/agents can see and do.

---

## 4. Manual Mode = Mental Gym

AI is great. Your brain still needs reps.

If you outsource **all** of the thinking and writing to the model, you lose the “muscle memory” that makes you valuable when things go off the rails.

### 4.1. Manual Mode rules of thumb

Use these as a simple policy:

- **New domain or concept?**  
  You write the first draft yourself.  
  (Use AI later to refactor, critique, add tests, or explore alternatives.)

- **Refactoring, boilerplate, repetitive glue?**  
  AI is perfect for this — let it help.

- **You can’t explain the code clearly?**  
  Don’t merge it.  
  If you can’t explain it, you don’t really own it.

---

## 5. The AI Skill Preservation Checklist

Try this as a **2-week experiment** with yourself or your team:

1. **10 minutes manual attempt before prompting**  
   - Even a short struggle before asking AI increases learning dramatically.

2. **Write intent + constraints first**  
   - “Here is what I’m trying to do, these are the constraints, this is success.”  
   - Then let AI help with the implementation.

3. **Ask for options, not just answers**  
   - Prompt like:  
     > “Give me 3 approaches, their trade-offs, and what can go wrong with each.”  
   - This uses AI to widen your thinking, not just auto-complete.

4. **Ship only if it passes V.U.E.**  
   - Verified. Understood. Explainable.  
   - If any of these is “no”, you’re not done yet.

5. **One “no-AI reps” session per week**  
   - Pick a small task: debugging, a kata, a design sketch.  
   - Do it fully manual.  
   - The point is not to suffer — it’s to keep the thinking muscle alive.

---

## 6. How to use this with your team

A few simple ways to introduce this without a giant process change:

- Add V.U.E as a **section in your PR template**  
- Use the **Failure Monsters** language in code review and incident post-mortems  
- Run a short **“no-AI reps” lunch session** once a week or once a sprint  
- Create a simple internal page with this file and a few of your own examples

---

If you adopt any of this, I’d love to hear how it went — especially any new “monsters” you’ve discovered in the wild.  
You can reach me at `pavlo.babenko@gmail.com` or on LinkedIn: `https://www.linkedin.com/in/pavlobabenko`.

**Typing is cheap. Judgment is premium.**
