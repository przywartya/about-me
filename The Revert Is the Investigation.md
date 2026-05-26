# The Revert Is the Investigation

Every engineering team has the same moment. A spike of customer reports lands in support. Multiple users hitting the same weird symptom. Nobody can reproduce it locally. And the team starts debating: *what's causing this?*

Someone proposes a revert candidate — usually a recent PR that touched the area in question. And then someone else, doing their best impression of a responsible engineer, says: **"Let's confirm root cause first before guessing and reverting."**

This sounds responsible. It is, in fact, almost always wrong.

## The Prior I Operate From

A software system's stability is something like a living organism. Left alone, it stays stable. The vast majority of destabilizations come from something *we* shipped. Our code, our config, our migration, our dependency bump.

So when I see a spike of user reports in a given window, the very first thing I do is open the merge log and look for a PR in that window that touches an area that could plausibly cause the symptom. Not because I'm guessing — but because the probability that the cause is "us, recently" is overwhelmingly higher than "the universe spontaneously decided to break."

This is the prior that makes everything else in this post make sense. If you don't believe it, you'll burn weeks investigating ghosts. If you do believe it, your first move during an incident becomes obvious.

## What "Revert-First" Actually Means

When I say "revert first," I don't mean "skip investigation." **The revert *is* the investigation.** It's the cheapest, fastest, most reversible experiment you can run against reality.

The standard playbook when a PR is timeline-correlated with a customer bug cluster is:

1. **Pick the revert candidate.** Whichever recent merge touches the surface area where the symptom appears.
2. **Identify the signal.** The log line, the error metric, the dashboard tile that fires when this bug happens.
3. **Ship the revert. Watch the signal.**

If the signal drops, you've found the cause without reading a single line of code. If it doesn't drop, you've eliminated a hypothesis in hours instead of days — and you can put the PR back tomorrow with the additional knowledge that the cause is somewhere else.

This is a real A/B test against production reality. No amount of staring at the diff can give you what one revert and a few hours of observation will give you.

## The Trap

The reason teams don't do this is that "let me confirm root cause first" sounds responsible. Of course we should understand the bug before we act. Of course we shouldn't just throw away code without evidence.

But here's the math that nobody runs:

| | Investigation-first | Revert-first |
|--|--|--|
| Time to an answer | Hours to days | Minutes to hours |
| Requires the right person staring at the diff | Yes | No |
| Often inconclusive | Yes | Rarely |
| Reversible | N/A | Yes — re-apply tomorrow |
| Cost while you wait | More users hit the bug | Whatever you lose by temporarily not shipping the feature |

While we debate mechanisms in Slack, customers keep bleeding. Thirteen reports in five days means every hour we sit on a hypothesis is more reports. The clock is wildly asymmetric and almost nobody factors that into the call.

## Don't Re-Merge Just Because the Revert Didn't "Fix" It

Here's the move that takes longer to learn: even if the reports don't drop after you revert, **the default is to keep the PR reverted**. Not "well, we ruled it out, ship it back." Re-revert it if it sneaks back in.

The logic is simple: the burden of proof is on the change, not on the revert. A revert is the conservative position. A merge is the aggressive position. Until you actually understand what changed and why it was safe, the prior still says "the system was stable before this and we don't yet know why it isn't now." Keep it out until someone has earned the right to put it back.

This feels harsh on the PR author. It isn't. It's how you draw a clean line between "we proved it was safe" and "we got tired of debating it."

## The Shitty Version of This Playbook

The standard playbook assumes step 2 actually works — that you have a log or a metric the bug throws. Sometimes you don't.

A recent incident on my team was a fabricated-state bug: the agent would tell users it had written a file, and the file wouldn't actually land. No exception. No failed S3 put. No socket error. Nothing in the logs even hinted at the failure. The only signal we had was *"customer reports stop coming in."*

That is the shitty version of the playbook. Slow signal. Noisy signal. Humiliating to depend on. But it's still a signal, and the asymmetry still holds: revert costs minutes and is reversible, waiting on a diff-reading marathon costs days while more users get hit.

When you're stuck in the shitty version, you do it anyway. You revert, you wait two or three days, and you watch the support channel. If the reports drop, you've still proven something. You just had to ask nature for the answer instead of asking Grafana.

## The Real Long-Term Lesson Is About Observability

Here's the part that matters more than any individual revert call: **you should never be in a state where customer reports are your primary signal for a regression.**

Every class of user-visible failure should have a log, a metric, or a dashboard tile that fires when it happens. So that step 2 of the playbook is always available. So that you can revert, refresh a chart, and know within minutes — not days — whether it worked.

If you find yourself depending on support ticket volume as your incident signal, that's a leading indicator of a different problem: your observability has fallen behind your product surface area. Fix that. Fix it before the next incident, not during the one after.

The shitty version of the playbook is sometimes unavoidable in the short term — sandboxed environments are notoriously hard to instrument, AI agent behavior is notoriously hard to log. But you should be actively trying to leave that state, not normalizing it.

## Two Modes of Engineering

The real disagreement under "should we revert first?" is usually a disagreement about which mode the team is in.

**Normal-time engineering**: confirm before acting. Understand the system. Make a careful change. Review carefully. This is the default, and it's correct most of the time.

**Active-incident engineering**: act on the cheapest reversible test. Let reality narrow the search space. Investigate after the bleeding stops, not during.

The mistake teams make is staying in normal-time engineering when they should be in active-incident engineering. The reverse mistake — running incidents constantly when nothing is actually broken — is rare. Almost everyone errs on the side of being too careful when users are already bleeding.

The signal to switch modes is usually obvious in hindsight: a real spike in reports, multiple customers hitting the same symptom, a fresh deploy in the same window. If you have all three, you're in active-incident mode. Act like it.

## The Move

If you take nothing else from this post: **when a PR is timeline-correlated with a customer bug cluster, your first move is to revert it.**

Not to call a meeting. Not to assign an investigation. Not to ask the author to "take a look." Revert it. Watch what happens. Then decide what to do next.

The cost of being wrong about the revert is approximately zero — you re-merge tomorrow with a fix. The cost of being right about it and having waited three days to test the theory is thirty more affected users, an exhausted on-call rotation, and a team that quietly learns to tolerate active incidents instead of resolving them.

Software systems are stable when left alone. Almost every fire was lit by something we shipped. Treat new commits as the prime suspect, not the trusted default.

**Revert first. Investigate second. Re-merge last — and only when you actually know why it's safe.**

---

*Related reading:*
- *[The Forest Ranger: How to Protect Your Team's Focus](https://github.com/przywartya/about-me/blob/main/The%20Forest%20Ranger%3A%20How%20to%20Protect%20Your%20Team's%20Focus.md) — on absorbing operational noise so product work can continue*
- *[Every Day You Don't Act, You're Choosing to Live With the Problem](https://github.com/przywartya/about-me/blob/main/Your%20Team%20Already%20Knows%20You're%20Avoiding%20the%20Conversation.md) — on the cost of inaction*
