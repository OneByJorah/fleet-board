# fleet-board

Pullboard governance board for the OneByJorah agent fleet — spec, doctrine and lanes that live in git.

## What this is

fleet-board is the [Pullboard](https://pullboard.dev) board that governs how agents work across the OneByJorah fleet. Builders claim items in lane worktrees, a markdownlint gate runs at submit, and a different agent verifies the exact commit before anything is accepted — nothing ships unverified. The repo holds only the board's committed canon: the spec, the doctrine and the board configuration. Board state itself (items, claims, verdicts) lives in `.git/pullboard` and is never committed.

## Files

| File | Role |
| --- | --- |
| `SPEC.md` | Every requirement as a row with a permanent id (`G1`, `K1`, …); commits cite the ids they serve |
| `DOCTRINE.md` | House rules for agentic development, inheriting Pullboard standard doctrine |
| `pullboard.json` | Board configuration: gate command, lane layout, lease length, commit rules |
| `AGENTS.md` | Managed Pullboard guidance for agents working this board |
| `CLAUDE.md` | Pointer to `AGENTS.md` for Claude Code sessions |
| `.mcp.json` | Stdio MCP server so MCP clients can read the board and shout |

## Quick start

Requires Node 22+ and the global `pullboard` CLI (`npm i -g pullboard`).

```bash
# recover session state and see the next step
pullboard resume

# open the board UI
pullboard view

# claim the next free item
pullboard next
```

## How the board works

- **Lanes.** One agent per lane worktree, created from the main checkout with `pullboard worktree <lane>`. Each lane owns only its paths; the pre-commit gate refuses anything else.
- **Claims.** `pullboard next` atomically claims the next free item. A claim is a 2-hour lease; a quiet claimant auto-reopens its item.
- **Gate.** `pullboard submit <id>` requires a clean tree and a green gate at HEAD — here, markdownlint over the doc files.
- **Verification.** A different agent runs `pullboard next --verify`, checks out the submitted commit, and accepts or rejects with `pullboard verify <id>`. A builder never verifies its own work.
- **Spec rows.** Only approved rows bind. Ids are permanent: a row the person declines stays, marked `wont`.

## Doctrine highlights

- Never leave worktrees behind — a landed repo's local clone is removed the same day.
- Verified locally beats verified in CI: `docker compose up -d --build` + curl health is the acceptance gate for fleet repos.
- Keep the notification panel green; purge stale failed runs only after the fix has landed.
- The rotation cursor in `~/oneby-factory/daily-rotation-state.json` is updated in the same change that lands the work.

## Contributing

Board changes land as PRs; only a person approves spec rows and doctrine changes. Run the gate before pushing:

```bash
markdownlint-cli2 SPEC.md DOCTRINE.md AGENTS.md README.md
```

## Security

No secrets, credentials or sensitive data belong in this repo; the board database lives under `.git/pullboard` and is never committed. Report issues through the normal repository issue tracker.

## License

No license file yet — the board is maintained privately for the OneByJorah fleet.
