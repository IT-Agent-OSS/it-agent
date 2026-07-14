# Builder Checklist

## Purpose

`builder` が最低限外さないための実装チェックです。

## Checklist

- ローカル起動方法がある
- 起動コマンドが明確
- README 冒頭に first-run example を置ける
- MVP範囲が絞られている
- 未実装部分を明記している
- デモで見せる主機能がある
- 依存関係が過剰ではない
- verdict / score / classification を返すロジックでは、UI が説明表示できるように raw value だけでなく weighted value・reasoning・breakdown を返している
- plain ES module の browser artifact では、`node --input-type=module` でロジック層を検証できる smoke test コマンドを handoff に残している
- 公開・投稿・deploy のような高リスク操作は、肯定依頼か否定文脈かを区別して included scope に入れている
- README に書ける形になっている
- `artifacts/` 配下に最小 README（起動コマンド・ファイル構成・ライセンス 5 行程度）を常に置いている
- OK/pass センチネルパターンを複数カテゴリで使う場合、発火条件（`results.length === 0` か severity 条件か）をカテゴリ間で統一しており、スコア分母が意図せず増加しない
- 入力バリデーションで早期 return する場合、ユーザーへの視覚的フィードバック（エラーテキスト・ボーダー変化）を必ず返している（silent return 禁止）
