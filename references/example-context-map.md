# context-map.md — Example
# This is a fully worked example based on a real creative/academic workflow.
# Replace all entries with your own projects, files, skills, and connectors.
# See context-map-template.md for a blank version.

---

## Projects

### Long-form Writing (Academic / Essay)

**Trigger keywords:** paper, essay, writing, theory, draft, argument, research, bibliography

**Files to load:**
- `CLAUDE.md` — running notes on projects, voice guidelines, and session history
- `.claude/brand-voice-guidelines.md` — writing style and voice rules for academic register
- `Writing/active-draft.md` — current working draft

**Skills to enable:**
- `obsidian-cli` — reading and writing vault notes
- `obsidian-markdown` — Obsidian-flavored formatting for new notes
- `avoid-ai-writing` — enforce voice when drafting

**Connectors to enable:**
- `obsidian` — vault access for reading and writing notes

**Connectors to disable:**
- `gmail` — not needed, wastes context
- `google-calendar` — not needed, wastes context
- `figma` — not needed for writing sessions

---

### App Development

**Trigger keywords:** app, code, build, component, bug, Swift, React, frontend, backend, fix

**Files to load:**
- `CLAUDE.md` — project history and active notes

**Skills to enable:**
- `react-best-practices` — if working on frontend components
- `react-native-skills` — if working on mobile/native features
- `frontend-design` — if working from Figma designs

**Connectors to enable:**
- `figma` — design-to-code pipeline

**Connectors to disable:**
- `gmail` — not needed
- `google-calendar` — not needed
- `obsidian` — not needed for code sessions

---

### Teaching / Course Development

**Trigger keywords:** course, students, assignment, lecture, syllabus, lesson, curriculum, class

**Files to load:**
- `Courses/active-course.md` — lecture arc, theoretical throughline, assignment structures
- `CLAUDE.md` — session context

**Skills to enable:**
- `obsidian-cli` — reading and updating course notes
- `doc-coauthoring` — for building structured assignment docs or lecture PDFs

**Connectors to enable:**
- `obsidian` — vault access

**Connectors to disable:**
- `figma` — not needed
- `gmail` — not needed for planning sessions (enable separately if emailing students)

---

### Creative / Film / Visual Project

**Trigger keywords:** video, film, project, character, visual, script, storyboard, edit, footage

**Files to load:**
- `CLAUDE.md` — project notes
- `Projects/active-project/` — world-building, character notes, and references

**Skills to enable:**
- `obsidian-cli` — reading and updating project notes
- `frontend-design` — if working on any visual/mockup elements

**Connectors to enable:**
- `obsidian` — vault access

**Connectors to disable:**
- `gmail` — not needed
- `google-calendar` — not needed

---

### Research / Reference Building

**Trigger keywords:** research, reference, archive, mood board, aesthetic, visual reference, collect, gather

**Files to load:**
- `Research/` — existing archive notes
- `CLAUDE.md` — context

**Skills to enable:**
- `obsidian-cli` — reading and writing archive entries
- `obsidian-markdown` — proper Obsidian formatting

**Connectors to enable:**
- `obsidian` — vault access

**Connectors to disable:**
- `figma` — not needed
- `gmail` — not needed

---

## General / Catch-all

**For sessions that don't clearly match a project above:**

**Files to load:**
- `CLAUDE.md` — always load this

**Skills to enable:**
- `obsidian-cli` — almost always useful

**Connectors to enable:**
- `obsidian` — default on

**Connectors to disable:**
- Consider disabling `gmail`, `google-calendar`, and `figma` unless the session specifically involves those
