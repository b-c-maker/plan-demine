# plan-demine

[简体中文](README.md) | English (this file)

Clear the mines in your plan **before** work starts: **planning + mine-clearing in a single pass** — no "here's a plan, wait for the next round to review it."

**Division of labor: the user owns the direction, the agent assembles the parts, evidence verifies the facts.** Mine-clearing only verifies the facts of a plan the user has already signed off on — never the agent's self-chosen direction. A skewed direction, verified thoroughly, is just a well-verified mistake.

## Usage

| Scenario | Command |
|---|---|
| No plan yet; you want the full flow (triage → draft → sign-off → mine-clearing) | `/plan-demine` or just say "make a plan and clear it" |
| You have a plan file; clear it directly | `/plan-demine <path-to-plan>` |
| A plan you endorse is already in the conversation | `/plan-demine` (drafting stage auto-skipped) |
| Only an unsigned agent draft is in the conversation | `/plan-demine` (a lightweight sign-off happens first) |

## The single-pass flow

```
entry detection → triage (probe / minor / engineering)
  → drafting (nail down goal/scope/trade-offs; every unverified claim gets tagged [unverified])
  → ★sign-off gate: you approve direction + draft (mandatory — no sign-off, no clearing)
  → clearing (mine list → cheapest verifier per mine → evidence table → triage; facts only — doubtful direction goes back to you)
  → you approve the live-test list → run probes (isolated sandbox, deleted after)
  → confirm changes one by one → write them back into the plan → release verdict
```

The flow interrupts you exactly three times: **sign-off** (the anti-drift gate), probe approval, and one-by-one change confirmation.

## Three deliverables

1. **Evidence table** — every claim's status: verified / refuted / unresolved / accepted risk (there is no fifth state)
2. **The corrected plan** — changes written into place, `[unverified]` tags removed
3. **A one-line release verdict** — go / go-after-changes / not-cleared-to-start

## Design sources

- [gbasin/stress-test-skill](https://github.com/gbasin/stress-test-skill): six-stage skeleton, evidence grading, three-bucket verdicts, live-test approval
- [laurigates/claude-plugins · verify-before-plan](https://github.com/laurigates/claude-plugins): premise concept, four-part return contract, threshold filtering, cheapest-verifier selection
- [obra/superpowers · writing-plans](https://github.com/obra/superpowers): plan discipline (zero context assumed, file structure first, no placeholders, every step checkable)
- [obra/superpowers · brainstorming](https://github.com/obra/superpowers): three-level triage, non-shrinkable HARD-GATE approval, complexity only goes up, the sign-off gate
- [github/spec-kit](https://github.com/github/spec-kit), [eyaltoledano/claude-task-master](https://github.com/eyaltoledano/claude-task-master): process chaining and task decomposition

## Related

- [skill-flywheel](https://github.com/b-c-maker/skill-flywheel): sister skill — after the task, it auto-sediments reusable workflows into skills (with a reflection/correction loop). One governs starting; the other governs finishing.

## Install

- Location: user-level skills root (e.g. `~/.dsh/skills/plan-demine/` on DeepSeek Harness) — visible in all workspaces
- Layout: top-level `SKILL.md` + `README.md`, UTF-8 without BOM
- Runtime artifacts: plan docs live in `<projectRoot>/plans/`, probe sandboxes in `<projectRoot>/.plan-demine-poc/` (deleted after use)

## License

[MIT](LICENSE) © 2026 b-c-maker
