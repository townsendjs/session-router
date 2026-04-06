# context-map.md
# Your personal session router map.
# Add one entry per project or recurring context.
# Claude reads this at the start of every session to generate your setup checklist.

---

## How to use this file

Each entry has:
- **Trigger keywords** — words or phrases in your opening message that signal this context
- **Files** — paths to load into context (relative to your vault or project root)
- **Skills** — skill names to enable
- **Connectors** — MCP connectors to enable
- **Disable** — connectors or skills that waste context and should be turned off

You don't need to fill in every field. Leave blank what doesn't apply.

---

## Projects

### [Project Name]

**Trigger keywords:** keyword1, keyword2, keyword3

**Files to load:**
- `path/to/file.md` — brief description of what this contains

**Skills to enable:**
- `skill-name` — what it does in this context

**Connectors to enable:**
- `connector-name` — why it's needed here

**Connectors to disable:**
- `connector-name` — not needed, frees up context

---

### [Project Name]

**Trigger keywords:** keyword1, keyword2

**Files to load:**
- `path/to/file.md` — brief description

**Skills to enable:**
- `skill-name` — brief reason

**Connectors to enable:**
- `connector-name` — brief reason

**Connectors to disable:**
- `connector-name` — brief reason

---

## General / Catch-all

**For sessions that don't match a specific project:**

**Files to load:**
- `path/to/general-reference.md` — always-useful context

**Skills to enable:**
- (list any skills relevant to general work)

**Connectors to enable:**
- (list any connectors relevant to general work)
