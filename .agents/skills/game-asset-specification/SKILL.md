---
name: game-asset-specification
description: Use when an approved game task needs images, animation, UI visuals, sound, music, or defined placeholder dimensions and roles before implementation.
---

# Game Asset Specification

Specify only the assets needed by the current feature. This skill does not generate image or audio files and does not replace Superpowers design or planning.

## Entry condition

Read the implementation plan's `[NEW] 게임 작업 확인` first.

- `없음`: stop; do not create an asset document.
- `임시 에셋 사용`: describe the smallest placeholders that let implementation and verification continue.
- `실제 에셋 필요`: preserve the approved value; describe the required deliverables and separate the work blocked on actual assets from the work that can continue with placeholders.

Do not downgrade an approved `실제 에셋 필요` to `임시 에셋 사용` merely because some implementation can proceed with placeholders. Any change to the approved value requires a revised Superpowers plan and user approval.

## Procedure

1. Read the approved feature design and list only assets used by that feature.
2. Group files and variants that share one purpose, asset type, source identity, and acceptance target into one asset group.
3. Use one `docs/assets/<feature>.md` document by default. Different deliverables or independent approval and QA requirements are demonstrated reasons to split groups into `docs/assets/<feature>-<asset-group>.md`. Never create one document per individual file or variant.
4. Remove optional fields and conditional sections that do not apply.
5. Preserve the approved asset value and fill both `막힌 범위` and `계속 가능한 범위`. Write `없음` when either scope is empty.
6. For character or animation groups, complete the applicable production contract section without inventing missing values.

## Document format

```markdown
# 에셋 그룹 이름

## 범위 판단

- 승인된 에셋 상태: 임시 에셋 사용 / 실제 에셋 필요
- 막힌 범위:
- 계속 가능한 범위:

## 공통 명세

- 에셋 그룹 ID:
- 목적:
- 사용 화면:
- 파일 경로:
- 종류: 이미지 / 애니메이션 / UI / 효과음 / 음악
- 크기:
- 파일 형식:
- 그림 또는 소리의 분위기:
- 반드시 포함할 내용:
- 포함하면 안 되는 내용:
- 필요한 변형:
- 입력 자료·출처·사용 권리:
- 생성 AI에 전달할 설명:
- 실제 사용 크기 검증 방법:
- 완료 기준:

## 캐릭터 계약

캐릭터가 포함될 때만 작성한다.

- 정체성:
- 신체 비율:
- 얼굴·머리:
- 의상·팔레트:
- 숫자·표식:
- handedness·비대칭 장비:

## 애니메이션 계약

애니메이션이 포함될 때만 작성한다.

- 카메라:
- 시작 자세:
- 종료 자세:
- 동작 의미와 필수 키포즈:
- 프레임·시간 목표:
- 루프 여부:
- 피벗·발 기준선:
```

Keep the approved asset status, both scope fields, asset group ID, purpose, use screen, file path, type, file format, input rights, and completion criteria.

For visual, UI, or animation groups, also keep `크기` and `실제 사용 크기 검증 방법`. Record the intended display area or target size at the project's 1280×720 logical resolution. If the final render or cell size depends on later measurement, preserve it as `[검증 필요]` instead of deciding it for tool convenience.

Always fill `입력 자료·출처·사용 권리`. Write `없음 — 신규 제작` when no external input is used. If rights are unresolved, preserve `[검증 필요]` and include the affected work in `막힌 범위`.

Delete the character or animation contract only when that contract does not apply.

## Guardrails

- Do not stop unaffected work merely because final assets are unavailable; isolate the blocked scope without changing the approved asset value.
- Do not generate assets or invoke an asset generator unless the user separately requests it.
- Do not add game rules, UI behavior, or implementation steps to the asset document.
- Do not create multiple asset documents for one screen or feature unless different deliverables or independent approval and QA requirements demonstrate the need.
- Do not create one document per individual file or variant.
- Preserve `[미정]`, `[가정]`, and `[검증 필요]`; do not invent missing production-contract values.
- Use project-relative file paths. Do not request output outside the project.
- Do not preselect a final render or sprite cell size before the 1280×720 display target and validation method are defined.
- Do not add generator names, workflow gates, call counts, credits, manifest fields, hashes, or production steps. The external asset workflow owns routing, execution, snapshots, and result records.