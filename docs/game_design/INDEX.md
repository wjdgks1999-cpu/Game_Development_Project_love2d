# GDD Index

## 1. 목적

이 문서는 현재 유효한 게임 디자인의 진입점, 문서 트리, 읽기 경로, 소유권을 안내한다. 게임 규칙의 실제 값과 동작은 아래 표의 권위 문서가 소유하며, 이 문서는 그 규칙을 다시 정의하지 않는다.

## 2. 유효 범위

- `00_project_charter.md`부터 `10_implementation_guide_and_acceptance.md`까지가 현재 권위 GDD다.
- `contracts/`는 권위 GDD를 코드로 옮길 때 필요한 세부 형식과 계산 순서를 정의한다.
- `content/CONTENT_REQUIREMENTS.md`는 실제 콘텐츠의 준비 상태와 구현 차단 조건을 관리한다.
- `VALIDATION_MATRIX.md`는 검증 목표, 상태, 통과 기준, 증거를 관리한다.
- `decisions/`는 승인된 중요 설계 변경의 이유와 영향을 기록한다.
- `archive/`의 문서는 과거 참고 자료이며 현재 사양으로 사용하지 않는다.

## 3. 문서 트리

```text
docs/game_design/
├─ INDEX.md
├─ 00_project_charter.md
├─ 01_game_vision.md
├─ 02_protagonist_and_career_structure.md
├─ 03_vertical_slice_definition.md
├─ 04_player_experience_and_core_loop.md
├─ 05_pitching_match_and_balance.md
├─ 06_progression_quest_and_career.md
├─ 07_community_narrative_and_templates.md
├─ 08_mobile_ui_art_and_audio.md
├─ 09_technical_architecture_and_data.md
├─ 10_implementation_guide_and_acceptance.md
├─ VALIDATION_MATRIX.md
├─ contracts/
│  ├─ 01_match_resolution_contract.md
│  ├─ 02_game_event_contract.md
│  └─ 03_community_content_schema.md
├─ content/
│  └─ CONTENT_REQUIREMENTS.md
├─ decisions/
│  ├─ README.md
│  ├─ 0001-resume-from-current-batter.md
│  └─ 0002-add-implementation-contract-documents.md
└─ archive/
   └─ README.md
```

## 4. 읽기 경로

### 프로젝트 최초 파악 또는 전체 범위 변경

1. `INDEX.md`를 읽는다.
2. `00`부터 `10`까지 권위 GDD 전체를 읽는다.
3. `content/CONTENT_REQUIREMENTS.md`에서 현재 미정·미준비 항목을 확인한다.
4. `VALIDATION_MATRIX.md`에서 아직 증명되지 않은 목표를 확인한다.
5. 구현 세부사항이 필요한 단계에서만 관련 `contracts/` 문서를 읽는다.

### 개별 기능 설계·계획·구현

1. `INDEX.md`를 읽는다.
2. `00_project_charter.md`, `01_game_vision.md`, `03_vertical_slice_definition.md`, `10_implementation_guide_and_acceptance.md`를 확인한다.
3. 아래 소유권 표에서 현재 기능의 권위 GDD를 읽는다.
4. 권위 GDD의 관련 절이 안내하는 계약·콘텐츠·검증 문서를 읽는다.
5. 과거 결정의 이유가 필요할 때만 `decisions/`를 읽는다.

### 작업별 빠른 경로

| 작업 | 필수 세부 문서 |
| --- | --- |
| 투구·타격·수비·프롤로그 예외·훈련 점수 | `contracts/01_match_resolution_contract.md` |
| 경기·성장·커리어 사건, 로그, 저장 교환 | `contracts/02_game_event_contract.md` |
| 기사·게시글·댓글·발언 데이터 | `contracts/03_community_content_schema.md` |
| 인물·구단·타자·텍스트·아트·오디오 준비 | `content/CONTENT_REQUIREMENTS.md` |
| 테스트 계획·게이트 판정·증거 기록 | `VALIDATION_MATRIX.md` |

## 5. 상태 표기 처리

| 표기 | AI와 구현 작업의 처리 |
| --- | --- |
| `[확정]` | 권위 문서대로 구현한다. 변경하려면 승인 절차를 거친다. |
| `[가정]` | 프로토타입에 사용할 수 있지만 조정 가능한 값으로 분리하고 최종안처럼 단정하지 않는다. |
| `[미정]` | 임의로 결정하지 않는다. 구현에 꼭 필요하면 작업을 멈추고 사용자 결정을 요청한다. |
| `[검증 필요]` | 가설로 구현할 수 있으나 `VALIDATION_MATRIX.md`의 증거 없이 해당 최종 게이트를 통과시키지 않는다. |
| `[제외]` | 버티컬 슬라이스에 구현하지 않는다. |
| `[전체 게임]` | 장기 확장 범위이며 현재 구현에 넣지 않는다. |
| `[삭제 후보]` | 승인된 범위 축소 전까지 유지한다. |

별도 표기가 없는 규범 문장은 해당 권위 문서의 현재 규칙으로 적용한다. 다만 문서에 없는 새 수치, 콘텐츠, 예외 분기를 확정하라는 뜻으로 해석하지 않는다.

## 6. 문서 소유권

| 문서 | 소유하는 설계 | 소유하지 않는 내용 |
| --- | --- | --- |
| `00_project_charter.md` | 프로젝트 목표, 제작 제약, 최상위 성공 기준, 범위 축소 원칙 | 세부 시스템 수치와 구현 방식 |
| `01_game_vision.md` | 핵심 판타지, 경험 기둥, 목표 감정, 기능 추가·제거 판단 | 버티컬 슬라이스의 세부 장면과 판정식 |
| `02_protagonist_and_career_structure.md` | 주인공 설정, 경력, 약점, 구단 내 역할과 세계관적 커리어 근거 | 퀘스트 수치와 경기 판정 |
| `03_vertical_slice_definition.md` | 시작·종료 지점, 포함·제외 범위, 품질 경계, 버티컬 슬라이스 완료 기준 | 세부 경기 공식과 코드 구조 |
| `04_player_experience_and_core_loop.md` | 장면 순서, 플레이 흐름, 루프 연결, 체크포인트와 재시도 경험 | 세부 성장량과 투구 판정식 |
| `05_pitching_match_and_balance.md` | 투구 조작, 경기 판정, 타자·수비, 투수 책임, 밸런스와 프롤로그 예외 의미 | 커리어 분기와 공개 반응 문장 |
| `06_progression_quest_and_career.md` | 능력치, 훈련·휴식, 퀘스트, 패시브, 콜업과 엔딩 분기 규칙 | 투구 물리와 커뮤니티 템플릿 |
| `07_community_narrative_and_templates.md` | 공개 정보, 사건 태그 이름, 커뮤니티 규칙·문체·수량·선택 원칙 | 경기 결과와 커리어 판정 변경 |
| `08_mobile_ui_art_and_audio.md` | 모바일 UI, 화면 표현, 아트·애니메이션·사운드·에셋 품질 | 경기 확률과 성장 판정 |
| `09_technical_architecture_and_data.md` | 모듈 경계, 데이터 원칙, 난수, 저장·로그·자동 테스트 구조 | 게임 디자인 수치와 경험 목표 |
| `10_implementation_guide_and_acceptance.md` | 구현 의존 관계, 게이트, 종단 간 수용 검사와 문서·코드 대응 | 다른 권위 문서가 소유한 원본 수치 |
| `contracts/01_match_resolution_contract.md` | 판정 계산 순서, 좌표·단위, 구현 공식, 프롤로그 예외 절차, 테스트 벡터 | 경기 목표와 최종 튜닝 값 |
| `contracts/02_game_event_contract.md` | 공통 이벤트 필드, 코드, 열거형, 태그 매핑 | 사건의 야구적 의미와 공개 정책 |
| `contracts/03_community_content_schema.md` | 채널별 필드, 댓글 관계, 렌더링 출력 구조 | 실제 문구, 선택 원칙, 안전 정책 |
| `content/CONTENT_REQUIREMENTS.md` | 콘텐츠 목록, 준비 상태, 구현 차단 조건 | 실제 최종 콘텐츠와 설정 승인 |
| `VALIDATION_MATRIX.md` | 통합 검증 상태, 방법, 통과 기준, 증거, 차단 게이트 | 기대 동작 자체와 게임 규칙 |

## 7. 교차 규칙 소유권

같은 주제가 여러 문서에 등장해도 각 문서는 서로 다른 사실을 소유한다.

| 교차 주제 | 권위 문서 | 세부 계약·소비 문서 |
| --- | --- | --- |
| 첫 1군 등판만 고정 실패라는 범위 | `03_vertical_slice_definition.md` | `01`, `02`, `04`, `10` |
| 고정 실패의 경기 의미와 조건 | `05_pitching_match_and_balance.md` | `contracts/01`, `04`, `09`, `10` |
| 프롤로그 제약의 코드 격리 | `09_technical_architecture_and_data.md` | `contracts/01`, `10` |
| Android·가로·1280×720 프로젝트 제약 | `00_project_charter.md` | `03`, `08`, `09`, `10` |
| 화면 배치와 안전 영역 | `08_mobile_ui_art_and_audio.md` | `05`, `09`, `10` |
| 투수 책임의 야구적 판정 | `05_pitching_match_and_balance.md` | `contracts/02`, `06`, `07`, `09`, `10` |
| 사건 태그 이름과 공개 수준 | `07_community_narrative_and_templates.md` | `contracts/02`, `09`, `10` |
| 훈련·휴식·성장·퀘스트 수치 | `06_progression_quest_and_career.md` | `contracts/01`, `03`, `04`, `09`, `10` |
| 커뮤니티 규칙과 실제 반응 | `07_community_narrative_and_templates.md` | `contracts/03`, `03`, `04`, `09`, `10` |
| 콘텐츠 수량과 품질 요구 | 각 기능 권위 GDD | `content/CONTENT_REQUIREMENTS.md` |
| 기대 동작과 성공 기준 | 각 기능 권위 GDD | `VALIDATION_MATRIX.md` |

새 설계 변경부터 소비 문서에 원본 값을 추가로 복제하지 않고 권위 문서의 해당 절을 참조한다. 기존 반복 내용은 별도 감사와 사용자 승인 없이 일괄 수정하지 않는다.

## 8. 충돌 처리

다음 우선순위를 사용한다.

1. 현재 대화에서 사용자가 명시적으로 승인한 최신 결정
2. `decisions/`에 기록되고 권위 GDD에 반영된 승인 결정
3. 이 문서가 지정한 기능 권위 GDD
4. 권위 GDD와 일치하는 범위의 구현 계약
5. 앞선 비전·흐름 문서
6. `10_implementation_guide_and_acceptance.md`
7. 구현 과정에서 세운 가정

계약 문서가 권위 GDD와 충돌하면 계약을 우선하지 않는다. 먼저 권위 GDD의 올바른 의미를 확인하고 계약을 갱신한다. 소유권으로도 해결되지 않는 충돌은 임의로 판단하지 않고 사용자에게 확인한다.

## 9. 설계 변경 순서

이 순서는 기존 설계 승인 게이트 안에서 수행하며 새로운 승인 게이트를 추가하지 않는다.

1. 변경 대상과 권위 GDD를 확인한다.
2. 사용자와 설계 변경을 검토하고 기존 방식대로 승인을 받는다.
3. 중요 변경이면 `decisions/`에 변경 이유와 영향을 기록한다.
4. 권위 GDD를 수정한다.
5. 관련 `contracts/`, `content/`, `VALIDATION_MATRIX.md`를 갱신한다.
6. 소비 문서의 중복 값은 제거하거나 권위 문서 참조로 바꾼다.
7. 문서 트리나 소유권이 바뀐 경우에만 `INDEX.md`를 수정한다.
8. 폐기된 별도 설계안에 장기 참고 가치가 있을 때만 `archive/`로 이동한다.

결정 기록이 필요한 변경의 기준과 형식은 `decisions/README.md`를 따른다.
