# plan-to-ship workflow skills

## What

Four Claude Code skills that cover the full idea-to-implementation loop, meant to be run in order:

| Order | Skill | Purpose |
| --- | --- | --- |
| 1 | grill-me | Stress-test a plan or design through relentless interview |
| 2 | to-system-design | Turn the grilled conversation into a full system-design PRD, rendered as an interactive HTML artifact |
| 3 | to-issues | Break the PRD into independently-grabbable vertical-slice issues on the tracker |
| 4 | tdd | Implement each issue with a red-green-refactor loop |

`to-system-design` and `to-issues` need to know where your issue tracker lives and what triage labels you use; they'll ask the first time if it isn't already established.

## Why
Codifies a repeatable planning and delivery workflow, accessible directly from Claude Code.

## Acknowledgments
`grill-me`, `to-issues`, and `tdd` are adapted from [Matt Pocock](https://github.com/mattpocock)'s engineering skills — thank you for the inspiration. `to-system-design` is original to this repo.
