# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules

- Update `it-builder.toml` developer_instructions to add: (1) README.md is a required output alongside `main_files` — not optional, not implied by `--help`; (2) when a CLI tool reads from stdin as its no-argument fallback, the `--help` text must say so and note any platform portability limits (e.g. `/dev/stdin` is not available on Windows). Update `it-tester.toml` developer_instructions to add: when the artifact contains a named dispatch structure (switch, role map, branch set), every named branch must be covered by a runnable example file — "code-traced only" must be flagged as PARTIAL in unverified_areas, not as silent coverage.
- Builder checklist — `[ ] README.md created at artifact root — covers: what it does, single run command, expected output for both pass and fail cases, and the callable-logic contract for reuse`. This is a required line item, separate from `main_files`.
- Node.js / ES module CLI projects: stdin-fallback mode must be documented in `--help` (terminal will block waiting for input if no argument and no pipe). Also note `/dev/stdin` is macOS/Linux only; Windows requires an explicit file path argument.
- it-builder` の developer_instructions に「empty state は到達経路ごとにメッセージを分けること（未入力 / 検出ゼロ / 既知非対応形式は distinct）」を追加する。
- なし（今回はロジック構造の問題であり言語特化は不要）
- uiux ロールの観点に「空入力・無効入力での silent return は UI として成立しない」を明示的に追加する。builder ロールも「入力バリデーション時のフィードバック有無」を build checklist で確認する責務を持つ。
- なし（今回の学習はパターン汎用）
- **builder** — add to builder instructions: "Every artifact directory must contain a `README.md` that covers (1) how to open or run the artifact, (2) what any score/grade scale means, and (3) a one-liner showing how to call the logic layer from outside the browser if one exists. This README is a deliverable, not optional documentation."
- For governance/intake tools, require recommendations to include missing facts, confidence, and next actions rather than a single verdict.
- When an artifact returns approval-like labels, verify that the UI and copy state the result is advisory and not final approval.
## Recently Reflected Learnings

- Both failures are structural patterns that will recur in future runs, not one-off edge cases. Failure 1 (missing README) is a missing checklist item in the builder contract. Failure 2 (unverified branches) is a missing coverage rule in the tester contract. Both belong in the standard operating rules and will pay back immediately in the next run.
- 4 項目とも「既存チェックリストに記載あり or 新規追加可能」で、役割ルール変更で吸収できる範囲に収まる。artifact 単体の one-off 修正ではなく、次回以降の全 run で再現する可能性が高い。Failure 2 の UX 項目は day-043 でも同種の miss が確認されており、2 回目の反復で reflect の判断は正当。
- 4 項目すべてが特定の実装に依存しない汎用ルールであり、次回以降の build / review / uiux フェーズで再発を防げる。コストは各チェックリストへの 1〜2 行追加のみで適用できる。
- All seven learnings are non-obvious, will recur in future artifacts, and map cleanly to existing checklist or role instruction files. None are one-off artifact quirks. The separation pattern (Win 1) and structured output pattern (Win 2) are also worth preserving as positive examples in builder instructions.
- The lesson applies to future governance, compliance, security, and workflow triage artifacts, not just this shadow AI board.
- Agent-facing tools need explicit checks for structured recoverable error contracts and visible re-evaluation feedback.
- The learning generalizes beyond this artifact to MCP servers, local agent tools, and future triage/review boards.
- All five rules are reusable across future runs, none are one-off fixes, and they address failure modes that will recur in any governance/classification artifact (rules 1–4) or any no-build-step browser artifact (rule 5). The wins (pure logic separation, dual-gate classification) also confirm patterns worth preserving in builder guidance.
- 判定ロジックの危険ケース検知を優先レビューすること、そして callable logic を UI 外へ分離することを正式ルール候補として持ち帰る
- どちらも day-039 固有の偶然ではなく、今後の it-agent と ai-factory に再利用価値がある。
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
