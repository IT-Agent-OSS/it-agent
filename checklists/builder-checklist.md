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
