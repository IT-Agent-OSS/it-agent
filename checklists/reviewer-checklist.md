# Reviewer Checklist

## Purpose

`reviewer` が品質とOSS観点を一定水準で見るためのチェックです。

## Checklist

- 主要機能が目的に合っているか
- 明らかな回帰や破綻がないか
- README やセットアップの分かりにくさがないか
- README 冒頭で first-run example と expected output が見えるか
- 直近の reflected learning が今回の成果物で活きているか
- Web/UI artifacts では first visible value が user effort より前に出ているか
- 変換・分類・正規化系の Web ツールでは、complete sample と incomplete sample の両方で挙動確認できるか
- 分類・変換・抽出系なら、なぜその結果か / どれくらい確からしいかが見えるか
- 外向き claim や marketing copy を扱う成果物なら、主張の強さが evidence と釣り合っているか
- agent task planning や scope 判定系では、高リスク語を否定文脈でも誤って許可側に倒していないか
- 命名や画面の意味が伝わるか
- 一時しのぎ実装を標準化しようとしていないか
- `it-agent` に返すべき学習があるか
