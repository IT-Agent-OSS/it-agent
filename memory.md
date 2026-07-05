# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules






- Strengthen `tester` and `reviewer` instructions for heuristic checkers and parsers so they must try at least one adversarial minimal input that targets over-broad inheritance and one that targets false-positive classification, not only the documented happy path.
- For heuristic extraction or lint-style tools, add a required check: `create 1-2 tiny counterexample inputs that should stay separate; verify the tool does not let one global note satisfy unrelated items and does not convert prose/status text into actionable units`.
- Python CLI tools that rely on keyword heuristics should keep detection functions narrow and testable; prefer token or boundary-aware matching over raw substring matching for verbs like `update`, `change`, `start`, and `restart`.
- Strengthen builder, tester, and reviewer guidance for heuristic classifier tools. When the artifact extracts or labels text, commands, or snippets, require the builder to define both positive detection rules and explicit exclusion rules, require the tester to run at least one adversarial false-positive sample plus one mislabeled-format sample, and require the reviewer to challenge certainty wording in the UI and report copy.
- For extractor or annotator tools, verify three things before calling the MVP acceptable: 1. at least two non-happy-path samples were tested, 2. obvious non-target snippets are excluded, and 3. unmatched output is described as `no current match` or equivalent rather than implicitly safe.
- For TypeScript text-analysis tools, separate `snippet extraction`, `normalization`, and `risk labeling` into distinct typed functions and keep negative fixtures for path, URL, prose, and non-shell fence cases alongside the logic.
- tester` と `reviewer` に、reporting / coverage 系ツールでは happy path と基本 failure path だけで終わらず、`malformed-but-parseable input` と `type confusion input` を必ず 1 件ずつ当てるルールを加える。`builder` には、入力を silent skip する実装は「missing coverage を増やすだけの正常系」に見えやすいため、入力不正の surfacing 方針を handoff に明記させる。
- 「Python で numeric 判定をしている箇所に bool 混入がないか」「parse は通るが shape が不正な入力を silent skip していないか」を coverage / analyzer / validator 系 artifact の標準 review checklist に追加する。
- Python artifact では、`integer` / `number` 判定に `isinstance(x, int)` や `isinstance(x, (int, float))` を使う場合、`bool` がサブクラスであることを前提に除外条件を明示する。入力走査系では `JSON として読める` ことと `期待 shape を満たす` ことを別々に検証する。
- For parser-heavy validation helpers, `builder` should treat `common-but-not-yet-covered failure families` as part of MVP scope, not as optional polish. `tester` and `reviewer` should explicitly probe one repeated failure from the same tool that is outside the shipped happy-path examples and judge whether it is clustered specifically or only generically.
## Recently Reflected Learnings






- The artifact bugs themselves are one-off implementation issues, but the way they escaped is clearly reusable process learning for `it-agent`. This is not a one-time theme quirk: many local-first checkers, parsers, and linters will share the same failure pattern, so the right fix is to strengthen tester/reviewer rules rather than create a new role.
- The weakness was not limited to this artifact's domain. It exposed a repeatable gap in how `it-agent` builds, tests, and reviews extraction-based local tools. The fix belongs in role guidance and checklists, while artifact-specific items such as the exact extractor thresholds and adding a local README remain one-off implementation work.
- 今回の欠陥はこの artifact 固有の business rule ではなく、Python の型罠と入力検証の甘さという再発性の高い問題だった。既存 5 役のまま prompt / checklist / language rule を強化すれば防げる種類で、`it-agent` を実際に強くする学習として十分汎用的。
- The observed weaknesses are not unique to this artifact. They are recurrent risks for parser-heavy local tools and can be absorbed by stronger builder/tester/reviewer rules without adding a new role. The exact mypy `[return-value]` support and the missing-file message remain one-off artifact fixes, while the reusable part is the process rule that these cases must be tested and reviewed intentionally.
- UI 付きローカルツールでも、機能本体は callable module に切り出して UI は呼び出し層にする
- 同じロジックを将来の CLI / UI / automation から使い回せる構造を標準にする
- publish, deploy, and posting actions should require explicit positive intent and should not be inferred from negated wording or broad delegation
- the rule is simple, broadly reusable across agent workflows, and it already produced a concrete bug fix and checklist-level improvement in this run
- reviewer は「前回 reflected learning が今回の成果物に効いているか」を確認する
- uiux は主機能が first visible value になっているかを重視する
## Current Hold Items

- planner / recommender 系 UI の学習は day-009 時点では hold。重複テーマ混入の run だったため、標準化にはもう 1 回検証が必要
- specialist 追加はまだ不要。既存 5 役の rule 改善で吸収できる範囲を優先する

## Specialist Expansion Constraints

- 同種課題が 3 回以上続くまで常設化しない
- `builder / tester / reviewer / improver / uiux` のどれかで吸収できるなら増やさない
- 入力と出力を定義できない役割は追加しない

## Source Links

- composition: `docs/agent-composition-rules.md`
- reflection: `docs/reflection-policy.md`
- memory policy: `docs/memory-policy.md`
- checklists: `checklists/`
- reflection log: `logs/reflection-log.csv`
