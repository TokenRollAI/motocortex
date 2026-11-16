# DOD template

Define falsifiable acceptance mapped to `VISION.md`. Group by milestone only when real dependency or release gates warrant it.

<dod-template>
# DOD (Definition of Done)

## Acceptance contract

Check an item only when observed evidence proves it on the current code state; link that evidence in `PROGRESS.md`. Reopen any item whose blast radius is touched by later edits until re-verified.

## Global gates

- [ ] `G-1`: <final-state build, typecheck, lint, required regression suite, or explicit human sign-off>

## Acceptance items

- [ ] `DOD-1` (`SC-1`, `UC-1`): <expected runtime behavior | exact command, live procedure, or review | prerequisites if any>

## End-to-end verification

- [ ] `E2E-1` (`UC-1`..`UC-n`): <full-path scenario exercised across real boundaries and expected observable result>
</dod-template>
