# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules





- rule / policy QA ツールの builder は、例外条件と基本ルールを区別できる出力形を先に考える。
- reviewer は contradiction 系ツールで「条件違いを単純矛盾扱いしていないか」を確認する。
- TypeScript の text QA UI では、subject 正規化ロジックを UI と分離してテストしやすくする。
- 運用系チェッカーを作る builder は、signal の有無だけでなく優先順位づけまで最小要件として考える。
- tester は blocker / urgency / ownership の 3 観点が混ざるツールで、出力が優先順位を示せているか確認する。
- Python の運用チェッカーでは、キーワード検出結果と管理情報欠損を別ラベルで出す。
- Strengthen `builder` and `reviewer` instructions so diff/comparison tools must preserve semantic context, not only string deltas. If items are grouped by section, status, severity, or audience, moving the same statement between groups must be treated as a meaningful change case during implementation and review.
- For any parser- or heuristic-driven tool, tester and reviewer must include at least one input-format edge case and one semantic reclassification case, then verify the UI communicates unsupported input instead of returning a clean-looking empty result.
- For single-file TypeScript browser apps, builder handoff must explicitly document accepted input structure, parse assumptions, and empty/unsupported-input behavior in addition to the launch command.
- before inferring high-risk actions, check whether publish/deploy/post verbs are explicitly requested or only mentioned as exclusions, negations, or forbidden steps
## Recently Reflected Learnings





- contradiction 系では条件差分を単純矛盾扱いしていないかを標準観点にする
- 文書 QA 系テーマ全体に再利用できる判断軸だから。
- blocker 検出系では優先順位づけと metadata 欠損の分離表示を標準観点にする
- 今後の blocker / urgency / review 系ツール全体に効く観点だから。
- parser-heavy diff tool では unsupported input の明示と semantic reclassification case の確認を標準観点にする
- The failures expose stable improvements to existing roles and handoff checks without requiring any new agent. They align with `it-agent`'s rule of restraint by upgrading builder/tester/reviewer guidance and `ai-factory` gating instead of expanding the role set.
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
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
