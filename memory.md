# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules



- Strengthen `builder` and `reviewer` instructions so diff/comparison tools must preserve semantic context, not only string deltas. If items are grouped by section, status, severity, or audience, moving the same statement between groups must be treated as a meaningful change case during implementation and review.
- For any parser- or heuristic-driven tool, tester and reviewer must include at least one input-format edge case and one semantic reclassification case, then verify the UI communicates unsupported input instead of returning a clean-looking empty result.
- For single-file TypeScript browser apps, builder handoff must explicitly document accepted input structure, parse assumptions, and empty/unsupported-input behavior in addition to the launch command.
- before inferring high-risk actions, check whether publish/deploy/post verbs are explicitly requested or only mentioned as exclusions, negations, or forbidden steps
- when a request mixes latest-info lookup, publish intent, and broad delegation, narrow or clarify before execution instead of silently proceeding
- if a heuristic planner supports Japanese UI, include at least one Japanese negation case such as `公開しない` or `投稿しない` in local checks
- CLI でも最初の実行例と期待出力を早い位置で見せる
- local web app では、何ができて何が返るかを above the fold で分かるようにする
- heuristic ツールでは confidence や uncertainty を visible にする
- browser-based local tools では、complete state と incomplete state の対比が有効なら標準で見せる
## Recently Reflected Learnings



- parser-heavy diff tool では unsupported input の明示と semantic reclassification case の確認を標準観点にする
- The failures expose stable improvements to existing roles and handoff checks without requiring any new agent. They align with `it-agent`'s rule of restraint by upgrading builder/tester/reviewer guidance and `ai-factory` gating instead of expanding the role set.
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
- browser demo では、主機能が最終フレーム内に完全に収まることを確認する
- 収まらない時は縮小より先に UI 再構成や画面遷移を検討する
- external-facing claims need a separate evidence-sufficiency review, not only wording review
- heuristic numeric checks should be tested with at least one derived-support boundary case
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
