# Builder Output

- run_id: sample-run-001
- theme: Local note summarizer
- target_user: 個人ユーザー
- local_run_type: CLI
- selected_language: Python
- build_summary: 単一テキストファイルを読み込み、短い要約を表示するCLIツールを作る
- included_scope: ファイル読込、要約処理、標準出力表示
- excluded_scope: GUI、複数ファイル一括処理、履歴保存
- run_command: `python main.py sample.txt`
- setup_notes: Python 3.11 を前提にし、依存は最小限にする
- main_files: `main.py`, `README.md`
- known_limitations: 長文や複数言語対応は未対応
- demo_plan: 小さなメモを読み込んで要約結果がすぐ出る流れを見せる
