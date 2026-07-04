# skills

Claude Code skills, organized as **plan-to-ship**: a four-stage workflow that takes an idea from a rough conversation to shipped, tested code.

## The workflow

Run these in order:

| Stage | Skill | Purpose |
| --- | --- | --- |
| 1 | [`grill-me`](plan-to-ship/grill-me/SKILL.md) | Stress-test a plan or design through relentless interview, one question at a time |
| 2 | [`to-system-design`](plan-to-ship/to-system-design/SKILL.md) | Turn the grilled conversation into a full system-design PRD, rendered as an interactive HTML artifact |
| 3 | [`to-issues`](plan-to-ship/to-issues/SKILL.md) | Break the PRD into independently-grabbable vertical-slice issues on your tracker |
| 4 | [`tdd`](plan-to-ship/tdd/SKILL.md) | Implement each issue with a red-green-refactor loop |

Each skill's `SKILL.md` explains its own process in detail — this table is just the map.

## Using these skills in your own project

Copy the `plan-to-ship/` folder into wherever your Claude Code setup discovers skills (e.g. `.agents/skills/` or `.claude/skills/` at your project root). That's the whole workflow — `grill-me`, `to-system-design`, `to-issues`, and `tdd` all travel together, no other setup required. `to-system-design` and `to-issues` will ask you once, the first time they're used in a repo, where your issue tracker lives and what triage labels you use.

## Repo layout

```
plan-to-ship/                          the workflow — copy this whole folder
├── SKILL.md                           pipeline overview + acknowledgments
├── grill-me/SKILL.md                  stage 1
├── to-system-design/SKILL.md          stage 2
├── to-issues/SKILL.md                 stage 3
└── tdd/                               stage 4
    ├── SKILL.md
    ├── tests.md
    └── mocking.md
```

## Acknowledgments

`grill-me`, `to-issues`, and `tdd` are adapted from [Matt Pocock](https://github.com/mattpocock)'s engineering skills — thank you for the inspiration. `to-system-design` is original to this repo.
