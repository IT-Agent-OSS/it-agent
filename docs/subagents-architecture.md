# IT Agent Subagents Architecture

## Purpose

`it-agent` は 1 体の OSS として配布するが、内部では複数のサブエージェント役割を持つ。

この文書は、その内部構造を定義する。

## Core Principle

- 外部に見せるプロダクトは `it-agent` 単体
- 内部では役割分担したサブエージェントを使う
- 役割は narrow and opinionated に保つ
- 1 つの役割に何でもやらせない

## Default Roles

常設するのは次の5役だけ:

1. `builder`
2. `tester`
3. `reviewer`
4. `improver`
5. `uiux`

`it-agent` 本体が orchestrator の役割を持つ。

言語特化役は常設ではなく、必要時のみ追加する条件付き役とする。

## Workflow

```text
it-agent
-> builder
-> tester
-> reviewer
-> uiux
-> improver
-> reflection into IT Agent standard
```

## Parallelism

並列化しやすいのは以下:

- `tester` と `reviewer`
- `reviewer` と `uiux`
- 条件付き specialist 同士の比較観点
- 複数候補の技術選定比較

依存が強いので直列にすべきなのは以下:

- 要件未確定のまま build を始めること
- test 前に improvement を確定すること

## Information Boundaries

サブエージェントは、親が渡した情報だけで動く前提で設計する。

そのため、毎回最低限これを handoff する:

- theme or objective
- scope
- local run command
- known constraints
- previous findings

## Reflection Rule

`reviewer` と `tester` と `uiux` の所見を受けて、`improver` が以下を分類する:

- `reflect`
- `hold`
- `reject`

その結果を、`it-agent` の標準へ反映する候補として扱う。

## Internal Evolution

`it-agent` は以下の2方向で進化する:

1. 役割構成の進化
2. 各役割の中身の進化

特に後者を優先し、役割数を増やす前に既存役割の質を改善する。

詳細ルールは `agent-composition-rules.md` を参照。
