# 콘텐츠 준비 요구사항

## 1. 목적

이 문서는 버티컬 슬라이스에 필요한 인물, 구단, 타자, 텍스트, 이미지, 오디오의 준비 상태와 구현 차단 조건을 한곳에서 관리한다. 실제 콘텐츠의 설정·문구·파일을 대신하지 않는다.

- 수량과 사용 규칙의 권위는 각 GDD 원문에 있다.
- `[미정]` 항목은 AI가 임의로 확정하지 않는다.
- 승인된 실제 데이터나 에셋이 들어오면 상태와 증거 위치만 갱신한다.

## 2. 상태와 게이트

상태는 `미정`, `준비 전`, `제작 중`, `검수 대기`, `승인됨` 중 하나를 사용한다. 게이트 문자는 `10_implementation_guide_and_acceptance.md`의 구현 게이트를 따른다.

| ID | 산출물 | 요구 수량·조건 | 현재 상태 | 필요한 게이트 | 권위 문서 |
| --- | --- | --- | --- | --- | --- |
| CNT-CHAR-001 | 주인공 이름 | 게임 내 일관된 이름 1개 | 미정 | G, H, J | `02_protagonist_and_career_structure.md` |
| CNT-CHAR-002 | 주인공 외형 기준 | 전신 SD와 초상화가 공유할 외형 | 미정 | J | `02_protagonist_and_career_structure.md`, `08_mobile_ui_art_and_audio.md` |
| CNT-TEAM-001 | 소속 구단 | 한강 파이오니어스 | 승인됨 | G, H, J | `02_protagonist_and_career_structure.md` |
| CNT-TEAM-002 | 상대 구단 구성 | 각 경기 설정에 필요한 구단명·표식 | 미정 | D, E, H | `02_protagonist_and_career_structure.md`, `05_pitching_match_and_balance.md` |
| CNT-BAT-001 | 프롤로그 타자 세트 | 프롤로그 등판을 완주할 타자 데이터 | 준비 전 | D, E | `03_vertical_slice_definition.md`, `05_pitching_match_and_balance.md` |
| CNT-BAT-002 | 2군 타자 세트 | 2군 경기와 퀘스트 검증용 타자 데이터 | 준비 전 | D, E, G | `05_pitching_match_and_balance.md`, `06_progression_quest_and_career.md` |
| CNT-BAT-003 | 최종 타자 세트 | 프롤로그와 다른 최종 시험 구성 | 준비 전 | D, E, G | `03_vertical_slice_definition.md`, `05_pitching_match_and_balance.md` |
| CNT-PITCH-001 | 구종 데이터 | 포심, 슬라이더, 체인지업 | 승인됨 | C | `05_pitching_match_and_balance.md` |
| CNT-TEXT-001 | 커뮤니티 템플릿 | 권위 문서 14절 구성 전체를 포함한 초기 80개 | 준비 전 | H | `07_community_narrative_and_templates.md` |
| CNT-TEXT-002 | 주요 대사·공식 발언 | 위 80개 중 권위 문서에 열거된 8개 장면 | 준비 전 | G, H | `07_community_narrative_and_templates.md` |
| CNT-ART-001 | 주인공 표정 초상화 | 표에 정의된 총 13개 표정 변형 | 준비 전 | J | `08_mobile_ui_art_and_audio.md` |
| CNT-ART-002 | 주요 배경 | 문서에 정의된 주요 배경 4종 | 준비 전 | J | `08_mobile_ui_art_and_audio.md` |
| CNT-ART-003 | 전신 SD | 주인공, 좌타자, 우타자 | 준비 전 | J | `08_mobile_ui_art_and_audio.md` |
| CNT-ART-004 | 경기 시각 에셋 | 구종, 공 궤적, 타구, 수비 결과 표현 | 준비 전 | E, J | `08_mobile_ui_art_and_audio.md` |
| CNT-ART-005 | UI 에셋 | 버튼, 아이콘, 상태 표시, 커뮤니티 화면 요소 | 준비 전 | B, J | `08_mobile_ui_art_and_audio.md` |
| CNT-AUDIO-001 | 사용자 제공 오디오 | BGM, 효과음, 환경음, 햅틱 연동 목록 | 준비 전 | J | `08_mobile_ui_art_and_audio.md` |

상대 구단과 타자 수처럼 원문이 확정하지 않은 수량은 여기서 새로 정하지 않는다. 경기 구성과 테스트 케이스가 확정될 때 필요한 항목을 추가한다.

## 3. 구현 차단 규칙

- `[미정]`인 이름, 외형, 구단 설정을 최종 데이터로 만들지 않는다.
- 콘텐츠가 없어도 구조 개발이 가능한 경우에는 명확한 임시 ID와 테스트 데이터만 사용한다.
- 임시 데이터는 화면, 빌드, 로그에서 최종 승인 콘텐츠처럼 표시하지 않는다.
- 특정 게이트의 판정에 실제 문구나 에셋이 필요하면 해당 항목이 `승인됨`이 될 때까지 그 게이트를 통과 처리하지 않는다.
- AI가 임시 값을 제안할 수 있는 것은 작업 지시가 명시적으로 허용한 경우뿐이며, 제안과 승인은 분리한다.

## 4. 항목 완료 조건

각 항목을 `승인됨`으로 바꾸려면 다음 정보를 함께 기록한다.

1. 실제 파일 또는 데이터의 위치
2. 승인한 기준 문서와 버전 또는 결정 기록
3. 누락·중복·금지 표현 검사 결과
4. 관련 게이트에서 사용할 검증 증거 위치
