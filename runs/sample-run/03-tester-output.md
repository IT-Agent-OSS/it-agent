# Tester Output

- run_id: sample-run-001
- launch_status: PASS
- command_used: `python main.py sample.txt`
- happy_path_results: ローカルファイルを読み込み、短い要約が出力される
- failure_path_results: ファイル未存在時はエラーメッセージを返す
- reproduction_steps: 存在しないファイル名で実行すると失敗再現可能
- unverified_areas: 長文、大量ファイル、非UTF-8入力
