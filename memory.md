# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules

- `uiux` must explicitly test a browser artifact in both the default color scheme and a forced OS/browser dark color scheme before signing off on visual quality, since a `prefers-color-scheme` block existing in the CSS is not evidence it was actually exercised. Separately, `reviewer` and `tester` must add "change a control after a result/report is already rendered" (e.g. flip a dropdown, retoggle a filter, without clearing state first) as a standard non-linear regression probe for any stateful UI, not only the linear load -> analyze -> read path.
- New checklist items added to `it-agent/checklists/uiux-checklist.md` (verify controls in forced OS/browser dark mode, not only the default) and `it-agent/checklists/reviewer-checklist.md` plus `it-agent/checklists/tester-checklist.md` (test changing a control after a result is already shown, not only the first-pass linear flow).
- For CSS that ships a `prefers-color-scheme: dark` media query, base element rules (`button`, `select`, `input`, and similar controls) must reference themed custom properties (e.g. `var(--panel)`, `var(--text)`) rather than a literal color like `white`; a hardcoded literal in the base rule silently survives the dark-mode override block untouched. Added as a CSS/styling rule note for `builder`.
- Strengthen `reviewer` and `improver` guidance for heuristic tools so they must challenge confident labels such as `supported`, `safe`, or `complete` with at least one adversarial counterexample, not just confirm happy-path counts.
- For any heuristic classifier, require one false-positive probe and one false-support or false-attribution probe before recommending `PASS`; record whether the tool explains why a confident label was assigned.
- For Python text heuristics, avoid raw substring keyword checks for semantic classification when token- or phrase-aware matching is feasible in the standard library; require explicit word-boundary or tokenization logic for short keywords like `can`.
- For agent-facing browser tools, reviewer should treat the action surface itself as a quality target, not only the visible layout.
- Check whether the primary interactive path exposes stable selectors, descriptive action labels, and `name` attributes before calling the tool agent-ready.
- In browser-based HTML/JavaScript heuristics, keep evidence lists more prominent than any aggregate readiness score.
- Strengthen `reviewer` instructions for parser, checker, and spec-driven tools so the review must probe at least two realistic non-happy-path input shapes that are common in the target format, even when the bundled sample passes.

## Recently Reflected Learnings

- Neither failure is a one-off quirk of this specific handoff-checking domain. Any future browser artifact with a dark-mode CSS block can hit the identical hardcoded-color trap, and any future tool with a selector/dropdown driving computation against persistent textarea/file state can hit the identical stale-recompute trap. Both are narrow, concrete, and were independently reproduced (uiux's `getComputedStyle` read for the CSS bug; reviewer's and uiux's live Playwright reproduction for the stale-state bug), and both are absorbable into the existing `uiux`/`reviewer`/`tester` checklists without adding a new role, consistent with the preferred growth order in `agent-composition-rules.md`.
- The failures were not accidental one-off bugs tied only to this artifact. They expose repeatable process gaps in how `it-agent` tests and reviews heuristic classifiers, and the corrective rule is stable enough to improve future Python and text-analysis runs without adding a new role.
- The defect pattern is clearly reusable across future schema-driven tools, fits existing `reviewer` and ai-factory process layers, and does not depend on this single artifact's domain. The build/test/review evidence is strong enough to justify a standard-rule update.
- The issue was not a one-off product quirk. It exposed a repeatable weakness in builder claims, tester coverage, and reviewer contract checking for checker-style tools. The corrective rule is narrow, reusable, and fits existing `it-agent` roles without adding a new agent.
- reflect. The failures are not just one implementation mistake; they expose a repeatable weakness in how `builder`, `tester`, and the run process validate heuristic scanners. The rule is narrow enough to be actionable and broad enough to help future config, doc, and audit checkers.
- The lesson satisfies the `it-agent` evolution rule to improve existing roles instead of inventing new ones. It is reusable across languages and artifact types, directly strengthens the core build -> test -> review loop, and was supported by concrete evidence from this run rather than a one-off preference.
- The concrete bug belongs to this artifact, but the escape pattern is general and likely to recur in schema-diff, mapping, migration, and rename-review tools. The right response is to strengthen existing role guidance and checklists rather than add a new role or treat this as a one-off hold.
- The artifact bugs themselves are one-off implementation issues, but the way they escaped is clearly reusable process learning for `it-agent`. This is not a one-time theme quirk: many local-first checkers, parsers, and linters will share the same failure pattern, so the right fix is to strengthen tester/reviewer rules rather than create a new role.
- The weakness was not limited to this artifact's domain. It exposed a repeatable gap in how `it-agent` builds, tests, and reviews extraction-based local tools. The fix belongs in role guidance and checklists, while artifact-specific items such as the exact extractor thresholds and adding a local README remain one-off implementation work.
- 今回の欠陥はこの artifact 固有の business rule ではなく、Python の型罠と入力検証の甘さという再発性の高い問題だった。既存 5 役のまま prompt / checklist / language rule を強化すれば防げる種類で、`it-agent` を実際に強くする学習として十分汎用的。

## Current Hold Items

- planner / recommender 系 UI の学習は day-009 時点では hold。重複テーマ混入の run だったため、標準化にはもう 1 回検証が必要
- specialist 追加はまだ不要。既存 5 役の rule 改善で吸収できる範囲を優先する

## Specialist Expansion Constraints

- 同種課題が 3 回以上続くまで常設化しない
- `builder / tester / reviewer / improver / uiux` のどれかで吸収できるなら増やさない
- 入力と出力を定義できない役割は追加しない

## Source Links

- composition: `docs/agent-composition-rules.md`
- reflection: `docs/reflection-policy.md`
- memory policy: `docs/memory-policy.md`
- checklists: `checklists/`
- reflection log: `logs/reflection-log.csv`
