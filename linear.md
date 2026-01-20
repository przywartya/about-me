# Writing Good Linear Issues

## The Golden Rule

An engineer reading the ticket should be able to pick it up and complete it from start to finish without asking a single question to the issue author. This takes real effort from the author, but it pays off in reduced interruptions and faster delivery of the team. It also ensures strong documentation from the beginning of the project, shared team knowledge and reduced bus-factor / tribal-knowledge effect.

## Write With Empathy

Before submitting a ticket, read it as if you're the engineer picking it up — not as the person who wrote it with all the context already in your head. It's a mental excercise, but without it, the philosophy does not work.

Ask yourself:

- Does this make sense to someone without my context? You've been thinking about this problem for hours or days. They're seeing it for the first time.
- Would I feel confident starting this? If the ticket would make you hesitate or feel uncertain, it will do the same to others.
- What questions would I ask? If you can anticipate questions, answer them in the ticket before they're asked.
- Is anything assumed but not stated? Decisions that feel obvious to you might not be obvious to someone else.

The goal is to hand someone a ticket that makes them feel prepared and confident, not anxious about hidden complexity or unclear expectations. Ambiguity in a ticket translates directly into stress for the engineer picking it up.

## Required Sections

### 1. Context: Why Do We Need This?

Every ticket must explain why we're making this change. Include:

- **The problem or opportunity** — What's broken, missing, or could be better?
- **The impact** — What happens if we do this? What happens if we don't?
- **The reasoning** — Why this approach over alternatives?

**Why this matters:**

- Historical reference — Future engineers need to understand why something was built
- Prevents accidental removal — Someone might want to delete code without understanding its purpose
- Transparency — Stakeholders can understand the rationale
- Onboarding — New team members can get up to speed faster

### 2. Acceptance Criteria: Definition of Done

The outcome of the ticket must be crystal clear. Write specific, testable criteria.

**Good example:**
> When a tester fills out the screener, they automatically receive an email with a scheduling link that allows them to book an interview with the researcher.

**Bad example:**
> Implement automatic invites.

## Acceptable vs Unacceptable Ambiguity

| Acceptable | Not Acceptable |
|------------|----------------|
| How to implement it (technical approach) | Why we're doing it |
| Specific code structure | What "done" looks like |
| Library/tool choices | The expected outcome |

**The "why" and "acceptance criteria" are not up for debate.** If you're picking up a ticket and these are unclear, push back before starting.

## Handling Uncertainty

If you suspect there's complexity hiding underneath a ticket:

1. **Explore first** — Before coding, investigate and clear out the ambiguity
2. **Update the ticket** — Document your findings for others
3. **Split if needed** — Break into smaller, clearer issues

Don't start implementing when the ticket feels too ambiguous. That leads to wasted "figuring out time" that could span days.

## The Cost of Poor Tickets

When a ticket lacks context and clarity, the engineer picking it up loses time:

- **Day 1:** Getting alignment with stakeholders on what the ticket actually means
- **Day 2:** Exploring technical decisions and options
- **Day 3:** Finally implementing

The issue author already has context loaded up when writing a proejct down. Spending a few hours upfront to clarify the ticket saves the team days of exploration and back-and-forth.

## Keeping Tickets Fresh

- **Remove outdated tickets** — If significant time has passed or dependencies changed, consider deleting and recreating with current context
- **Update before handoff** — If assigning to someone else, review and refresh the description
- **Link related work** — Use Linear's "Related" field to connect research tickets to implementation tasks

## Research Tickets

Research tickets require extra care:

- Always link them to the implementation tasks they inform
- Include clear deliverables (document, decision, prototype)
- Add a note in acceptance criteria: "Update related implementation tickets with findings"
- Consider keeping research separate from project scope to reduce entropy and maintain stability

## Quick Checklist

Before marking a ticket ready for work:

- [ ] "Why" section explains the problem and impact
- [ ] Acceptance criteria are specific and testable
- [ ] Technical direction is provided (not the exact solution, but enough to avoid rabbit holes)
- [ ] Related tickets are linked
- [ ] Any known constraints or decisions are documented
- [ ] A stranger could pick this up without Slack messages
