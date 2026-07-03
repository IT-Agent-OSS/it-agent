# IT Agent Subagents Implementation Plan

## Current Status

現時点では、サブエージェントは `役割定義` と `.codex` の構造だけを持つ。

まだやっていないこと:

- 実際の運用実績蓄積
- language specialist の増設
- run_state.json の実運用
- 反映ログとの結線
- UI/UX 観点の標準チェック化

## Next Build Order

1. `.codex` の role definitions を安定化
2. `run_state.json` の初版を決める
3. `it-agent` 本体が見る handoff 形式を決める
4. `uiux` role の handoff 観点を決める
5. `it_improver` の reflect/hold/reject 出力形式を決める
6. 言語特化 role を追加する

## Important Constraint

`it-agent` 自体を巨大な工場にはしない。

内部にサブエージェント構造を持っていても、外向きの見え方は一貫して:

- local-first
- tool/system builder
- evolving OSS

に保つ。
