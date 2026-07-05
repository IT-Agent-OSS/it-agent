# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules



- For parser-heavy validation helpers, `builder` should treat `common-but-not-yet-covered failure families` as part of MVP scope, not as optional polish. `tester` and `reviewer` should explicitly probe one repeated failure from the same tool that is outside the shipped happy-path examples and judge whether it is clustered specifically or only generically.
- When reviewing local validation tools, verify both `specific repeated family coverage` and `intentional CLI/operator failure messaging`. Concretely: one unsupported-but-common log family should be tested, and one basic operator error such as a bad file path should return a short tool-level message rather than only an interpreter traceback.
- For Python CLI log analyzers, require a small regression test set that covers normalization families and CLI exit behavior separately. At minimum: one known family cluster case, one common uncovered-family probe, one generic fallback case, and one missing-input-path case.
- before inferring high-risk actions, check whether publish/deploy/post verbs are explicitly requested or only mentioned as exclusions, negations, or forbidden steps
- when a request mixes latest-info lookup, publish intent, and broad delegation, narrow or clarify before execution instead of silently proceeding
- if a heuristic planner supports Japanese UI, include at least one Japanese negation case such as `公開しない` or `投稿しない` in local checks
- 機能ロジックは UI ファイルに埋め込まず、ローカルでも `UI -> callable logic` の境界を作る
- API 化しなくても、後から CLI / UI / 別 wrapper から再利用できる構造を優先する
- CLI でも最初の実行例と期待出力を早い位置で見せる
- local web app では、何ができて何が返るかを above the fold で分かるようにする
## Recently Reflected Learnings



- The observed weaknesses are not unique to this artifact. They are recurrent risks for parser-heavy local tools and can be absorbed by stronger builder/tester/reviewer rules without adding a new role. The exact mypy `[return-value]` support and the missing-file message remain one-off artifact fixes, while the reusable part is the process rule that these cases must be tested and reviewed intentionally.
- UI 付きローカルツールでも、機能本体は callable module に切り出して UI は呼び出し層にする
- 同じロジックを将来の CLI / UI / automation から使い回せる構造を標準にする
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
- browser demo では、主機能が最終フレーム内に完全に収まることを確認する
- 収まらない時は縮小より先に UI 再構成や画面遷移を検討する
- external-facing claims need a separate evidence-sufficiency review, not only wording review
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
