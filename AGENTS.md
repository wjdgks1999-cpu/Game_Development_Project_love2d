# Game Development Workflow

Use Superpowers as the default design, planning, TDD, review, and verification process. Do not modify or duplicate its skills.

Every implementation plan must include:

```markdown
## [NEW] 게임 작업 확인

- 에셋: 없음 / 임시 에셋 사용 / 실제 에셋 필요
- 직접 플레이 확인: 필요 / 불필요
- 공통 기반 변경: 필요 / 불필요
```

- In the implementation plan's ordinary prose, state:
  - the vertical-slice play segment and core experience this feature supports;
  - the target quality: final or temporary;
  - whether completed play segments require integration revalidation.
- Use `game-asset-specification` only when the asset value is `임시 에셋 사용` or `실제 에셋 필요`.
- Use `human-playtest` only when direct play confirmation is `필요`, at the planned playable point.
- The user performs the playtest; Codex prepares at most three checks and records the user's results.
- Continue with temporary assets whenever they are sufficient.
- Route fixes through a new Superpowers plan and TDD cycle.
- Do not extract one-off game code into a common foundation.
- Do not proceed to the next approved project stage without explicit user approval.

## GDD Management

- Read `docs/game_design/INDEX.md` before game-design or implementation work.
- For initial project understanding or cross-cutting scope changes, read all current GDDs listed by the index. For feature work, also read the core and authoritative documents selected by the index.
- Treat the index as a routing map, not as a replacement for the authoritative GDDs.
- Treat GDDs as specifications, not as evidence that code, builds, tests, or validation are complete.
- Do not use `docs/game_design/archive/` as current requirements.
- Preserve existing design-status markers until a user decision or verification evidence changes their status.
- Resolve duplicated rules through the authoritative owner listed in the index. If ownership does not resolve a conflict, ask the user instead of guessing.
- After an approved important design change, record its reason in `docs/game_design/decisions/` and update the authoritative GDD before implementation. This uses the existing design approval gate and does not add a new gate.
