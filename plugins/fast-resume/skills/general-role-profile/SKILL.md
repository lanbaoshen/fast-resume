---
name: general-role-profile
description: 'Research current public postings and build a source-backed general target-role profile when no specific JD is supplied. Use for 目标岗位调研、通用 JD 参考、岗位画像、市场岗位要求, target-role research, role profiles, or job-market research.'
---

# General Role Profile

Build a current market reference for a target role when no specific JD is available. If the user supplies a JD, return it to the calling workflow for direct analysis.

## Inputs

- Required: target role, job market or location, and output language.
- Optional: seniority, industry, company type, and caller-provided output path.

Reuse known values and ask only for missing required inputs. If the role or market is too broad for useful searches, ask one concise clarifying question.

## Workflow

1. Search current public postings using generic role, market, seniority, industry, synonyms, and local terminology.
2. Prefer employer career pages and authoritative occupational sources. Use aggregators only for discovery or supplemental evidence.
3. Aim for 5-10 usable postings from independent employers. Keep the sample aligned with the requested role, market, and seniority; report when fewer sources are available.
4. Assign stable IDs (`SRC-001`, `SRC-002`, ...) and record each source's publisher, title, location or work arrangement, type, URL, access date, responsibilities, qualifications, tools, terminology, seniority signals, and expected evidence. Record the posting date when available.
5. Exclude duplicates, snippet-only pages, stale postings, and materially different roles from recurrence counts, but retain them in the source log with the reason.
6. Normalize clear synonyms, count each finding once per independent posting, and report recurrence as `n/N sources` rather than a market percentage.
7. Separate recurring from employer-specific expectations and required from preferred qualifications. Capture expected proof, conflicts, regional terms, sample bias, and weak evidence. Weight central duties and screening criteria, not frequency alone.

If usable sources are unavailable, create a `临时岗位画像` only when useful. State that it comes from existing knowledge, describe the limitation, and provide no fabricated citations.

## Evidence Rules

- Use only public sources available without bypassing authentication, paywalls, robots restrictions, or other access controls.
- Never put personal, resume, private-employer, or confidential-project information in web queries.
- Never invent sources, requirements, frequencies, dates, or quotations.
- Keep every synthesized finding traceable to source IDs, URLs, and access dates.
- Summarize in original wording; do not reproduce long passages.
- Label sourced synthesis `推定岗位画像`, never a real opening or JD.
- Do not evaluate a candidate, rewrite a resume, or provide application advice.

## Output

Use the caller-provided path when present. Otherwise write to:

```text
resume/research/<target-profile-slug>.md
```

Use a lowercase ASCII slug that distinguishes the target role, market, and language. Never overwrite research for an unrelated target profile. Keep the Markdown readable and use this structure:

```markdown
---
schema-version: 1
kind: general-role-profile
status: pending-confirmation
target-role: <role>
market: <market>
language: <language>
research-date: YYYY-MM-DD
basis: public-postings | provisional-knowledge
usable-source-count: <number>
---
```

Include, when supported: research scope and limitations, role summary, responsibilities, required and preferred qualifications, terminology and tools, expected evidence, contextual or conflicting signals, and the source log. Show recurring findings in a `Finding | Recurrence | Sources` table and mark whether each logged source was included.

Omit empty optional sections. Preserve source IDs when refreshing a file and never recycle removed IDs. Summarize the scope, strongest recurring expectations, and limitations, then ask the user to confirm or correct the profile. Keep `status: pending-confirmation` until confirmation; then set `status: confirmed` and add `confirmed-date: YYYY-MM-DD`.

Return the research path, profile type, status, source count, and unresolved limitations to the caller.

If the user asks to skip research, do not create a misleading research artifact. Return that choice so the calling workflow can record it and continue with a general-role resume.
