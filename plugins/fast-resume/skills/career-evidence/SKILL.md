---
name: career-evidence
description: 'Collect, import, confirm, and maintain truthful career evidence in resume/facts.md. Use for 从零采集简历信息、导入已有简历、职业经历访谈、STAR 追问、事实确认、冲突处理, resume intake, career-evidence interviews, fact confirmation, or fact-base maintenance.'
---

# Career Evidence

Maintain the candidate's target-independent career fact base in `resume/facts.md`. This skill owns evidence intake, confirmation, conflicts, and interviews; it does not own resume wording, selection, design, or export.

## Non-negotiable Rules

- Never invent or strengthen experience, responsibilities, skills, dates, credentials, employers, metrics, or outcomes.
- Treat imported claims as `待确认`; keep source conflicts as `冲突` until the user resolves them.
- Give each fact a stable, never-recycled ID and retain its source, confirmation state, ownership, and metric precision.
- Treat `facts.md` as the only factual source. Other workflows may read it but must return new or corrected claims here for confirmation.
- Treat import as evidence normalization, not target-driven compression: deduplicate repeated claims, but preserve each confirmed claim's strength, dates, ownership, context, actions, results, metrics, and precision. Resume selection or condensation must never mutate `facts.md`.
- Never infer protected or sensitive information or store an identity-document number.

## Privacy and Workspace Setup

Before creating `resume/`:

1. Confirm that the current workspace is trusted and approved for storing the files.
2. Explain that files remain in the workspace, while relevant context is processed by GitHub Copilot.
3. Warn against public commits and offer to add `resume/` to `.gitignore` without overwriting existing rules.

Never store personal data in the skill installation directory. Use lowercase ASCII slugs and this shared structure:

```text
resume/
├── facts.md
├── research/
│   └── <target-profile-slug>.md
└── resumes/
    └── <target-role-slug>-<language>/
        └── resume.html
```

Exclude age, sex, marital status, full street address, and photo unless the target market requires the field and the user explicitly requests it. Never put personal details, private-employer information, or confidential terms into web searches.

## Run Intake

Inspect `resume/facts.md` before asking questions.

- **New**: collect target role, market, and output language; optionally collect seniority, industry, and company type. Offer `快速`, `标准` (default), and `深入` modes by interview depth, never by promised quality.
- **Import**: inventory supplied Markdown, TXT, HTML, or text-based PDF files. Extract claims at their original strength, record the source filename, group duplicates, and confirm one topic-sized group at a time. If a PDF has no selectable text, request a text export or permission to use an available OCR tool.
- **Resume**: summarize confirmed facts, conflicts, open items, and estimated remaining rounds without repeating answered questions.

The user may change interview depth or skip any question without restarting the workflow.

Interview by topic: contact and headline facts, employment, projects or representative work, education and credentials, skills, and occupation-relevant optional sections.

For each round:

1. Ask 3-5 concise questions about one topic and state the estimated remaining questions or rounds.
2. Reuse existing answers and let the user skip any question.
3. For important experiences, gather Situation, Task, Action, and Result internally; distinguish the user's actions from team outcomes.
4. Probe for credible scale, frequency, time, quality, cost, reach, risk, or efficiency, while accepting `无` when no metric exists.
5. Resolve ambiguous dates, titles, ownership, and conflicts with the user, then persist confirmed facts and unresolved gaps.

Do not expose STAR labels as resume prose or pass unconfirmed claims to `resume-content`.

## Maintain `facts.md`

Keep readable Markdown with minimal frontmatter:

```markdown
---
schema-version: 1
updated: YYYY-MM-DD
---
```

Use only fields relevant to the fact type:

```markdown
## FACT-001: Short factual title

- 状态: 已确认 | 待确认 | 冲突
- 来源: user interview or source filename, YYYY-MM-DD
- 适用方向: role, capability, or industry tags
- Situation: background and constraints
- Task: the user's responsibility or objective
- Action: the user's own actions
- Result: outcome and impact
- 指标: exact value, honest approximation/range, derived value, or none
- 指标类型: 精确 | 估算 | 推导 | 无
- 指标依据: source or reasoning, or none
```

Metric rules:

- `精确`: supported by a reliable source or confident recollection.
- `估算`: an honest approximation; downstream wording must signal approximation.
- `推导`: calculated from recorded confirmed inputs.
- `无`: no defensible metric; never manufacture one.

Identity, education, certification, and skill facts need no artificial STAR fields but still require status, source, and ID. Preserve confirmed facts unless new user evidence changes them; omission from one resume is not deletion from the fact base.

## Handoff

Return the fact-base path, newly confirmed IDs, pending items, conflicts, target context, and remaining interview estimate. Signal when enough confirmed evidence exists for `resume-content` to prepare or refresh a draft.
