---
name: resume-assessment
description: 'Assess resume quality on its own or evaluate evidence-based fit against a job description or confirmed role profile, then produce a concise HTML report. Use for 简历评估、简历体检、STAR 检查、TMQ 检查、JD 匹配、岗位匹配、优势分析、薄弱点分析, resume assessment, resume audit, JD match, job fit, strengths, or gaps.'
---

# Resume Assessment

Assess without rewriting. Use confirmed evidence when available, separate candidate fit from resume presentation, and produce a concise HTML report.

## Modes and Inputs

- `general-quality`: requires a resume; checks standalone quality. Facts and target context are optional.
- `target-match`: requires a real JD or confirmed role profile, plus a resume or confirmed facts. With facts but no resume, assess candidate fit and mark visibility `未评估：尚无简历`; with a resume but no facts, assess textual alignment but mark candidate capability unverified.

Inspect the resume and `resume/facts.md` when present. Reuse known context, treat imported claims as `待确认`, and call profile-based results `推定岗位匹配`. If both modes are requested, combine them without repeating findings.

Route fact intake, confirmation, and conflicts to `career-evidence`; public role research to `general-role-profile`; selection, rewriting, and tailoring to `resume-content`; visual changes to `resume-design`; and resume preview or export to `resume-delivery`. Recommend actions, but do not silently rewrite the resume or strengthen its claims.

Never invent facts, infer that an omitted capability is absent, or treat keyword similarity as proof of experience. Do not produce numeric match, quality, or ATS scores.
Before writing personal data, reuse or complete the trusted-workspace approval from `career-evidence`.

## General Quality

Check:

1. truth, conflicts, ownership, chronology, credentials, and metric precision;
2. internal STAR evidence: context, responsibility, personal action, and result without forcing STAR headings into the prose;
3. useful quantification, accepting `无` when no metric is defensible;
4. focused bullets, clear structure, low repetition, readable density, and content-level ATS hygiene.

Assess `Quantify` directly and claims against confirmed facts when available. Without a target, mark job-specific `Tailor` and candidate-to-role `Match` as `未评估：需要目标岗位`.

Use `高风险`, `需改进`, or `通过`. Reserve `高风险` for truth, conflict, unsupported metrics, or material ambiguity.

## Target Match

First run the trust checks from the general assessment, then:

1. Split the target into atomic `REQ-*` items and classify each as `硬门槛`, `核心要求`, `加分项`, or `背景信息`.
2. Map each item to confirmed `FACT-*` evidence; judge directness, ownership, result, scale, recency when relevant, and metric credibility.
3. Assign one coverage label:
   - `已覆盖`: confirmed evidence directly supports the requirement;
   - `证据不足`: related evidence exists but is indirect, weak, or unconfirmed;
   - `尚未覆盖`: no relevant confirmed evidence exists.
4. Separately label resume visibility `清晰呈现`, `表达较弱`, or `未呈现`. Judge both discoverability and proportional emphasis: `清晰呈现` means the evidence is easy to find and receives detail appropriate to the requirement priority; `表达较弱` includes evidence that is buried, underspecified, or crowded out by lower-relevance content.

Compare emphasis across roles and projects. Flag equal-weight treatment when low-relevance detail occupies space that should support stronger hard or core requirement evidence. Relevance outranks recency; prefer newer evidence when otherwise comparable or when skill freshness materially affects the requirement, but do not penalize older direct evidence merely for age.

Report `高匹配且已呈现`, `高匹配但未呈现`, `证据缺口`, `经历缺口`, and `硬门槛风险`. High match requires a hard or core requirement, direct confirmed evidence, clear personal ownership, and a concrete result or scale where expected.

Use one supported conclusion: `匹配基础强`, `有条件匹配`, `证据不足，暂不能判断`, or `存在关键不匹配`. Report category counts, not percentages.

## HTML Report

Write the report to a caller-provided path or, by default:

```text
resume/assessments/<assessment-slug>.html
```

Use a lowercase ASCII slug and never overwrite an unrelated assessment.

Create one responsive, print-friendly HTML file with semantic headings, selectable text, inline CSS, `lang`, UTF-8, and no scripts, external resources, tracking, charts, gauges, or watermarks.

Keep the visible report short:

1. mode, evidence basis, target basis, and date;
2. one conclusion plus one scope limitation;
3. category counts, at most three strengths, and at most five priority actions;
4. the complete evidence matrix in native `<details>`.

Show every truth or hard-gate risk even when limits are exceeded. Keep each finding to evidence, impact, and action in at most two short sentences. Do not repeat the JD, explain methodology, add filler, or give unsupported generic advice.

For `general-quality`, the matrix contains `Location | Finding | Evidence | Severity | Action`. For `target-match`, it contains `Requirement | Priority | FACT evidence | Evidence strength | Resume visibility | Coverage | Action`. Add `data-requirement-id` and `data-fact-ids` where applicable.

## Validate and Handoff

Before reporting completion:

- reconcile counts with the matrix and verify referenced facts;
- keep truth and hard-gate risks outside collapsed content;
- check for readable HTML, scripts, and external resources;
- run desktop, mobile, and print checks when tools are available and name checks not run.

Return the report path, mode, evidence basis, overall conclusion when available, highest-priority findings, unavailable checks, and handoff owner for each next action. Send factual questions to `career-evidence` and approved wording or ordering work to `resume-content`.
