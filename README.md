# session-router

A Claude skill that automatically intercepts the start of every new session, reads your project context map, and generates a tailored checklist of files, skills, and MCP connectors to enable or disable before you begin.

Built by [Jeff Hnilicka](https://github.com/yourusername). Contributions welcome.

---

## What it does

Most Claude sessions start cold — you type your first message and Claude has no idea what project you're in, what files are relevant, or which connectors you need on. This skill fixes that.

On every new session:

1. Claude reads your opening message
2. If it's clear enough, it immediately generates a setup checklist
3. If not, it asks a focused question or two
4. The checklist tells you exactly which skills to enable, which MCP connectors to turn on, and which ones to turn off to free up context
5. You say "ready" and the real session begins

At any point mid-session, run `/session-router check` to get a quick adjustment checklist — things that have become deadweight since the start, and things that would help given where the session has actually gone.

---

## Why this matters

Claude's context window isn't free. Every MCP connector you have enabled — even idle ones — registers its tool definitions on every single message. A few connectors you're not using can silently consume 10–20% of your context before you've typed a word.

This skill makes context management a first-class habit instead of an afterthought.

---

## Installation

1. Download `session-router.skill` from [Releases](../../releases)
2. In Claude Desktop or Claude.ai, go to **Settings → Skills**
3. Install the `.skill` file
4. Copy `references/context-map-template.md` and fill it in with your own projects
5. Save your filled-in version as `context-map.md` in the same skill directory — or reference it by path in the skill

---

## Setup: Your Context Map

The skill reads a file called `context-map.md` that you configure. This is where you list:

- Your projects and trigger keywords
- Which files to load for each project
- Which skills to enable
- Which MCP connectors to turn on or off

A blank template is at `references/context-map-template.md`.
A fully worked example (based on a real creative/academic workflow) is at `references/example-context-map.md`.

---

## Toggle Options

You can control skill behavior with HTML comments inside `SKILL.md`:

| Toggle | Default | Effect |
|--------|---------|--------|
| `AUTORUN` | `true` | Set to `false` to disable autorun — skill only fires when you call `/session-router` |
| `SHOW_DISABLE_SUGGESTIONS` | `true` | Set to `false` to hide the "consider disabling" section |
| `REQUIRE_CONFIRMATION` | `true` | Set to `false` to skip the "ready" confirmation step and proceed immediately |
| `ALWAYS_ASK` | `false` | Set to `true` to always ask clarifying questions even with clear signal |

Example — disable autorun:
```html
<!-- AUTORUN: false -->
```

With autorun off, invoke manually:
```
/session-router
/session-router MythTech writing session
```

---

## Compatibility

- Claude.ai (web and desktop)
- Claude Code
- Cowork

Requires at least one skill or MCP connector configured to be useful.

---

## Contributing

This is a community skill. If you improve the routing logic, add support for new connector types, or build a better context-map schema, open a PR.

If you share your own `context-map.md` as an example for your workflow (developer, researcher, educator, designer, etc.), that's especially valuable — add it to `references/examples/`.

---

## License

MIT
