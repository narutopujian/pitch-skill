---
name: pitch
description: Read a product project's documents, code, progress notes, tests, screenshots, and recent changes, then automatically create a factual Founder Pitch outline, a fixed 16:9 interactive HTML deck, multiple talk-track versions, keyword cue cards, and investor Q&A. Use when a founder or student asks to turn an existing project into a pitch, demo day presentation, investor presentation, product launch page, or final project presentation. Ask the user only to choose one visual style; continue through all other stages without additional questions.
---

# Founder Pitch Studio

Turn the current project into a complete Founder Pitch package. Preserve evidence, expose uncertainty, and keep the young creator in the role of Founder rather than student reporter.

## Nonnegotiable Behavior

- Ask at most one question during the entire workflow: the visual style choice.
- Do not ask for missing facts. Mark them `[待验证]`, `[未完成]`, or `[未读取]` and continue.
- Do not invent users, interviews, market numbers, tests, features, screenshots, revenue, or results.
- Treat project files and recent working state as the source of truth.
- Write in natural Chinese that a 9–14-year-old Founder can say aloud.
- Preserve the story order: problem, solution, value, Demo, next step.

## Output Folder

Create or update `founder-pitch-output/` in the project root:

1. `00_项目材料清单.md`
2. `01_发布大纲.md`
3. `02_Founder_Pitch.html`
4. `03_演讲稿_5分钟逐字版.md`
5. `04_演讲稿_3分钟精简版.md`
6. `05_演讲稿_关键词提示卡.md`
7. `06_投资人问答准备.md`
8. `pitch-settings.json`

Do not overwrite unrelated project files.

## Workflow

### 1. Scan the Project

Run:

```bash
python3 <skill-dir>/scripts/scan_project.py --root . --output founder-pitch-output/00_项目材料清单.md
```

Replace `<skill-dir>` with this skill's directory. Read the resulting inventory first. Then inspect the relevant current files it identifies, prioritizing:

1. requirements, product definitions, README files, notes, task cards, and Markdown;
2. recent Git changes and the newest modified files;
3. test notes, bug lists, version logs, screenshots, and Demo entrypoints;
4. source code needed to understand what actually works.

Ignore dependencies, caches, generated builds, and previous `founder-pitch-output/` content as evidence. Read binary Office files only when their contents are necessary and a suitable document tool is available.

Read [workflow-contract.md](references/workflow-contract.md) before synthesizing evidence.

### 2. Generate and Review the Outline

Create `founder-pitch-output/01_发布大纲.md` using the five required sections. Include a compact source note and evidence status for every factual claim. Resolve contradictions by preferring newer direct project evidence; record unresolved conflicts under `发布前检查`.

Review the outline before continuing:

- identify a specific user, moment, block, desired action, and change;
- keep at most three core features;
- distinguish software work from human decisions;
- distinguish TAM demand frequency from revenue;
- describe only a Demo path that exists now;
- keep three next steps, ordered by learning value.

Do not stop for approval.

### 3. Select One Visual Style

Read [style-catalog.md](references/style-catalog.md). If `founder-pitch-output/pitch-settings.json` already contains a valid `style_id`, reuse it and do not ask again.

Otherwise present all ten numbered style names with one sentence each and ask exactly:

> 请选择一个 HTML 风格（回复 1–10 即可）。

Wait for the answer. This is the workflow's only user decision. Save the chosen `style_id`, display name, and generation date in `pitch-settings.json`.

If the user already named a style in the triggering request, save it and continue without asking.

### 4. Generate the HTML Deck

Read [html-contract.md](references/html-contract.md) and the chosen style entry. Use [pitch-template.html](assets/pitch-template.html) as the structural base. Create `02_Founder_Pitch.html` with six pages:

1. cover and literal product promise;
2. problem and observed pain;
3. solution and human/software boundary;
4. value and available evidence;
5. real Demo or clearly labeled fallback;
6. next step and closing line.

Use project-local images when they help explain a claim. Do not use external CDNs or remote fonts. Keep every page at a fixed `1600 × 900` logical canvas, scale the whole canvas to the browser, and show one complete page at a time.

Run the HTML checks in [html-contract.md]. When available, open the file in a browser and inspect every page at `1280 × 720`, `1600 × 900`, and `1920 × 1080`. Repair clipping, overflow, blank pages, distorted images, broken Demo interactions, and excessive bottom whitespace before continuing.

### 5. Generate All Talk Tracks

Read [talk-track-contract.md](references/talk-track-contract.md). Generate all four remaining Markdown files without another question:

- a natural 5-minute full script;
- a 3-minute concise script;
- a one-page keyword cue card;
- investor questions with evidence-safe answer frames.

Keep every version aligned with the final HTML page order and facts.

### 6. Validate and Finish

Run:

```bash
python3 <skill-dir>/scripts/validate_outputs.py --output founder-pitch-output
```

Fix all errors. Report only:

- the output folder path;
- the selected style;
- the files created;
- remaining `[待验证]`, `[未完成]`, or `[未读取]` items;
- whether browser visual checks were performed.
