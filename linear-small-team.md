# Writing Linear Issues

## The Point

Write tickets so people don't interrupt you with questions.

If someone can pick up your ticket and finish it without Slacking you, you wrote a good ticket. If they need to "figure out what you meant" for a day before starting, you wrote a bad ticket — and you'll pay for it in context-switching when they come asking.

## The Mental Exercise

Before submitting, read your ticket as if you're seeing it for the first time. You've been thinking about this problem for hours. They're seeing it cold.

Ask yourself: *Would I feel confident starting this, or would I immediately have questions?*

If you'd have questions, answer them yourself upfront in the ticket.

## When to Skip This

If you're writing a ticket for yourself, or you can explain it in 30 seconds on a call, don't overthink it. This matters when handing work to someone who doesn't have your context.

## What Makes a Good Ticket

Three things:

1. **Why** — What's the problem? What happens if we do/don't fix it?
2. **What "done" looks like** — Specific, testable acceptance criteria
3. **Enough direction to avoid rabbit holes** — Not the exact solution, but the general approach

The "why" and "done" are not up for debate. The "how" can be flexible.

---

## Example: Bad vs Good

### ❌ Bad Ticket

**Title:** Add OAuth flow integration for RevenueCat

**Description:**
- oauth flow for revenuecat https://www.revenuecat.com/docs/projects/oauth-setup

*This ticket is doable, but the engineer has to spend time figuring out: What endpoints do we need? Where do tokens go? What's the redirect flow? What counts as "done"? They'll either guess wrong or Slack you.*

---

### ✅ Good Ticket

**Title:** Add RevenueCat OAuth Flow

**Context: Why Do We Need This?**

We're building a RevenueCat integration that will allow users to connect their RevenueCat account to their project. Before we can build features like project selection or SDK key retrieval, we need a secure way for users to authenticate.

OAuth with PKCE is RevenueCat's recommended method — it's secure, standard, and users can revoke access anytime.

**Technical Approach**

1. **Login endpoint** (`/api/revenuecat/login`): Generate PKCE code_verifier, store in Modal Dict, redirect to RevenueCat
2. **Callback endpoint** (`/api/revenuecat/callback`): Exchange code for tokens, store in database, redirect user back
3. **Token storage**: Store access_token and refresh_token in `project_credentials` table
4. **Token refresh**: Access tokens expire in 1 hour, refresh before API calls

**Acceptance Criteria**

- [ ] User can initiate OAuth via `/api/revenuecat/login?project_id={id}`
- [ ] After success, tokens stored in `project_credentials`
- [ ] User redirected to `/project/{id}?revenuecat_connected=true`
- [ ] `/api/revenuecat/status/{id}` returns connection state
- [ ] `/api/revenuecat/disconnect/{id}` clears tokens
- [ ] Token refresh works when access token expired

**Files to Create/Modify**

- `modal-backend/routers/revenuecat.py` (new)
- `modal-backend/migrations/add_revenuecat_columns.sql` (new)
- `next-frontend/src/app/api/revenuecat/login/route.ts` (new)
- `next-frontend/src/app/api/revenuecat/callback/route.ts` (new)

---

## The Shortcut

If writing all that feels like overkill for a small task, at minimum include:

1. One sentence on **why**
2. A few bullet points on **what done looks like**

That's enough for most things.
