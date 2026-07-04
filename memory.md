# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules


- before inferring high-risk actions, check whether publish/deploy/post verbs are explicitly requested or only mentioned as exclusions, negations, or forbidden steps
- when a request mixes latest-info lookup, publish intent, and broad delegation, narrow or clarify before execution instead of silently proceeding
- if a heuristic planner supports Japanese UI, include at least one Japanese negation case such as `公開しない` or `投稿しない` in local checks
- 機能ロジックは UI ファイルに埋め込まず、ローカルでも `UI -> callable logic` の境界を作る
- API 化しなくても、後から CLI / UI / 別 wrapper から再利用できる構造を優先する
- CLI でも最初の実行例と期待出力を早い位置で見せる
- local web app では、何ができて何が返るかを above the fold で分かるようにする
- heuristic ツールでは confidence や uncertainty を visible にする
- browser-based local tools では、complete state と incomplete state の対比が有効なら標準で見せる
- 動画や UI は固定テンプレート化せず、標準化するのは判断原則と review 観点に留める
- publish / deploy / post のような外部反映行為は、高リスク scope として明示依頼があるかを慎重に見る
- 外向き claim を扱う成果物では、reviewer が evidence sufficiency を独立観点として確認する
- heuristic な数値判定を含む成果物では、tester が derived support の境界ケースを 1 つ残す
- spec QA builder は、抽出対象を 1 つに混ぜず `assumption` と `missing fields` を最初から分離する。
- reviewer は spec helper で、欠損基準が UI か README に明示されているか確認する。
- TypeScript の text-review UI は、抽出カテゴリを別カードで出して比較しやすくする。
- triage 系 builder は label だけでなく、境界の根拠を何で説明するかまで最初に決める。
- reviewer は urgency classifier に説明可能性があるかを確認する。
- Python の rubric checker は score と reasons を分離出力し、後から閾値変更しやすくする。
- rule / policy QA ツールの builder は、例外条件と基本ルールを区別できる出力形を先に考える。
- reviewer は contradiction 系ツールで「条件違いを単純矛盾扱いしていないか」を確認する。
- TypeScript の text QA UI では、subject 正規化ロジックを UI と分離してテストしやすくする。
- 運用系チェッカーを作る builder は、signal の有無だけでなく優先順位づけまで最小要件として考える。
## Recently Reflected Learnings


- UI 付きローカルツールでも、機能本体は callable module に切り出して UI は呼び出し層にする
- 同じロジックを将来の CLI / UI / automation から使い回せる構造を標準にする
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
- browser demo では、主機能が最終フレーム内に完全に収まることを確認する
- 収まらない時は縮小より先に UI 再構成や画面遷移を検討する
- external-facing claims need a separate evidence-sufficiency review, not only wording review
- heuristic numeric checks should be tested with at least one derived-support boundary case
- spec 系ツールでは抽出カテゴリ分離と欠損基準の明示を標準にする
- 今後の仕様レビュー補助ツール全般に効く構造だから。
- triage 系ツールでは label より先に理由の透明性を確認する
- 他の classifier 系ツールにもそのまま効く学びだから。
- contradiction 系では条件差分を単純矛盾扱いしていないかを標準観点にする
- 文書 QA 系テーマ全体に再利用できる判断軸だから。
- blocker 検出系では優先順位づけと metadata 欠損の分離表示を標準観点にする
- 今後の blocker / urgency / review 系ツール全体に効く観点だから。
- parser-heavy diff tool では unsupported input の明示と semantic reclassification case の確認を標準観点にする
- The failures expose stable improvements to existing roles and handoff checks without requiring any new agent. They align with `it-agent`'s rule of restraint by upgrading builder/tester/reviewer guidance and `ai-factory` gating instead of expanding the role set.
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
