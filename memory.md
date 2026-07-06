# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules



- For agent-facing browser tools, reviewer should treat the action surface itself as a quality target, not only the visible layout.
- Check whether the primary interactive path exposes stable selectors, descriptive action labels, and `name` attributes before calling the tool agent-ready.
- In browser-based HTML/JavaScript heuristics, keep evidence lists more prominent than any aggregate readiness score.
- before inferring high-risk actions, check whether publish/deploy/post verbs are explicitly requested or only mentioned as exclusions, negations, or forbidden steps
- when a request mixes latest-info lookup, publish intent, and broad delegation, narrow or clarify before execution instead of silently proceeding
- if a heuristic planner supports Japanese UI, include at least one Japanese negation case such as `公開しない` or `投稿しない` in local checks
- 機能ロジックは UI ファイルに埋め込まず、ローカルでも `UI -> callable logic` の境界を作る
- API 化しなくても、後から CLI / UI / 別 wrapper から再利用できる構造を優先する
- CLI でも最初の実行例と期待出力を早い位置で見せる
- local web app では、何ができて何が返るかを above the fold で分かるようにする
## Recently Reflected Learnings



- review the primary interactive path for stable selectors, descriptive actions, and structured field names before treating a browser tool as agent-ready
- This is not specific to WebMCP alone. The same failure mode will recur across browser automation helpers, local agent dashboards, and any future browser-first QA tool.
- UI 付きローカルツールでも、機能本体は callable module に切り出して UI は呼び出し層にする
- 同じロジックを将来の CLI / UI / automation から使い回せる構造を標準にする
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
- browser demo では、主機能が最終フレーム内に完全に収まることを確認する
- 収まらない時は縮小より先に UI 再構成や画面遷移を検討する
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
