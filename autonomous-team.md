# How to Stop Being the "Guardian of All Code"

In your journey as an engineering leader — whether you're a tech lead, an engineering manager, or an early-stage founder — you will hit a point where you are reviewing too many PRs and you can't handle it anymore. You've written most of the code. You know the domain, you know the problems, you know the technology. So naturally, you became the go-to code reviewer. All of your teammates tag you, and you're basically the person accountable and responsible for pushing stuff to production.

Your team trusts you. They trust that you will review it thoroughly, find the edge cases, and make sure it's safe to ship. You have to give your permission before anything goes out.

And that's exactly the problem. You've become the guardian of all code, and now you're the bottleneck.

The real question isn't "how do I review PRs faster?" It's: **how do you build a team that is autonomous enough that you are not needed to do code reviews anymore?** How do you give everyone more trust to deploy freely?

## Why You're Stuck

The reason you're stuck is not that your team isn't good enough. It's that you've never given them the space to be good enough.

When you're doing all the code reviews and you're on top of all the issues, every other engineer on the team is thinking: "Ok, this is not my problem. Adam is looking at it. Adam is thinking about it. I don't have to think about it, I don't have to learn the domain, because Adam already knows the domain. So why should I bother?"

You're basically taking away that learning from them. Every edge case you catch is a learning opportunity someone else didn't get. Every pattern you enforce is context someone else didn't build. The deep knowledge you have — about the codebase, the product, the domain — you accumulated it by being in the weeds. Your team needs to be in the weeds too. And right now, you're standing in the way.

## The Solution Sounds Simple (But Isn't)

In principle, it's super simple: you need multiple people on the team who have deep context about the technology, the product, and the domain, and who have the leadership skills to make sure that whatever gets pushed to production is high quality and safe. Basically, you need a few senior engineers who can review other people's PRs and take ownership of what ships.

In practice, it's your job as a leader to make this happen. It doesn't happen on its own.

## Two Tracks for Building Autonomy

I think about this as two parallel tracks for how a team can operate without you in the critical path.

### Track 1: Project-Based Ownership

When you have a project, the [tech lead](https://github.com/przywartya/about-me/blob/main/the-tech-lead.md) of that project should be the person reviewing all the PRs. They're managing the team that's pushing the project forward, they have the deepest context on what's being built, and they're the natural owner of code quality for that body of work. You don't need to be involved. The project lead is accountable.

This is the easier one to set up because projects have natural boundaries and a clear lead. If you've scoped the project well and picked the right lead, they should be fully capable of deciding what's safe to ship.

### Track 2: General Work Without a Single Owner

General issues, maintenance, tech debt, whatever — the stuff that doesn't belong to a specific project. This is where it gets harder, because there's no single obvious reviewer. This work requires broad domain knowledge, and that's exactly why it historically lands on your plate.

For this track, you need multiple senior engineers or engineering leaders on your team who know the domain well enough to provide good code reviews and make ship/no-ship decisions. Not one backup — two or three people who can confidently approve PRs across the codebase.

But here's the catch: to make that happen, you have to give them the space to grow into that role. They need to accumulate context about the domain, about the codebase, about the problems that exist in both. If you're the one doing all the reviews, you're not giving them that space. You're absorbing all the context and all the reps, and they never get the chance to build that muscle.

## What Your Job Actually Looks Like Now

You're not reviewing code anymore. You're building a system where code gets reviewed well without you. Here's what that takes:

**Set the expectation explicitly.** Tell your senior engineers: this is your job now, this is your responsibility. Don't be vague about it. Say it out loud: "Officially, from now on, I will not be conducting all code reviews. We have these two senior engineers on the team, and they will be conducting code reviews on my behalf." The rest of the team needs to hear it too, so they know who to go to and who to trust.

**Step away deliberately.** You have to actually stop being available as the default. If you're still an option, you will remain the option. Remove yourself from the automatic review assignments. Redirect people who tag you. This is uncomfortable, especially when you know you could catch something they might miss. Do it anyway.

**Keep them accountable.** Do random check-ins. Drop in on a review once in a while and see if they're doing a good job. Are they catching edge cases? Are they providing thoughtful feedback? Are they ensuring high-quality code is getting pushed to production? If not, that's a coaching conversation — not a reason to take the reviews back. Your job is to make sure the other leaders on your team are doing a good job.

**Give them room to learn.** They won't be as good as you on day one. They haven't had the reps you've had. But every review they do is a rep they wouldn't have gotten if you were still hoarding all the reviews. The context builds over time, and it builds faster than you think.

## Trust Is Built, Not Granted

You can't just announce "I trust everyone to deploy freely now" and walk away. Trust is something you build by giving people progressively more responsibility and seeing how they handle it. Start with the senior engineers. Let them own reviews. Verify they're doing it well. Then widen the circle.

Over time, you're not the guardian of all code anymore. You're the person who built a team that doesn't need a guardian — because the standards, the context, and the ownership are distributed across the team.

That's what scaling yourself looks like. Not doing more, but making yourself unnecessary.

## But What About the Messy Middle?

If you're reading this and thinking, "Ok, the project-based track makes sense, but what about the rest? The maintenance, the bug fixes, the tech debt — that stuff doesn't have a leader, it doesn't have a clear scope, it just... exists" — then you've identified the biggest struggle.

That unstructured line of work is where things fall apart. There's no project lead, no clear definition of done, no one accountable. It's just a backlog of stuff that everyone knows needs fixing but nobody owns.

Here's the thing though: it doesn't have to stay unstructured. You can take a chunk of that work — say, "clean up this microservice" or "fix the flaky test suite in this domain" — and turn it into a project. Assign a leader. Give them a scope, a team, and a timeline. Now you have someone accountable for the success of that initiative, someone who owns the code reviews for it, someone you can keep accountable.

You're basically taking the same playbook from Track 1 and applying it to work that people usually treat as background noise. You're assigning a leader to a problem.

I'll dig deeper into this in my next post: [Tech Debt as Innovation](./tech-debt-as-innovation.md) — how to stop treating tech debt as a chore and start structuring it as the kind of work that actually moves the product forward.
