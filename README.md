# bear-light

A MATATAG-aligned Daily Lesson Log (DLL) builder for Philippine DepEd teachers — designed to work with any AI model that supports the Skills.sh / Claude skill format.

---

## What it does

`bear-light` helps teachers generate complete, submission-ready DLLs through a structured, guided conversation with an AI. It handles both the **Weekly DLL** and **Daily DLL** formats used under the DepEd MATATAG curriculum, filling every section of the official template — from the school header and learning competencies down to formative assessment and reflections.

The skill is built around one core principle: **a DLL is a thinking document, not a formatting exercise.** It pushes the AI to ask the right questions first, flag anything uncertain in bold, and produce content that actually matches what the teacher is doing that week — not generic filler that happens to have the right headers.

---

## Who this is for

- **DepEd teachers** who want AI assistance with DLL writing without learning any technical tools — just upload the skill and start a conversation.
- **Developers and portfolio reviewers** looking at how a real instructional workflow gets encoded as a reusable AI skill.
- **School coordinators or department heads** who want to see what AI-assisted lesson planning looks like when it's designed responsibly (accuracy flagging, competency code verification, no invented details).

---

## File structure

```
bear-light/
├── SKILL.md                          # The skill definition — the AI reads this
├── assets/
│   ├── dll_weekly_blank.docx         # blank Weekly DLL template
│   └── dll_daily_blank.docx          # blank Daily DLL template
└── references/
    └── dll_template.md               # Section-by-section breakdown of both formats
```

### What each file does

**`SKILL.md`** — The core of the skill. Defines the step-by-step workflow the AI follows: collecting the school header, choosing Weekly vs. Daily format, reading uploaded modules, drafting in markdown, rendering a visual preview, and exporting to `.docx`. It also encodes the operating principles — no emojis in official documents, bold-flag all uncertain content, never invent competency codes.

**`assets/dll_weekly_blank.docx`** and **`assets/dll_daily_blank.docx`** — The actual blank DepEd templates, sourced from Castillejos National High School's official documents. These are used at the export stage: the AI fills content into the existing table structure rather than building from scratch, which preserves the original formatting (Montserrat font, borders, layout) exactly.

**`references/dll_template.md`** — A plain-text breakdown of both DLL formats, showing which sections are shared and which fork by day. The AI uses this as the authoritative section structure during drafting. The one structural difference between Weekly and Daily formats is documented here precisely: only the "Learning Competency" and "Learning Objectives" rows split into Day 1–5 columns in the Daily format — everything else stays a single block.

---

## How it works (the conversation flow)

The skill walks the AI through a fixed sequence of steps. No step is skipped.

**Step 0a — School header**
Before anything is drafted, the AI collects the official school header (Department, Region, Schools Division, Municipality, School Name). These go into the document letterhead. A wrong header on a DepEd document is not a minor slip — the skill treats this accordingly.

**Step 0b — Weekly or Daily**
The two formats differ structurally, not just in length. The AI confirms which format is needed before drafting.

**Step 1 — What materials exist?**
If only a topic is given, the AI asks clarifying questions before drafting. If modules or softcopies are uploaded, it reads them first and curates what belongs in a planning document versus what was written for the learner.

**Step 2 — Competency codes**
The skill never invents or guesses a formal MATATAG competency code. If the exact code isn't certain, it leaves a bold `[VERIFY CODE]` placeholder and asks the teacher to confirm it. Competency language (not the formal code) can be drafted normally.

**Step 3 — Draft in markdown**
The full DLL is drafted in the chat first, in markdown. This is the iteration phase — the teacher reviews and requests changes before anything is finalized or exported.

**Step 4 — Visual preview, then export**
Once the teacher confirms the draft, the AI renders a clean visual preview. Then — and only then — it offers to export the document as a `.docx` file using the matching blank template from `assets/`.

---

## Key design decisions

**Accuracy over speed.** The skill is deliberately slower than a one-shot "generate a DLL" prompt. It asks questions, flags gaps, and refuses to guess on high-stakes fields like competency codes. This is intentional — the teacher is accountable for this document, not the AI.

**Model-agnostic by design.** The skill is written so it can run on Claude, GPT-4, Gemini, or any other capable model through the Skills.sh format. The operating principles (no emojis, bold-flag uncertainty) are stated explicitly rather than assumed.

**Templates over generation.** At the export stage, the AI fills the existing official `.docx` templates rather than generating a new document from scratch. This matters because DepEd documents have specific formatting requirements that are brittle — rebuilding the table structure from code almost always breaks something.

**Retrospective sections handled honestly.** The "Reflections" section of the DLL is inherently written after the week has happened. The skill drafts it as guiding prompts rather than pre-written content the teacher hasn't lived yet.

---

## Usage

### With Claude (claude.ai)

1. Upload `bear-light.skill` (or the extracted folder) to a Claude conversation.
2. Tell Claude what DLL you need: subject, grade level, topic, and week.
3. The skill guides the rest of the conversation.

### With Skills.sh or other platforms

Follow the platform's skill installation instructions. The skill entry point is `bear-light/SKILL.md`.

### Requirements

No installation, no code, no API keys needed on the teacher's end. The skill runs entirely in the AI conversation. The `.docx` export requires the AI to have file creation capability (available in Claude's computer use / tool-enabled modes).

---

## Limitations

- **Competency codes are not auto-filled.** The skill will always ask the teacher to verify MATATAG codes rather than generate them. This is a feature, not a missing piece.
- **Learner Context cannot be pre-filled.** The AI has no knowledge of the actual class — this section always requires the teacher's own input.
- **The Reflections section is intentionally left as prompts** in the initial export, because the week hasn't happened yet at drafting time.
- **The `.docx` templates are specific to Castillejos National High School's letterhead.** Teachers from other schools will need to update the header or replace the template assets.

---

## About

Built by **Jerry Serillano**.

This skill was developed as part of a broader effort to make AI-assisted DepEd documentation practical for frontline teachers — without requiring technical setup, API keys, or any coding knowledge.

---

The skill logic (`SKILL.md`, `references/`) is open for educational and non-commercial use.
