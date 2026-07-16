# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules

- it-builder` の developer_instructions に「empty state は到達経路ごとにメッセージを分けること（未入力 / 検出ゼロ / 既知非対応形式は distinct）」を追加する。
- なし（今回はロジック構造の問題であり言語特化は不要）
- uiux ロールの観点に「空入力・無効入力での silent return は UI として成立しない」を明示的に追加する。builder ロールも「入力バリデーション時のフィードバック有無」を build checklist で確認する責務を持つ。
- なし（今回の学習はパターン汎用）
- **builder** — add to builder instructions: "Every artifact directory must contain a `README.md` that covers (1) how to open or run the artifact, (2) what any score/grade scale means, and (3) a one-liner showing how to call the logic layer from outside the browser if one exists. This README is a deliverable, not optional documentation."
- For governance/intake tools, require recommendations to include missing facts, confidence, and next actions rather than a single verdict.
- When an artifact returns approval-like labels, verify that the UI and copy state the result is advisory and not final approval.
- Browser JavaScript artifacts should expose core logic as an importable module and include a small Node-based test path when practical.
- For agent-facing tools, reviewer/tester should confirm error contracts are structured, recoverable, observable, and user-actionable.
- **Builder**: add a rule that when a logic module returns a `breakdown`, `reasoning`, or `explanation` object alongside a verdict, that object must include all data the UI needs to render a human-readable explanation — including multipliers and weights, not just raw dimension values. Storing raw values without weights shifts the rendering burden to the UI and requires the UI to couple to internal logic constants. This is a data-contract failure, not a UI omission.
## Recently Reflected Learnings

- 4 項目とも「既存チェックリストに記載あり or 新規追加可能」で、役割ルール変更で吸収できる範囲に収まる。artifact 単体の one-off 修正ではなく、次回以降の全 run で再現する可能性が高い。Failure 2 の UX 項目は day-043 でも同種の miss が確認されており、2 回目の反復で reflect の判断は正当。
- 4 項目すべてが特定の実装に依存しない汎用ルールであり、次回以降の build / review / uiux フェーズで再発を防げる。コストは各チェックリストへの 1〜2 行追加のみで適用できる。
- All seven learnings are non-obvious, will recur in future artifacts, and map cleanly to existing checklist or role instruction files. None are one-off artifact quirks. The separation pattern (Win 1) and structured output pattern (Win 2) are also worth preserving as positive examples in builder instructions.
- The lesson applies to future governance, compliance, security, and workflow triage artifacts, not just this shadow AI board.
- Agent-facing tools need explicit checks for structured recoverable error contracts and visible re-evaluation feedback.
- The learning generalizes beyond this artifact to MCP servers, local agent tools, and future triage/review boards.
- All five rules are reusable across future runs, none are one-off fixes, and they address failure modes that will recur in any governance/classification artifact (rules 1–4) or any no-build-step browser artifact (rule 5). The wins (pure logic separation, dual-gate classification) also confirm patterns worth preserving in builder guidance.
- 判定ロジックの危険ケース検知を優先レビューすること、そして callable logic を UI 外へ分離することを正式ルール候補として持ち帰る
- どちらも day-039 固有の偶然ではなく、今後の it-agent と ai-factory に再利用価値がある。
- Neither failure is a one-off quirk of this specific handoff-checking domain. Any future browser artifact with a dark-mode CSS block can hit the identical hardcoded-color trap, and any future tool with a selector/dropdown driving computation against persistent textarea/file state can hit the identical stale-recompute trap. Both are narrow, concrete, and were independently reproduced (uiux's `getComputedStyle` read for the CSS bug; reviewer's and uiux's live Playwright reproduction for the stale-state bug), and both are absorbable into the existing `uiux`/`reviewer`/`tester` checklists without adding a new role, consistent with the preferred growth order in `agent-composition-rules.md`.
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
