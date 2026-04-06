---
name: session-router
description: Automatically intercepts the start of every new session to assess what the user is working on, then generates a tailored checklist of context files, skills, and MCP connectors to enable or disable before proceeding. Use this skill at the beginning of every conversation before giving any substantive response. Triggers on any opening message — even a greeting or a vague topic mention — and outputs a structured session setup checklist. If the user's intent is unclear, ask focused clarifying questions first. Never skip this step at session start unless the AUTORUN toggle in the body of this file is set to false, in which case only run when the user explicitly invokes /session-router. Also handles mid-session context checks when the user invokes /session-router check.
---

# Session Router

A session management skill with two modes: **session start** routing that generates a setup checklist before work begins, and **mid-session checks** that recommend adding or dropping context as the session evolves.

---

## Mode 1 — Session Start

**Always run at session start, before any substantive response.**

1. Read the user's first message
2. Check if intent is clear enough to map to a context (see: Confidence Threshold)
3. If yes → generate the Session Checklist
4. If no → ask the minimum questions needed, then generate the checklist
5. Wait for user to confirm readiness
6. Proceed with the session

### Step 1 — Read the Context Map

Before generating any checklist, read the user's context map:

```
context-map.md
```

This file lives alongside SKILL.md and defines the user's projects, associated files, skills, and connectors. If this file is missing or empty, tell the user:

> "I don't have a context map set up yet. Would you like me to help you create one? It only takes a few minutes and makes every future session faster."

Then offer to build it interactively using the template in `references/context-map-template.md`.

---

### Step 2 — Confidence Threshold

Assess whether the opening message gives enough signal to route confidently.

**Sufficient signal:** project name, topic area, file mention, task type, or any phrase that maps clearly to an entry in the context map.

**Insufficient signal:** pure greetings ("hey"), ambiguous topics ("I need help with something"), or topics that could span multiple projects.

If signal is **insufficient**, ask up to 3 focused questions — no more. Example:

> "Before I pull up the right tools and files, can you tell me:
> - What project or topic are we working on today?
> - Are you writing, building, researching, or something else?"

Do not ask questions the opening message already answers.

---

### Step 3 — Generate the Session Checklist

Once you have enough signal, output the checklist in this format:

---

**Session Setup — [Project/Topic Name]**

**Enable these skills:**
- [ ] `skill-name` — reason it's relevant

**Enable these MCP connectors:**
- [ ] `connector-name` — reason it's relevant

**Load these files into context:**
- [ ] `path/to/file.md` — what it contains and why

<!-- SHOW_DISABLE_SUGGESTIONS: set to false to hide this section -->
**Consider disabling (not needed this session):**
- [ ] `connector-name` — why it's not relevant and frees up context

**When you're set up, just say "ready" and we'll begin.**

---

### Step 4 — Wait for Confirmation

After delivering the checklist, stop. Do not begin the actual work until the user signals readiness. Accepted signals include: "ready", "done", "go", "let's go", "ok", "all set", or any equivalent.

When confirmed, acknowledge briefly and proceed:

> "Got it — let's go."

---

## Mode 2 — Mid-Session Check

Triggered when the user types `/session-router check` at any point during an active session.

Scan the conversation so far and compare what was loaded at the start against how the session has actually developed. Then output a concise adjustment checklist.

### What to look for

**Deadweight — loaded but unused:**
- A connector was enabled at the start but hasn't been relevant to any message
- A file was loaded for context that hasn't been referenced or needed
- A skill was enabled for a task that didn't materialize

**Gaps — needed but not loaded:**
- The conversation has drifted into a topic, task type, or project not covered by the initial routing
- A file, skill, or connector from the context map would clearly help with where things have gone
- The user has mentioned something (a tool, a file, a project) that maps to an unloaded context

### Mid-Session Check Output Format

---

**Session Check**

**You can probably turn these off (freeing up context):**
- [ ] `connector-name` — hasn't come up, not likely needed

**Consider adding these:**
- [ ] `skill-name` — would help with [what's emerged in the session]
- [ ] `path/to/file.md` — relevant to [current direction]

*No changes needed? Just ignore this and keep going.*

---

Keep the check output short. If nothing meaningful has changed, say so in one line and move on. Don't manufacture suggestions.

---

## Toggle Options

The following behaviors can be controlled with HTML comments in this SKILL.md file. Set the value after the colon to enable or disable.

```
<!-- AUTORUN: true -->
```
Default: `true`. When `true`, the skill runs automatically at the start of every session before any substantive response. Set to `false` to disable autorun — the skill will only activate when explicitly called with `/session-router`. Useful if you prefer manual control or only want routing for certain sessions.

```
<!-- SHOW_DISABLE_SUGGESTIONS: true -->
```
Default: `true`. When `true`, the session start checklist includes a "consider disabling" section. Set to `false` to hide it.

```
<!-- REQUIRE_CONFIRMATION: true -->
```
Default: `true`. When `true`, the skill waits for the user to say "ready" before proceeding after the session start checklist. Set to `false` to skip the confirmation gate and proceed immediately.

```
<!-- ALWAYS_ASK: false -->
```
Default: `false`. Set to `true` to always ask clarifying questions at session start even when signal is sufficient. Useful during initial setup when your context map is new.

---

## Manual Invocation

If `AUTORUN` is set to `false`, the skill runs only when the user types `/session-router` or a natural equivalent like "run session router" or "set up my session".

Manual invocation with a topic hint is also supported:

```
/session-router [topic or project name]
```

Treat any text after `/session-router` as the opening message signal and route accordingly.

To trigger a mid-session check at any time:

```
/session-router check
```

---

## Tone Guidelines

- Be direct and efficient. This is infrastructure, not conversation.
- Don't over-explain the checklist. The user knows what it's for.
- If a context maps to something unexpected, briefly say why.
- Keep all output scannable — one line per item maximum.
- Mid-session checks should feel lightweight. If there's nothing to flag, say nothing or say it in a single sentence.

---

## Reference Files

- `references/context-map-template.md` — Blank template for users setting up their own context map
- `references/example-context-map.md` — Fully worked example based on a real creative/academic workflow
