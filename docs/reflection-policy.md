# IT Agent Reflection Policy

## Purpose

`ai-factory` から渡された学習を、`it-agent` 側でどう記録し、標準に取り込むかの方針です。

## Rule

- 反映判断は `ai-factory` が行う
- `it-agent` は反映先として、その学習を構造化して蓄積する
- `reflect` されたものだけを標準ルール候補として扱う
- 直近で再利用価値が高い reflected learning は `memory.md` に要約して保持する

## Record Location

- `logs/reflection-log.csv`
- `memory.md`

## Typical Target Layers

- role instruction
- checklist
- documentation pattern
- uiux rule
- capture rule
- local run policy
- language-specific rule
