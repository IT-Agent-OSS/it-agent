# IT Agent Memory

## Core Identity

- `it-agent` はローカルで動くツールやシステムを作るための OSS エージェント設計
- 常設ロールは `builder / tester / reviewer / uiux / improver` の 5 つだけ
- 増やすべきなのは役割名ではなく、既存ロールの判断基準と handoff 品質

## Active Standard Rules










- Strengthen `builder` and `tester` guidance for audit and checker-style tools so they treat malformed source data as a first-class failure case and explicitly verify that documented matcher behavior matches the real implementation.
- For local audit/checker artifacts, require one negative test for malformed source rows and one contract test for any documented pattern-matching or parsing rule; reject silent row skipping unless it is surfaced as a warning or error by design.
- For Python CLIs, catch expected parse and validation failures at the CLI boundary and emit concise file-specific user errors instead of raw tracebacks for common operator mistakes.
- Strengthen `builder` and `tester` instructions for heuristic multi-source checkers so they must validate the claimed rule with a fixture, not only prove that the command launches and returns counts.
- If a sample README or demo narrative says "this input should warn" or "this case should not warn", tester must include an explicit reproduction that proves each stated expectation against actual output.
- For TypeScript CLI scanners that recurse directories, include either a default ignore list for common generated/vendor folders or a test that shows curated path input is mandatory and documented.
- Strengthen `tester` and `reviewer` guidance for local review tools so they explicitly verify that any displayed score, severity, sort order, or summary metric is safe for the decision it claims to support. If a tool tells users what to fix first, the checks must confirm that ranking logic matches that goal.
- For tools that output findings, require one check for `priority integrity` and one for `evidence traceability`. `Priority integrity` asks whether severity and ordering match the stated triage purpose. `Evidence traceability` asks whether each finding exposes enough concrete source detail for a user to validate and act on it quickly.
- None. This lesson is cross-language and should live in shared tester/reviewer rules rather than HTML/JavaScript-specific instructions.
- Strengthen `builder`, `tester`, and `reviewer` guidance for reviewer-facing diff or migration tools: when evidence is derived from matched identifiers, preserve disambiguating context from analysis through final output, and do not allow the presentation layer to collapse distinct records into the same label.
## Recently Reflected Learnings










- The issue was not a one-off product quirk. It exposed a repeatable weakness in builder claims, tester coverage, and reviewer contract checking for checker-style tools. The corrective rule is narrow, reusable, and fits existing `it-agent` roles without adding a new agent.
- reflect. The failures are not just one implementation mistake; they expose a repeatable weakness in how `builder`, `tester`, and the run process validate heuristic scanners. The rule is narrow enough to be actionable and broad enough to help future config, doc, and audit checkers.
- The lesson satisfies the `it-agent` evolution rule to improve existing roles instead of inventing new ones. It is reusable across languages and artifact types, directly strengthens the core build -> test -> review loop, and was supported by concrete evidence from this run rather than a one-off preference.
- The concrete bug belongs to this artifact, but the escape pattern is general and likely to recur in schema-diff, mapping, migration, and rename-review tools. The right response is to strengthen existing role guidance and checklists rather than add a new role or treat this as a one-off hold.
- The artifact bugs themselves are one-off implementation issues, but the way they escaped is clearly reusable process learning for `it-agent`. This is not a one-time theme quirk: many local-first checkers, parsers, and linters will share the same failure pattern, so the right fix is to strengthen tester/reviewer rules rather than create a new role.
- The weakness was not limited to this artifact's domain. It exposed a repeatable gap in how `it-agent` builds, tests, and reviews extraction-based local tools. The fix belongs in role guidance and checklists, while artifact-specific items such as the exact extractor thresholds and adding a local README remain one-off implementation work.
- 今回の欠陥はこの artifact 固有の business rule ではなく、Python の型罠と入力検証の甘さという再発性の高い問題だった。既存 5 役のまま prompt / checklist / language rule を強化すれば防げる種類で、`it-agent` を実際に強くする学習として十分汎用的。
- The observed weaknesses are not unique to this artifact. They are recurrent risks for parser-heavy local tools and can be absorbed by stronger builder/tester/reviewer rules without adding a new role. The exact mypy `[return-value]` support and the missing-file message remain one-off artifact fixes, while the reusable part is the process rule that these cases must be tested and reviewed intentionally.
- UI 付きローカルツールでも、機能本体は callable module に切り出して UI は呼び出し層にする
- 同じロジックを将来の CLI / UI / automation から使い回せる構造を標準にする
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
