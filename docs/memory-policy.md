# IT Agent Memory Policy

## Purpose

`it-agent` の `memory.md` は、役割定義、checklist、reflection 履歴の上にある短期標準記憶として使う。

詳細ルールの source of truth は既存ドキュメントに残し、`memory.md` は「今どの標準が有効か」を最短で伝える。

## Source Of Truth

- 役割構成: `docs/agent-composition-rules.md`
- reflection 方針: `docs/reflection-policy.md`
- handoff: `docs/handoff-contract.md`, `docs/handoff-templates.md`
- checklist: `checklists/`
- 反映履歴: `logs/reflection-log.csv`

## Memory Scope

`it-agent/memory.md` に書くのは次だけにする。

1. Core identity
2. Active standard rules
3. Recently reflected learnings
4. Current hold items
5. Specialist expansion constraints
6. Source links

## Read Timing

次の場面で `memory.md` を最初に読む前提にする。

1. 新しい reflect を取り込む前
2. builder / tester / reviewer / uiux / improver の共通方針を確認する前
3. specialist を追加するか迷うとき
4. README や checklist を更新するとき

## Write Rule

書いてよい内容:

- `reflect` 済みで、次回も再利用すべきルール
- `hold` だが、現在注意喚起として価値が高いもの
- 常設ロール全体に効く短い判断基準

書かない内容:

- 単発 artifact 固有の細かい UI 仕様
- 長い run narrative
- すでに checklist や docs に完全に書いてあり、優先度も低いもの

## Relationship With Reflection Log

- `logs/reflection-log.csv` は履歴
- `memory.md` は現在有効な要約

履歴を全部読む代わりに、まず `memory.md` を読んで、その後必要なら詳細へ降りる設計にする。

## Initial Rollout

導入初期は、`ai-factory` で `reflect` と判断したもののうち、再利用価値が高いものだけを `memory.md` に要約して載せる。

## Success Condition

1. `it-agent` の現在有効な標準が 1 枚で読める
2. 新しい run で参照すべき reflected learning を見落としにくい
3. 新ロール追加より先に既存5役の改善を促せる
