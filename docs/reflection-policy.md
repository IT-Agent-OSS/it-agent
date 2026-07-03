# IT Agent Reflection Policy

## Purpose

`ai-factory` から渡された学習を、`it-agent` 側でどう記録し、標準に取り込むかの方針です。

## Rule

- 反映判断は `ai-factory` が行う
- `it-agent` は反映先として、その学習を構造化して蓄積する
- `reflect` されたものだけを標準ルール候補として扱う

## Record Location

- `logs/reflection-log.csv`

## Typical Target Layers

- role instruction
- checklist
- documentation pattern
- uiux rule
- capture rule
- local run policy
- language-specific rule
