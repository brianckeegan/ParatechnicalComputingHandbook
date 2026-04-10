# 26  Collaboration Mechanics

> **TIP:**
>
> **Prerequisites (read first if unfamiliar):** [sec-git-github](#sec-git-github).
>
> **See also:** [sec-project-management](#sec-project-management), [sec-documentation](#sec-documentation), [sec-asking-questions](#sec-asking-questions).

## Purpose

Collaboration is not a vague soft skill. It is a set of repeatable mechanics that make work legible, reviewable, and safe to change. In computing and data science, effective collaboration relies on shared artifacts (docs, issues, pull requests), disciplined communication (clear requests and responses), and predictable workflows (review, merge, release). This chapter teaches novice-friendly practices for working with other people without creating confusion, duplication, or fragile “tribal knowledge.”

## Learning objectives

By the end of this chapter, you should be able to:

1.  Explain why collaboration depends on shared artifacts (docs, issues, PRs) rather than private messages.

2.  Write project documentation that supports onboarding and reproduction.

3.  Participate in code review as an author and reviewer using a respectful, actionable style.

4.  Use comment threads to clarify intent, document decisions, and close the loop.

5.  Propose and follow a lightweight workflow for tasks, reviews, and merges.

6.  Maintain collaboration hygiene: small changes, clear ownership, explicit decisions, and visible status.

## Running theme: make work visible, small, and easy to review

If teammates can understand what changed, why it changed, and how to verify it, collaboration scales.

## 26.1 A beginner mental model: collaboration surfaces

Effective collaboration on a software or data-science project happens across several distinct **surfaces**, and a healthy team uses each one for what it is good at. The **repository** holds the code, notebooks, and documentation — it is the canonical source of what the project actually *is*. **Issues** are where tasks, bugs, questions, and decision records live — anything that needs to be tracked over time but is not itself code. **Pull requests** are where proposed changes get reviewed and discussed before they become part of the repository. **Code review comments** are tied to specific lines of a diff and capture the back-and-forth that produced the merged version. **Project boards or milestones** show the overall status: what is in progress, what is blocked, what is done. And **chat and meetings** are the lightweight coordination layer — useful for unblocking each other quickly, but explicitly *not* the system of record. If a decision happens in chat, write it down somewhere persistent before the conversation scrolls off.

The **core collaboration loop** that ties these surfaces together is short and repeatable: plan in issues → implement on a branch → open a PR → review and comment → revise → merge → document the outcome → repeat. Every healthy collaborative project works some variant of this loop, and the rituals you build around it (PR templates, review checklists, definition of done) all exist to make the loop itself reliable.

Three roles show up in almost every collaboration. The **author** proposes a change, provides the context a reviewer needs to evaluate it, and responds to feedback. The **reviewer** protects quality, asks clarifying questions when intent is unclear, and mentors less-experienced authors through the process. The **maintainer** or **lead** sets the policies (which branches are protected, which merge strategy is used, who can approve), arbitrates decisions when reviewers disagree, and makes sure things actually get followed through to completion. On a small student project, one person may play all three roles at different times; on a larger team, they are usually different people.

## 26.2 Documentation as collaboration infrastructure

### What documentation is for (student framing)

- Onboarding: a new collaborator can start quickly.

- Reproducibility: a collaborator can rerun results.

- Decision trace: why key choices were made.

- Operations: how to build/run/test.

### Minimum viable documentation set

- `README.md`: purpose, setup, how to run, outputs.

- `CONTRIBUTING.md`: how to contribute, style rules, review expectations.

- `CODE_OF_CONDUCT.md` (when appropriate): norms and escalation.

- `DECISIONS.md` (or ADRs): consequential decisions and rationale.

- Data dictionary / codebook: dataset meaning and transformations.

### Writing for your audience

- Assume the reader is competent but unfamiliar with your local context.

- Put the most common tasks first.

- Provide “copy/paste to run” commands and expected outputs.

### Documentation upkeep: avoid staleness

- Update docs in the same PR as code changes.

- Treat docs as part of the definition of done.

- If documentation is missing, file an issue.

## 26.3 Work planning mechanics: issues and task decomposition

### Why issues beat chat threads

- Searchable, linkable, and persistent.

- Establishes a shared memory.

- Supports prioritization and assignment.

### Anatomy of a good issue

- Clear title: verb + object.

- Context: why it matters.

- Definition of done.

- Evidence: links, examples, errors.

- Labels: type (bug/task/question), priority, area (data/code/docs).

### Decomposition patterns (novice-friendly)

- Split by artifact: data ingestion, cleaning, analysis, visualization, report.

- Split by risk: do uncertain tasks early.

- Split by reviewability: tasks that fit in a small PR.

## 26.4 Code review fundamentals (what it is and why it works)

### Goals of review

Code review has four jobs running at once. The most obvious is to improve **correctness, readability, and maintainability** — to catch the bug, the unclear name, the function that is doing too much. The second is to **catch edge cases** the author may not have considered, since fresh eyes see the empty list, the missing key, the off-by-one. The third is to **transfer knowledge across the team**: the reviewer learns what the author has been working on, the author learns what the reviewer cares about, and the project’s collective understanding grows with every PR. The fourth is to **align changes with project standards** — the conventions, the architecture, the things “we always do this way” — so that the codebase stays coherent over time.

### What review is not

Equally important is what review is *not*. It is **not a personal critique**: the comments are about the code, not the author. It is **not a substitute for verification**: a reviewer cannot manually run every code path, and “two reviewers approved” does not mean “the code works.” Running the change is how you know it works. And it is **not a place to redesign the whole system in one comment** — if the PR’s approach is fundamentally wrong, that conversation belongs in an issue *before* the code is written, not buried in line-by-line comments after.

### Review checklists (student baseline)

When you sit down to review a PR, walk through six questions in roughly this order. **Correctness and clarity:** does the code actually do what its description says it does, and is the intent obvious? **Verification steps:** how does the author know it works? Did they include a clear “how to test” section in the PR description, with commands a reviewer can run? **Reproducibility:** could someone else clone the repo and run the change end to end? **Documentation:** are the README, docstrings, and inline comments updated to match the new behavior? **Data impacts:** if the change touches data — new schema, renamed columns, new file paths, new assumptions — are those changes documented? **Security and privacy:** are there any new secrets accidentally committed, any new ways for sensitive data to leak, any commands that need elevated privileges?

Most PRs only need one or two of those checks to be substantive — but knowing the full list keeps you from missing the kind of issue that is easy to spot if you remember to look.

## 26.5 Authoring reviewable changes

### Small PR discipline

- One purpose per PR.

- Avoid mixing refactors with new features.

- Keep diffs readable: remove dead code separately.

### PR descriptions that help reviewers

- Summary: what changed.

- Motivation: why.

- How to test: steps and expected outputs.

- Screenshots/figures (if relevant).

- Links: related issues, background docs.

### Pre-review self-check

- Re-read your own diff.

- Run a smoke test.

- Confirm docs updated.

- Ensure no secrets or large accidental files are included.

## 26.6 Reviewing and commenting mechanics

### Comment taxonomy (so feedback is legible)

Blocker  
Must fix before merge (correctness, security, reproducibility).

Suggestion  
Improvement that is optional.

Question  
Clarification needed to evaluate.

Nit  
Minor style/detail; non-blocking.

### Writing effective comments

- Be specific: point to a line and explain the issue.

- Provide rationale: tie to a goal (correctness, clarity, consistency).

- Offer a concrete suggestion when possible.

- Prefer questions when intent is unclear (see [sec-asking-questions](#sec-asking-questions) for how to frame a well-structured technical question).

### Tone and collaboration hygiene

- Assume good intent.

- Critique the code, not the person.

- Use neutral language and avoid sarcasm.

- Acknowledge good work and improvements.

### Thread management

- One issue per thread.

- Resolve threads when addressed.

- Summarize decisions in the PR description or decision log when important.

### Responding to reviews as an author

- Reply to each thread: explain what you changed or why you disagree.

- If you disagree, propose an alternative and ask for alignment.

- Avoid “drive-by” changes that introduce new behavior without explanation.

## 26.7 Merging, ownership, and handoffs

### Definition of done (team agreement)

- Review approvals obtained.

- Tests and smoke checks pass.

- Documentation updated.

- Issue linked and closed with a summary.

### Handoff notes

- If someone else will continue the work, leave a short status note.

- Identify next steps and open questions.

## 26.8 Collaboration practices for data science artifacts

### Notebooks and noisy diffs

- Keep notebooks tidy: avoid huge outputs.

- Clear unnecessary output before merging.

- Prefer “notebook as narrative, code in `src/`”.

### Data and model artifacts

- Avoid committing large raw datasets unless policy says otherwise.

- Document data retrieval and transformations.

- Store outputs deterministically and link from reports.

### Reproducibility check as a collaboration contract

- Another collaborator should be able to recreate the environment and rerun.

- Include a minimal “how to reproduce” section in the PR.

## 26.9 Cadences and rituals (lightweight, student-friendly)

### Weekly planning

- Review open issues, reprioritize, assign.

- Identify blockers and dependencies.

### Daily/async updates

- Short status: what I did, what I will do, what is blocking me.

- Post updates in issues/PRs when they affect others.

### Retrospectives (optional)

- What went well, what was painful, what to change next time.

- Convert pain points into issues and documentation improvements.

## 26.10 Common failure modes and fixes

### Work hidden in private messages

- Fix: move decisions into issues/PRs; link evidence.

### Mega-PRs that no one can review

- Fix: split into smaller PRs; stage refactors separately.

### Review ping-pong and stalled progress

- Fix: clarify blockers vs suggestions; propose a decision; time-box debates.

### Unclear ownership

- Fix: assign issues; define a driver for each milestone.

### Documentation drift

- Fix: require doc updates in PR checklist; treat missing docs as a bug.

## 26.11 Worked examples (outline)

### Turn a chat question into a good issue

- Convert vague request into context + definition of done.

### Author a reviewable PR

- Create a small branch, open PR with testing steps, request review.

### Perform a constructive code review

- Use the comment taxonomy; request one blocker and one suggestion.

### Close the loop after merge

- Update docs, close issue with summary, tag next steps.

## 26.12 Templates

### Template A: PR checklist

    ## PR Checklist

    * [ ] Linked issue(s)
    * [ ] Summary and motivation included
    * [ ] How to test included
    * [ ] Docs updated (README/notes)
    * [ ] No secrets or large accidental files
    * [ ] Smoke test run

### Template B: Review comment format

    Type: Blocker / Suggestion / Question / Nit
    What I see:
    Why it matters:
    Suggested change:

### Template C: Decision record (lightweight)

    Decision:
    Date:
    Context:
    Options considered:
    Chosen option:
    Rationale:
    Consequences:

### Template D: CONTRIBUTING basics

    * How to set up environment
    * Branch naming and PR policy
    * Review expectations
    * Style/testing expectations
    * Where to ask questions

## 26.13 Exercises

1.  Write a README for a small class project that a classmate can run.

2.  Turn three vague tasks into well-scoped issues with a definition of done.

3.  Open a PR with a strong description and testing steps.

4.  Review a peer’s PR using the taxonomy; request one change and one clarification.

5.  Close an issue by summarizing what changed, what remains, and how to reproduce.

## 26.14 One-page checklist

- Work is tracked in issues/PRs, not only chat.

- Documentation exists and is updated with code changes.

- PRs are small and include “how to test”.

- Reviews are respectful, actionable, and categorized.

- Decisions are recorded and threads are resolved.

- After merge, issues are closed with a clear summary and links.

## 26.15 Quick reference: collaboration norms

- Prefer artifacts over memory.

- Prefer clarity over speed.

- Prefer small, reversible changes.

- Ask questions early; document decisions.
