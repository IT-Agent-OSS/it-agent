# IT Agent Subagents State Model

## Purpose

サブエージェント間で受け渡す状態を、最低限そろえるためのモデルです。

## Why This Matters

サブエージェントはコンテキストを自動共有しない前提で考えた方が安全です。

そのため、状態同期点を明確にする。

## Suggested State File

- `run_state.json`

## Suggested Fields

- `run_id`
- `date`
- `theme`
- `objective`
- `target_user`
- `scope`
- `selected_language`
- `local_run_type`
- `build_status`
- `test_status`
- `review_status`
- `uiux_status`
- `improvement_status`
- `reflection_decision`
- `artifacts`
- `notes`

## Suggested Sync Points

1. `theme_locked`
2. `build_started`
3. `build_ready_for_test`
4. `test_completed`
5. `review_completed`
6. `uiux_completed`
7. `reflection_decided`

## Rule

状態が曖昧なまま次のサブエージェントへ進めない。

## Example

サンプルは `run-state-example.json` を参照。
