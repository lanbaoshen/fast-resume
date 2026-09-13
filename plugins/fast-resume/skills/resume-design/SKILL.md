---
name: resume-design
description: 'Style an existing working HTML resume for screen and print while preserving its content and semantic order. Use for 简历视觉设计、排版、字体、颜色、间距、布局、打印样式, resume styling, typography, layout, or print design.'
---

# Resume Design

Style the working HTML created by `resume-delivery`. Treat its content and semantic order as fixed, and adapt the presentation to the candidate's occupation, target market, seniority, language, and page constraints.

## Scope and Boundaries

This skill owns visual direction and presentation-layer HTML/CSS. Facts, writing, content strategy, candidate evaluation, preview infrastructure, final approval, versioning, and export remain with the calling workflow. Ask only when a missing visual choice would materially change the result.

- Preserve all visible text, semantic document order, and every `data-fact-ids` and `data-placeholder` value exactly. Never add, remove, rewrite, prioritize, or reorder content for visual convenience.
- Do not derive resume content from `facts.md`, a job description, or role research. Return missing, unsuitable, or overlong content to the calling workflow instead of resolving it here.
- Never create visuals that imply facts. Keep all information selectable and meaningful in document order; do not carry it only in icons, images, generated graphics, pseudo-elements, or backgrounds.
- Use no external resources, remote fonts, tracking, runtime scripts, or watermarks. Embed a custom open-license font only when its local asset and license are available.
- Update only an existing working HTML file and return content, ordering, or traceability problems to the calling workflow.

Default to an **ATS-first** single-column design in the supplied reading order. Use an expressive layout only when the user requests it after being told the ATS tradeoff; always preserve semantics, selectable text, legibility, and print reliability.

## Design Workflow

### 1. Assess the Visual Constraints

Inspect the document before choosing a style. Identify:

- relevant conventions for the occupation, market, and seniority;
- language-specific typography, especially CJK and Latin mixing;
- text density, line measure, paper size, and page-break pressure;
- semantic order, markup hooks, and sound existing design choices that must be preserved.

Do not research what the resume should say. If visual research is necessary, search only generic role, industry, market, and document-design terms; never use confidential details.

### 2. Choose the Direction

For a substantial redesign, briefly define:

- the intended visual character;
- typography and language fallbacks;
- restrained color tokens and their purpose;
- paper size, margins, content measure, spacing rhythm, and hierarchy.

For a focused adjustment, change only the affected tokens and rules. Preserve sound existing choices unless the user requests a redesign or they prevent readable screen or print output.

### 3. Build for Screen and Print

Implement the direction in semantic HTML and maintainable CSS:

- Define design tokens as CSS custom properties for color, type, spacing, rules, and page geometry.
- Use a restrained type scale and readable line measure. Prefer `9.5pt`-`11pt` print body text; never shrink below `9pt` to force a page count or scale type with viewport width. Check CJK and Latin wrapping separately.
- Keep spacing, dates, and bullets scannable. Support the language with appropriate line breaking, punctuation, fallbacks, and real font weights.
- Preserve semantic elements and DOM order. Repair presentation markup only for accessibility or print reliability and without changing content.
- Keep selector specificity predictable; avoid overlapping element and utility rules that silently cancel spacing or typography decisions.
- Ensure accessible contrast and grayscale legibility; do not rely on color alone. Keep focus visible for interactive links in the screen preview.
- Default to `A4` where customary and `Letter` in the US and Canada. Define `@page` size, margins, print colors, link treatment, and break behavior; avoid clipped bullets, isolated headings, split entries, blank pages, and excessive gaps.
- Make the screen preview responsive without changing reading order. Write no preview scripts into `resume.html`, and omit nonessential animation or hover effects.
- Avoid sidebars, layout tables, charts, skill percentages, icon-only labels, and visual effects that weaken extraction or printing unless an approved expressive direction requires them.

If content cannot fit readably within the requested page count, report it to the calling workflow. Do not alter content, collapse hierarchy, or use illegibly small type to conceal the problem.

### 4. Check the Rendered Result

Use the available browser and print rendering supplied by the calling workflow. Check:

- hierarchy, scanability, alignment, and consistency with the chosen direction;
- clipping, overlap, overflow, blank pages, and awkward breaks;
- CJK and Latin glyphs, punctuation, weights, wrapping, contrast, and grayscale legibility;
- responsive behavior, selectable text, coherent order, unchanged content, and intact traceability attributes.

Correct visual defects, repeat the focused check, and state any checks that tools could not verify. Return the working file to `resume-delivery` for preview management, quality gates, versioning, and export.

## Handoff

Report the working HTML path, design concept, principal visual decisions, unresolved fit or ATS risks, and completed screen and print checks. Route content decisions back to the calling workflow; do not call the result final or claim downstream gates passed.
