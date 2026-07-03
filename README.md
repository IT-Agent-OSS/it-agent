# IT Agent

`IT Agent` は、ローカルで動くツールやシステムを作るための、ローカルファーストな OSS エージェント設計です。

このリポジトリで公開するのは `it-agent` 本体です。  
毎日改善を回す内部運用基盤は別リポジトリで管理し、このリポジトリには含めません。

## これは何か

`IT Agent` は、1つの全体統括エージェントと、少数の役割特化サブエージェントで構成されます。

常設するのは次の5役です。

- `builder`
- `tester`
- `reviewer`
- `uiux`
- `improver`

大事なのは、エージェント名を増やすことではありません。  
本当に必要な役割だけに絞り、その中身を継続的に改善していくことです。

## コア原則

- ローカルファースト: まずローカルで起動できることを重視する
- 役割は少なく: 繰り返し必要な役割だけを持つ
- 改善ループを明示: フィードバックを標準ルールへ戻す
- UI/UXも品質: 動くだけでなく、分かりやすく使いやすいことを重視する
- テンプレートより原則: 固定の見た目ではなく、判断基準を育てる

## 現在含まれているもの

このリポジトリには現在、次の内容が入っています。

- 役割定義
- サブエージェント構成ドキュメント
- handoff 契約
- レビューと UI/UX のチェックリスト
- `.codex` 用のサブエージェント設定
- reflection ログ
- 受け渡しイメージが分かる sample run

まだ、一般ユーザー向けに完成した実行ランタイム一式は入っていません。  
現時点では、`IT Agent` の構造と進化方針を公開する OSS リポジトリです。

## リポジトリ構成

```text
.codex/
  agents/                サブエージェント定義
checklists/             再利用するレビュー観点
docs/                   設計、ルール、roadmap、handoff 文書
logs/                   reflection 履歴
runs/sample-run/        受け渡しサンプル
```

## エージェント構成

### 常設ロール

- `builder`: ローカルで動くツールやシステムを実装する
- `tester`: 起動確認、正常系、失敗系を検証する
- `reviewer`: 品質、回帰リスク、OSSとしての見え方を確認する
- `uiux`: 分かりやすさ、使いやすさ、見せ方を改善する
- `improver`: 所見を `reflect / hold / reject` に整理する

### 条件付き specialist

言語特化や用途特化の役割は、必要性が繰り返し確認されたときだけ追加します。

例:

- `python-specialist`
- `ts-specialist`

基本方針は、先に既存役割の精度を改善し、それでも足りないときだけ新しい役割を足すことです。

## 主要ドキュメント

- [Agent Composition Rules](./docs/agent-composition-rules.md)
- [Subagents Architecture](./docs/subagents-architecture.md)
- [Handoff Contract](./docs/handoff-contract.md)
- [UIUX Review Checklist](./docs/uiux-review-checklist.md)
- [Reflection Policy](./docs/reflection-policy.md)
- [Roadmap](./docs/roadmap.md)

## 基本フロー

```text
it-agent
-> builder
-> tester
-> reviewer
-> uiux
-> improver
-> reflection into the IT Agent standard
```

実際の受け渡しイメージは [runs/sample-run](./runs/sample-run/README.md) を見ると把握しやすいです。

## UI/UX と動画の進化方針

`IT Agent` は、コード品質だけでなく、ツールの見せ方も改善対象とします。

- UI や動画の質もプロダクト品質の一部
- 再利用するのは原則や判断観点
- 固定の見た目テンプレートを守ることは目的にしない
- 毎回、その成果物に合う見せ方を選ぶ

## この OSS が向いている人

このリポジトリは、次のような人に向いています。

- 少数ロールで組むサブエージェント構成を学びたい
- 役割分担と handoff の設計を再利用したい
- ローカルファーストなツール生成エージェントを設計したい
- フィードバックを標準ルールへ戻す運用を OSS 化したい

## ライセンス

このリポジトリは MIT License で公開しています。
