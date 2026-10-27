# DD-0001: 경기 중단 시 현재 타자 시작으로 복귀

- 상태: 승인됨
- 날짜: 2026-08-09
- 권위 문서: `docs/game_design/04_player_experience_and_core_loop.md#14-모바일-체크포인트`
- 사용자 승인 근거: 현재 작업에서 현재 타자 시작 시점으로 통일하는 권장안 승인
- 대체하는 결정: 없음

## 변경

- 이전: 등판 중 앱이 중단되면 해당 등판 시작 지점으로 복귀한다.
- 이후: 등판 중 앱이 중단되면 현재 타자 시작 지점으로 복귀한다. 완료된 이전 타자의 결과는 유지한다.

## 이유와 증거

- 플레이테스트 또는 자동 검증: 아직 없음. 문서 일관성 감사에서 복귀 지점 충돌을 확인했다.
- 변경 이유: `08_mobile_ui_art_and_audio.md`, `09_technical_architecture_and_data.md`, `10_implementation_guide_and_acceptance.md`가 모두 현재 타자 시작 복귀를 요구한다. 같은 기준으로 통일하면 완료된 이전 타자를 반복하지 않으면서 진행 중인 투구를 확정하지 않는 복구 계약을 유지할 수 있다.

## 영향

- 함께 확인할 소비 문서: `docs/game_design/08_mobile_ui_art_and_audio.md`, `docs/game_design/09_technical_architecture_and_data.md`, `docs/game_design/10_implementation_guide_and_acceptance.md` — 현재 결정과 이미 일치한다.
- 구현 및 재검증 범위: 현재 타자 시작 스냅샷, 완료된 이전 타자 결과 보존, 동일 난수 상태 복구, 경기 중단·복귀 자동 테스트와 실제 Android 기기 복귀 검증.
