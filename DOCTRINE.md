# Doctrine

Our house rules for agentic development.

Inherits Pullboard standard doctrine version 1.

## W · Writing

## C · Code

## T · Tests

## P · Git and the gate

## D · Dependencies

## S · Security and data

## Fleet doctrine (jorahdev / OneByJorah)

- Never leave worktrees behind: a landed repo's local clone is removed the same day.
- Verified locally beats verified in CI: `docker compose up -d --build` + curl health is the acceptance gate.
- Keep the notification panel green: purge stale failed runs only after the fix has landed.
- Cursor state in ~/oneby-factory/daily-rotation-state.json is the rotation's source of truth; update it in the same change that lands the work.
