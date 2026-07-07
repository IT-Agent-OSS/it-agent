# IT Agent Composition Rules

## Purpose

`it-agent` の中身を増やしすぎず、必要な役割だけで進化させるためのルールです。

## Core Principle

`it-agent` は、システムやツールを作るために本当に必要な役割だけを持つ。

以下を避ける:

- 役割名だけ増えること
- 実態のない専門エージェントを量産すること
- 1回しか使わない役割を常設化すること

## Default Structure

`it-agent` 本体が全体判断を持ち、常設サブエージェントは次の5つだけにする。

1. `builder`
2. `tester`
3. `reviewer`
4. `improver`
5. `uiux`

## Role Definitions

### builder

- ローカルで起動できるツール/システムを実装する
- 原則として、利用イメージが湧く最小UIも用意する
- CLIだけで成立する場合でも、動画や初見デモのためのUIラッパーを優先的に検討する
- 機能ロジックは UI に直接埋め込まず、別ファイル / 別モジュールで呼び出せる形に切り出す
- ローカル用途では HTTP API 化までは不要だが、`UI -> callable logic` の呼び出し境界は必ず作る
- UI は機能の本体ではなく、入力を渡して結果を受け取る呼び出し層として設計する

### tester

- 起動可否、主要動作、失敗系を確認する

### reviewer

- 品質、使いやすさ、回帰リスク、OSSとしての見え方を確認する

### improver

- 学習を `reflect / hold / reject` に分け、標準ルールへ返す

### uiux

- 見た目、導線、操作性、第一印象を改善する
- 機能は動いていても、分かりにくい、弱い、触りたくならないUIを見逃さない
- ファイル投入、実行、結果確認が一画面で理解できるUIを優先する
- X動画で見せやすい画面構成になっているかまで責任範囲に含める
- UI 内に機能ロジックを埋め込みすぎず、差し替えや再利用がしやすい呼び出し構造になっているかも確認する

## Orchestration Rule

- `it-agent` 本体が orchestrator の役割を持つ
- 初期段階では `orchestrator` を独立常設エージェントにしない
- 必要な委譲判断は `it-agent` 本体が行う

## Specialist Rule

- 言語特化や用途特化の専門役は、初期状態では常設しない
- 必要時のみ呼ぶ `条件付きサブエージェント` とする

例:

- `typescript-specialist`
- `python-specialist`
- `go-specialist`

運用ルール:

- specialist の定義ファイル(`.codex/agents/*.toml`)は先に置いてよいが、`.codex/config.toml` への登録は必要になった時だけ行う
- 未登録の定義ファイルは「候補」であり、常設5役の rule 改善で吸収できる間は登録しない

## When A New Role Can Be Added

新しい役割を追加してよいのは、以下をすべて満たす場合だけ。

1. 同じ種類の課題が 3 回以上繰り返し発生した
2. `builder / tester / reviewer / improver / uiux` のどれかに吸収しにくい
3. 分離すると品質か速度が明確に上がる
4. 入力と出力を定義できる
5. 役割名ではなく、実務上の責任が説明できる

## When A New Role Should Not Be Added

以下の場合は追加しない。

- 何となく便利そう
- 名前を付けたいだけ
- 1回しか使わない
- 既存5役の指示を少し変えれば対応できる
- 学習ルールとして吸収した方が良い

## Preferred Order Of Growth

`it-agent` は次の順で進化する。

1. 既存5役の精度向上
2. チェックリストや標準手順の追加
3. 言語特化ルールの追加
4. それでも足りない場合に限り、新役割の追加

## Reflection Rule

- レビュー結果を受けて `it-agent` を更新するか判断するのは `ai-factory` 側
- `it-agent` は反映先であり、役割追加も `ai-factory` の改善判断を通して行う

## Rule Of Restraint

迷ったら、役割を増やすのではなく、既存役割のルールを改善する。

## Internal Evolution Rule

`it-agent` は外側の役割名だけでなく、中身も進化対象とする。

進化対象:

- 各役割の developer instructions
- チェックリスト
- handoff 形式
- 言語別ルール
- UI/UX 観点
- ローカル起動ポリシー
- 機能層と UI 層の分離ルール

つまり、役割数をむやみに増やさなくても、各役割の中身を改善し続けることを標準とする。
