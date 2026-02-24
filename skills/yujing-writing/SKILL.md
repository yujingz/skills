---
name: yujing-writing
description: "Draft, rewrite, and structure strategy, engineering-practice, product, and team-alignment documents in Yujing's writing style: judgment-first, concise, list-driven, and execution-oriented. Use when the user needs trend analysis, annual goals, technical planning, team communication, or decision-ready Chinese/English/bilingual docs."
---

# Yujing Writing

## Goal
Produce writing that is direct, structured, and decision-ready: state judgment first, then expand with executable items.

## Required References
Read `references/style-signals.md` before drafting strategy docs, meeting docs, or annual-goal docs.

## Workflow
1. Identify document intent: trend scan, annual goals, engineering practice, product direction, or execution update.
2. Confirm audience and language mode: Chinese, English, or bilingual mirrored sections.
3. Build a section-first outline with explicit nouns, such as `趋势`, `目标`, `工程实践`, `产品方向`, `风险`, `下一步`.
4. Draft each point as `判断/事实 -> 影响 -> 动作`, and keep each sentence focused on one idea.
5. For goals, use numbered objectives with numbered sub-actions and explicit acceptance boundaries.
6. Add an automation pass: for each manual step, check whether it can be automated, validated, or delegated to AI.
7. Add a verification pass: specify review/acceptance methods (for example AI review + human review + BDD boundary).
8. Run the quality gate before finalizing.

## Global Style Rules
- Keep tone calm, decisive, and implementation-oriented.
- Prefer short declarative lines over long narrative paragraphs.
- Use contrast framing when useful, such as `A is getting cheaper, B is still expensive`.
- Use direct recommendations for execution, such as `Use the best model` and `Automate manual work whenever possible`.
- Prefer concrete operational verbs: `define`, `integrate`, `automate`, `validate`, `review`, `accept`.
- Prefer concrete nouns: `friction`, `workflow`, `boundary`, `owner`, `timeline`, `cost`, `toolchain`.
- Keep strategy tied to operations: every major viewpoint should map to a concrete engineering or product action.
- Separate `committed`, `optional`, and `out of scope` content explicitly.
- Avoid hype, vague abstractions, and slogan-only statements.

## Bilingual Rules
- Mirror heading structure across Chinese and English when bilingual output is requested.
- Align key terms on first mention, then stay consistent.
- Translate for clarity and business intent, not literal word-for-word mapping.

## Templates
Use one template as the default scaffold and adapt only when the user asks.

### Trend and Direction Template
1. Trends
2. This year's goals
3. Engineering practices
4. Product direction
5. Risks and boundaries
6. Next actions

### Technical Execution Template
1. Context and target
2. Scope and non-goals
3. Implementation approach
4. Validation and acceptance boundary
5. Risks and mitigation
6. Owners and timeline

### Team Operating Template
1. Context
2. Core judgments
3. Execution principles
4. Action items with owners
5. Review and acceptance method
6. Risks and blockers

## Quality Gate
1. State the core judgment of each section in the first line.
2. Map each trend or viewpoint to at least one operational implication.
3. Include measurable constraints or acceptance boundaries where available.
4. Distinguish `committed`, `optional`, and `out of scope`.
5. Include an automation opportunity check for repetitive manual work.
6. Include a validation approach for quality control and acceptance.
7. Keep wording concise and remove filler.

## Defaults for Missing Inputs
1. Assume audience is engineering and product leads plus execution owners.
2. Assume output should be list-first and decision-ready, not long-form narrative.
3. Assume the user wants practical actions that reduce human-AI friction.
