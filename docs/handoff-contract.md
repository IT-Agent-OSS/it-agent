# IT Agent Handoff Contract

## Purpose

`it-agent` 内の各ロールが、何を受け取り、何を返すかをそろえるための共通ルールです。

## Core Rule

各ロールは、前段の成果をそのまま雰囲気で解釈せず、必要項目を明示的に受け取って動く。

## Shared Required Fields

すべての handoff で最低限渡す:

- `run_id`
- `date`
- `theme`
- `objective`
- `target_user`
- `scope`
- `local_run_type`
- `selected_language`
- `known_constraints`

## Builder Handoff In

- selected theme
- target user
- required local run type
- chosen language
- known constraints

## Builder Handoff Out

- build summary
- included scope
- excluded scope
- run command
- setup notes
- main files
- known limitations
- demo plan

## Tester Handoff In

- builder output
- run command
- setup notes
- expected happy path
- expected failure path

## Tester Handoff Out

- launch status
- exact command used
- happy path results
- failure path results
- reproduction steps
- unverified areas

## Reviewer Handoff In

- builder output
- tester output

## Reviewer Handoff Out

- overall verdict
- strengths
- weaknesses
- regression risks
- OSS clarity issues
- suggested fixes

## UIUX Handoff In

- builder output
- tester output
- reviewer output
- screenshots or demo notes when available

## UIUX Handoff Out

- first impression issues
- hierarchy issues
- flow confusion points
- visual weaknesses
- interaction weaknesses
- quick win suggestions
- what should become a standard UI/UX rule

## Improver Handoff In

- builder output
- tester output
- reviewer output
- uiux output

## Improver Handoff Out

- reflect / hold / reject
- reusable learning
- target layer
- update summary
- next-run changes

## Preferred Sequence

```text
builder
-> tester
-> reviewer
-> uiux
-> improver
```

## Parallel Option

以下は状況により並列化できる:

- `reviewer` と `uiux`

ただし、どちらも `builder` と `tester` の結果を前提にする。
