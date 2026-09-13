---
name: resume-delivery
description: 'Build, preview, validate, version, and export an approved resume as semantic HTML and selectable-text PDF. Use for HTML 简历、实时预览、质量检查、ATS 检查、定稿、版本化、导出 PDF, resume rendering, quality gates, finalization, or PDF export.'
---

# Resume Delivery

Turn a fixed content contract into a traceable working HTML document, preview and validate the resulting artifact, then create immutable finalized HTML/PDF versions. This skill owns artifact assembly, validation, preview, versioning, and export. It does not decide facts, wording, content order, or visual presentation.

## Required Inputs and Boundaries

Require:

- fixed visible text and semantic order from `resume-content`;
- supporting confirmed IDs in `resume/facts.md`;
- target role, market, language, and output directory;
- the existing `resume.html`, when present.

Return factual changes to `career-evidence`, wording or ordering changes to `resume-content`, and presentation changes to `resume-design`. Delivery verifies the resulting artifact instead of revising decisions owned by those skills.

Do not install packages or system dependencies without explaining their purpose and receiving explicit approval. Do not create a final PDF until the user explicitly approves finalization, and never overwrite a finalized version.

## Working Artifact

Write the working document to:

```text
resume/resumes/<target-role-slug>-<language>/resume.html
```

Use lowercase ASCII slugs. Create the first HTML draft as soon as confirmed evidence supports meaningful content; do not wait for every interview round to finish. When the file already exists, preserve sound structure and visual choices and make focused incremental changes. Redesign wholesale only at the user's request or when the current structure cannot meet the output requirements.

After creating or updating the semantic working HTML, hand it to `resume-design` when visual work is in scope. Resume preview, validation, and export after the design pass returns the same working file.

Treat these as artifact acceptance criteria, not visual-design instructions:

- preserve the content contract's exact visible text, semantic order, `data-fact-ids`, and `data-placeholder` values;
- treat emphasis tiers and omission rationale as internal contract metadata; never render those labels or use them to change the fixed text or order;
- keep information in selectable text and coherent, ATS-friendly DOM order;
- verify every claim's `FACT-*` IDs against confirmed entries in `facts.md`; never add a claim only in HTML;
- keep final CSS and any permitted local font data inside the document;
- include no external resource, tracking, runtime script, watermark, or image-only contact information.

After each meaningful update, report what changed or remains unresolved and refresh the preview.

## Preview

Start or reuse a local live-reload preview when available and provide its URL. In VS Code, offer the Simple Browser or an external browser; in CLI, print the local URL. If no live server is available, provide the static HTML path and explain that manual refresh is required.

Preview-only live-reload code may be injected by the server but must never be written into final HTML.

## Quality Gates

Run focused checks after substantial updates and the full set before finalization.

### Hard Errors

Block finalization and PDF export when any condition is true:

- a claim lacks valid traceability or uses an unconfirmed, conflicting, or missing fact;
- an unresolved `data-placeholder="true"` or placeholder text remains;
- HTML or PDF rendering fails;
- final HTML contains an external resource, tracking, runtime script, or watermark;
- PDF text is not selectable or copyable.

The user cannot waive a hard error. Report the exact issue and smallest corrective action.

### Warnings

The user may knowingly accept:

- page count outside the market- and seniority-appropriate recommendation;
- ATS risk from a creative layout;
- target-irrelevant content the user insists on retaining.

Record acknowledgement before finalization. Do not issue unverifiable percentage scores.

### Rendered Checks

Inspect actual browser and print/PDF output, not source alone. Reuse `resume-design` findings where applicable, but independently verify the final artifact for:

- clipping, overflow, overlap, blank pages, isolated headings, and awkward page breaks;
- visible/selectable text, coherent links and document order, and intact traceability;
- responsive behavior and CJK/Latin wrapping where applicable.

Report a short actionable issue list and name unavailable checks; never claim an unrun gate passed.

## Finalize and Export

Proceed only after explicit user approval that the working draft is final.

1. Run all hard gates, warning checks, and rendered checks.
2. Resolve every hard error. Present warnings and obtain acknowledgement where applicable.
3. Find the highest existing `resume-vN` and choose the next unused integer.
4. Copy approved `resume.html` to `resume-vN.html`; keep `resume.html` as the working file.
5. Prefer local Node.js, Playwright, and Chromium for PDF generation. Detect availability before use.
6. If dependencies are missing, explain why they are needed and request approval before installation.
7. Export `resume-vN.pdf` with backgrounds and print CSS enabled.
8. Verify page layout and extract or select PDF text to confirm it is not image-only.
9. Report final paths, completed checks, and accepted warnings.

If the user declines dependencies, deliver the checked HTML and explain how to print it with a system browser. Do not label an unchecked manual PDF as having passed the PDF gate.

## Handoff

Report the working or versioned artifact paths, preview URL when active, completed checks, hard blockers, accepted warnings, and any issue routed back to evidence, content, or design. Never call a draft final before explicit approval and all hard gates pass.
