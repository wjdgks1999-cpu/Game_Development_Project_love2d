# 경기·성장 이벤트 계약

## 1. 목적과 권위

이 문서는 경기, 성장, 커리어, 커뮤니티 시스템이 같은 사건을 같은 코드와 필드로 주고받기 위한 구현 계약이다.

- 사건의 야구적 의미, 인과관계, 투수 책임은 `05_pitching_match_and_balance.md`가 결정한다.
- 공개 태그 이름과 공개 가능 범위는 `07_community_narrative_and_templates.md`가 결정한다.
- 저장·직렬화 원칙은 `09_technical_architecture_and_data.md`가 결정한다.
- 이 문서는 위 결정을 코드에서 일관되게 표현하는 방식을 소유하며, 원문 규칙을 바꾸지 않는다.

원문과 충돌하면 먼저 해당 권위 문서를 수정한 뒤 이 계약을 맞춘다. 새 필드와 이벤트 종류는 별도 표기가 없으면 `[가정]`이며 구현 중 조정할 수 있다.

## 2. 공통 이벤트 봉투

| 필드 | 형식 | 규칙 |
| --- | --- | --- |
| `event_id` | 문자열 | 저장 범위에서 고유한 ID |
| `event_type` | 열거형 | 3절의 값만 사용 |
| `sequence` | 정수 | 같은 실행에서 단조 증가하는 결정적 순번. 벽시계 시각으로 판정하지 않음 |
| `source` | 문자열 | 이벤트를 만든 시스템 ID |
| `match_id` | 문자열 또는 `null` | 경기 밖 사건이면 `null` |
| `plate_appearance_id` | 문자열 또는 `null` | 타석 밖 사건이면 `null` |
| `pitch_id` | 문자열 또는 `null` | 투구 밖 사건이면 `null` |
| `importance` | 정수 | `0`~`3` |
| `tags` | 문자열 배열 | 4절의 표준 태그 사용 |
| `responsibility` | 열거형 | 5절 참조 |
| `visibility` | 열거형 | 6절 참조 |
| `causes` | 배열 | 원인이 여러 개일 때 구조화해 보존 |
| `payload` | 객체 | 이벤트 종류별 실제 값. 확인되지 않은 사실을 생성하지 않음 |
| `rng_ref` | 문자열 또는 `null` | 재현에 필요한 난수 흐름 참조 |

`event_id`, `sequence`, `event_type`, `source`, `importance`, `tags`, `responsibility`, `visibility`, `causes`, `payload`는 필수다. 선택 필드가 해당되지 않으면 생략하지 말고 `null`을 사용한다. `[가정]`

## 3. 이벤트 종류

| `event_type` | 발생 시점 |
| --- | --- |
| `pitch_resolved` | 한 투구의 위치와 결과 확정 |
| `plate_appearance_ended` | 한 타석 종료 |
| `batted_ball_resolved` | 타구와 수비 결과 확정 |
| `runner_advanced` | 주자 진루 확정 |
| `run_scored` | 득점과 책임 확정 |
| `outing_ended` | 등판 종료 |
| `training_pitch_resolved` | 훈련 한 구 결과 확정 |
| `training_ended` | 훈련 점수와 보상 확정 |
| `quest_state_changed` | 퀘스트 상태 변경 |
| `career_state_changed` | 보직·콜업·강등·엔딩 상태 변경 |
| `community_bundle_created` | 공개 반응 묶음 생성 |
| `save_recovered` | 저장 복구 또는 재개 완료 |

위 목록은 현재 버티컬 슬라이스의 공통 교환 단위다. 더 세밀한 내부 신호는 외부 이벤트로 노출하지 않아도 된다. `[가정]`

## 4. 표준 태그 매핑

### 4.1 수비·타구·책임

| GDD 표현 | 표준 태그 |
| --- | --- |
| 정상 수비 | `normal_defense` |
| 실책 | `defensive_error` |
| 야수 선택 | `fielders_choice` |
| 수비 범위 부족 | `range_deficit` |
| 빗맞은 안타 | `bloop_hit` |
| 강한 타구 | `hard_contact` |
| 불운성 타구 | `bad_luck` |
| 타자의 좋은 대응 | `batter_good_response` |

`투수 실투에서 발생한 타구`는 결과 태그와 함께 실제 원인에 맞는 `release_mistake`, `location_miss`, `slider_hung` 중 하나 이상으로 기록한다. 근거가 없는데 포괄적인 실투 태그를 추가하지 않는다.

### 4.2 포수 사인

- 사인과 선택이 맞으면 `catcher_sign_matched`
- 사인과 선택이 다르면 `catcher_sign_mismatched`

두 태그는 `private` 전용이다. 공개 반응은 포수의 정확한 사인이나 플레이어의 내부 선택을 직접 밝히지 않는다.

### 4.3 커리어와 경기 태그

`07_community_narrative_and_templates.md`에 정의된 영문 태그가 표준 코드다. 아직 그 문서에 없는 새 의미가 필요하면 임의 문자열을 만들지 말고 권위 문서와 이 매핑을 함께 갱신한다.

## 5. 투수 책임

| 값 | 의미 |
| --- | --- |
| `pitcher_responsible` | 결과의 주된 책임이 투수에게 있음 |
| `pitcher_not_responsible` | 실책 등으로 투수 책임이 아님 |
| `not_applicable` | 책임 판정 대상이 아님 |

복합 원인을 억지로 한 값에 넣지 않는다. 최종 책임은 위 값으로 표시하고 세부 원인은 `causes`에 남긴다.

`pitcher_responsible` 또는 `pitcher_not_responsible`인 사건은 `07_community_narrative_and_templates.md`의 템플릿 필터와 호환되도록 같은 값을 `tags`에도 포함한다.

## 6. 공개 수준

| 값 | 사용 범위 |
| --- | --- |
| `public_fact` | 기사와 커뮤니티에 사실로 사용 가능 |
| `public_inference` | 커뮤니티의 추론형 표현에만 사용 가능 |
| `official_only` | 감독 등 공식 발언에만 사용 가능 |
| `private` | 비공개 대사와 개발 로그에만 사용 가능 |

상위 공개 수준으로 자동 승격하지 않는다. 여러 원인을 합친 출력은 포함된 정보 중 가장 제한적인 공개 수준을 따른다.

## 7. 생산자와 소비자

| 생산자 | 주요 이벤트 | 주요 소비자 |
| --- | --- | --- |
| 경기 판정 | 투구, 타석, 타구, 주자, 득점, 등판 | UI, 퀘스트, 커리어, 커뮤니티, 저장 |
| 훈련 | 훈련 투구, 훈련 종료 | 성장, 퀘스트, UI, 저장 |
| 퀘스트·커리어 | 상태 변경 | UI, 커뮤니티, 저장 |
| 커뮤니티 | 반응 묶음 생성 | 커뮤니티 UI, 저장 |
| 저장 복구 | 복구 완료 | UI, 진단 로그 |

소비자는 원본 이벤트를 고치지 않는다. 필요한 표시값은 별도 출력 모델로 변환한다.

## 8. 예시

아래 값은 구조를 설명하기 위한 예시이며 실제 콘텐츠나 확정 밸런스 값이 아니다.

```json
{
  "event_id": "event_pitch_example",
  "event_type": "pitch_resolved",
  "sequence": 42,
  "source": "match_resolution",
  "match_id": "match_example",
  "plate_appearance_id": "pa_example",
  "pitch_id": "pitch_example",
  "importance": 0,
  "tags": ["swinging_strike"],
  "responsibility": "not_applicable",
  "visibility": "public_fact",
  "causes": [],
  "payload": {"pitch_result": "swinging_strike"},
  "rng_ref": "match_rng_example"
}
```

```json
{
  "event_id": "event_run_example",
  "event_type": "run_scored",
  "sequence": 77,
  "source": "match_resolution",
  "match_id": "match_example",
  "plate_appearance_id": "pa_example",
  "pitch_id": "pitch_example",
  "importance": 2,
  "tags": ["defensive_error", "pitcher_not_responsible"],
  "responsibility": "pitcher_not_responsible",
  "visibility": "public_fact",
  "causes": [{"type": "fielding", "tag": "defensive_error"}],
  "payload": {"runs": 1},
  "rng_ref": "match_rng_example"
}
```

```json
{
  "event_id": "event_bundle_example",
  "event_type": "community_bundle_created",
  "sequence": 101,
  "source": "community_reaction",
  "match_id": null,
  "plate_appearance_id": null,
  "pitch_id": null,
  "importance": 3,
  "tags": ["recalled"],
  "responsibility": "not_applicable",
  "visibility": "public_fact",
  "causes": [{"event_id": "career_event_example"}],
  "payload": {"bundle_id": "bundle_example"},
  "rng_ref": "community_rng_example"
}
```

## 9. 검증 규칙

1. 같은 시드, 입력, 상태에서는 이벤트 순서와 판정 필드가 같아야 한다.
2. `pitch_id`가 있는 사건은 유효한 `plate_appearance_id`와 `match_id`를 가져야 한다.
3. 실책 득점은 근거 없이 `pitcher_responsible`이 될 수 없다.
4. `private` 정보는 공개 반응 입력으로 전달할 수 없다.
5. `payload`의 수치와 `tags`, `responsibility`가 서로 모순되면 생성 실패로 처리한다.
6. 존재하지 않은 구종, 기록, 선수, 구단을 이벤트 보정 과정에서 만들지 않는다.
7. 저장 후 복구한 이벤트는 기존 `event_id`와 `sequence`를 유지한다.
8. 필수 필드 누락과 알려지지 않은 열거형 값은 조용히 대체하지 않고 오류로 기록한다.
