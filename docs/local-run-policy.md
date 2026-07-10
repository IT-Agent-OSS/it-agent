# Local Run Policy

## Principle

`it-agent` が作る成果物は、まずローカルで立ち上がることを満たす。

## Allowed Output Types

- CLI tools
- Local web apps
- Local APIs
- Desktop helper tools
- Automation scripts

## Not Required At MVP Stage

- 本番公開
- 外部ホスティング
- SaaS化
- LINE連携

## Verification Minimum

- 起動手順がREADMEに書ける
- 第三者が手元で再現できる
- 主要動作を動画に撮れる
- plain ES module の browser artifact は、ブラウザ起動とは別に `node --input-type=module` でロジック層を検証できる smoke test コマンドを残す
