---
name: human-playtest
description: Use when an approved game plan requires direct feature or integration play confirmation for controls, UI, animation, sound, difficulty, pacing, rewards, dialogue, story, or connected flow and the planned playable point has been reached.
---

# Human Playtest

Prepare a focused playtest for the user and turn the user's observations into actionable records. Codex does not perform or infer the human experience check.

## Entry condition

Read the implementation plan's `[NEW] 게임 작업 확인` first.

- `불필요`: stop; do not create a playtest document.
- `필요`: continue only at the execution point named in the plan.

Identify the approved play level before preparing checks:

- `기능 플레이`: focus on the current feature and record it in `docs/playtests/<feature>.md`.
- `통합 플레이`: cover the vertical slice's defined start-to-end flow and record each session in `docs/playtests/vertical-slice-<milestone>.md`.

## Readiness gate

The planned play scope is ready only when all are true:

- The game launches.
- The user can reach the feature.
- The required input can be performed.
- The screen or sound being judged is present.
- For `통합 플레이`, the defined start, end, representative route, and current session purpose are named.

If any condition is false, move the playtest to the nearest planned playable milestone. Do not mark it passed or failed.

## Procedure

1. Determine whether the approved scope is `기능 플레이` or `통합 플레이`, and state the current session purpose.
2. Derive no more than three checks for the current session from the approved goal.
3. If `통합 플레이` needs more than three checks, split it into separate sessions. Give each session one purpose, no more than three checks, and a separate session record in `docs/playtests/vertical-slice-<milestone>.md`.
4. Phrase each check around an observable input, presentation, or result.
5. Write the pending check sheet to the path required by the selected play level.
6. Ask the user to play and report what happened for each check in the current Codex chat. Tell the user not to edit the playtest document; Codex records the user's results there.
7. Record only the user's result; never invent or infer a pass.
8. Convert vague feedback into a concrete observation by asking what input, screen, sound, or result caused it.
9. If a feature change is needed, return to a new Superpowers correction plan and TDD cycle.

## Document format

```markdown
# 직접 플레이 확인 결과

- 플레이 수준: 기능 플레이 / 통합 플레이
- 대상: 기능 이름 / 마일스톤
- 세션 목적:
- 시작 지점: 통합 플레이에서만 작성
- 종료 지점: 통합 플레이에서만 작성
- 실행 시점:
- 상태: 확인 대기 / 완료 / 수정 필요

| 항목 | 결과 | 확인 내용 |
|---|---|---|
| | 통과 / 문제 있음 / 확인 대기 | |

## 수정할 내용

- 없음
```

Use at most three table rows. Replace `없음` only with concrete, actionable issues supported by the user's observations.

## Overall integration-play completion

A single integration session may be complete without completing the overall integration play. Mark the overall integration play complete only when all are true:

- The user has played the representative scenario from the defined start to the defined end.
- Every planned integration session has been recorded.
- Important findings have been resolved or explicitly accepted by the user.
- The user has approved the integration-play result.

Overall integration-play completion is evidence for vertical-slice completion; it does not replace the approved project completion criteria.

## Guardrails

- Do not run after every small code change.
- Do not ask broad questions such as `재미있는가?` or record `이상하다` without details.
- Do not treat automated tests as a substitute for the user's play result.
- Do not infer overall integration completion from feature-play results, automated tests, or only a subset of the planned integration sessions.
- Do not modify the game directly from playtest feedback; plan the correction first.
