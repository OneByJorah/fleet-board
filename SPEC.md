# fleet-board spec

Every requirement is a row with an id. Agents build against approved rows; commits cite the ids they serve. `pullboard spec check` lints this file.

Statuses: approved = decided · draft = proposed · pending = open question · fact = true today · wont = won't build, decided and kept · retired = no longer applies, kept. Ids are permanent: never delete or renumber a row. Tiers: must · aim.

Write each requirement as one row under its section, in this format. The fence keeps the example out of the spec, so no placeholder id is ever committed; your own rows go below, outside it.

```text
- G1 [draft, must] The first thing the client needs, in one line. | gate: the test that proves it
- K1 [draft, must] A constraint, e.g. runs locally with no account. | gate: review
```

## G · Goals: what the client asked for

## K · Constraints
- K1 [draft, must] Every change lands as a PR that a second agent verified; no direct pushes to main from builders. | gate: review
- K2 [draft, must] A repo is only "done" after local verification: build + health check green on this machine. | gate: review
- K3 [draft, must] Factory standard holds on every repo: clean .env.example, healthchecks, non-root nginx, guarded release-please, real README. | gate: review
- G1 [draft, must] Daily rotation keeps running: one repo per run audited, fixed, verified, merged. | gate: review
- G2 [draft, aim] Freebuff / OpenCode workers participate in the board as builders when their quota allows. | gate: review
