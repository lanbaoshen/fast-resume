---
name: resume-content
description: 'Select, write, and tailor resume content from confirmed career evidence and assessment findings. Use for 内容取舍、简历改写、岗位定制、要点写作、章节排序, resume writing, content strategy, bullet writing, content selection, or tailoring after assessment.'
---

# Resume Content

Turn confirmed career evidence into target-specific resume copy and a fixed content contract.

## Inputs and Boundaries

- Target role, job market, and output language.
- Confirmed facts from `resume/facts.md`.
- A real job description, a confirmed general role profile, or the user's explicit choice to proceed without research.
- The matching `resume-assessment` report when acting on a resume audit or tailoring to a target.
- Optional seniority, industry, company type, current resume, and desired page range.

This skill owns content selection and order, wording, tailoring, and content-level ATS structure. It does not own formal resume assessment, requirement prioritization, target-coverage labels, or assessment reports. Route those to `resume-assessment`, fact confirmation to `career-evidence`, market research to `general-role-profile`, presentation to `resume-design`, and HTML/PDF finalization to `resume-delivery`.

Use only confirmed facts. Keep every substantive claim linked to stable `FACT-*` IDs; return missing, conflicting, or unconfirmed information to `career-evidence` without repairing or strengthening it. Generate each role and language version independently rather than translating sentence by sentence.

Handle conventional professional resumes. When another artifact is required, such as an academic CV, Europass document, government form, portfolio resume, cover letter, LinkedIn profile, or application tracker, explain the boundary and assist only with the conventional resume portion when useful.

## Consume the Target Basis

- **Real job description**: use the matching `target-match` assessment and preserve its `REQ-*` IDs, priorities, coverage labels, and stated ambiguities. Do not independently issue a second match judgment.
- **No real job description**: reuse a confirmed matching profile from `resume/research/`. For targeted tailoring, consume the corresponding assessment and label the basis `推定岗位匹配`. If the user skips research, record that choice and state the general-role basis without claiming target match.

Preserve source IDs, assessment limitations, and evidence distinctions. Never turn `证据不足`, `尚未覆盖`, or an unconfirmed resume claim into affirmative content.

## Act on Assessment Findings

Confirm that the report matches the current target, fact base, and resume version. If it is stale or materially incomplete, return it to `resume-assessment` instead of silently re-evaluating it here.

- Preserve `高匹配且已呈现` content unless a stronger content-level reason supports changing it.
- Surface `高匹配但未呈现` evidence in the most relevant section.
- Return `证据缺口` and credibility risks to `career-evidence` as focused questions before writing the claim.
- Do not repair an `经历缺口` or `硬门槛风险` with adjacent keywords or stronger wording.
- Resolve general-quality findings through focused edits, ordered by truth risk, target impact, and readability.

Do not reproduce the assessment report in the resume or turn diagnostic language into candidate-facing prose.

## Select and Write Content

Apply Tailor-Match-Quantify:

- **Tailor**: select and order confirmed facts for the target profile and market.
- **Match**: use target terminology only when the evidence genuinely supports it.
- **Quantify**: include credible scale or impact while preserving `精确`, `估算`, or `推导` precision.

Do not give every experience equal prominence. Keep all confirmed facts in the fact base, but allocate resume space for the current target using:

1. target relevance: direct evidence for hard or core requirements before transferable or low-relevance evidence;
2. evidence value: clear ownership, credible outcomes, useful scale, and distinct contribution before weak or repetitive claims;
3. recency: recent demonstrations before older equivalent evidence, especially for fast-changing skills;
4. chronology value: enough context to show credible progression and continuity for the target market.

Relevance outranks recency: an older experience that directly proves a core requirement may receive more detail than a recent unrelated role. Keep a recent low-relevance role visible when needed for chronology, but compress its bullets. Never disguise an older achievement as recent or use a rigid year cutoff without a market-specific reason.

Assign each role or project an internal emphasis tier:

- **Lead**: direct, strong target evidence; give it prominent placement and the most specific supporting bullets.
- **Support**: transferable, reinforcing, or less current evidence; use fewer bullets and remove duplication.
- **Context**: low-relevance or superseded evidence; retain only the identity, dates, and minimal continuity context when needed, or intentionally omit it when chronology and market conventions allow.

Use reverse chronological role order by default, while ordering bullets within each role by target relevance and impact. When space is constrained, remove low-relevance contextual detail first, then redundant supporting evidence; preserve unique hard-requirement proof and a coherent recent chronology.

Compress important Situation, Task, Action, and Result evidence into natural resume language without exposing STAR headings. Give each bullet one main action or outcome, make ownership explicit, and remove empty self-praise, repetition, irrelevant detail, and keyword stuffing. Never present team results as individual ownership or estimates as exact numbers.

Choose a market- and seniority-appropriate section order and page target. Ordinary professional resumes usually aim for one or two pages, but content relevance and readability take priority over arbitrary compression. If the user insists on low-relevance content, identify it as a warning for finalization rather than silently removing it.

## Content Contract

Hand `resume-delivery` a fixed content contract containing:

- target role, market, language, and profile basis;
- assessment report path, mode, applicable `REQ-*` IDs, and unresolved limitations;
- sections in semantic document order;
- exact visible text for every heading, label, date, summary, and bullet;
- the `FACT-*` IDs supporting each substantive claim;
- each role or project's emphasis tier and the rationale for material compression or omission;
- visible language-appropriate placeholders marked as unresolved;
- intentional omissions and any accepted low-relevance content;
- unresolved content, evidence, page-count, or ATS risks.

Report the selected direction, addressed assessment findings, fact IDs, omissions, placeholders, and warnings. After handoff, factual changes return to `career-evidence`, diagnostic changes return to `resume-assessment`, wording or ordering changes return here, and presentation must not alter the contract.
