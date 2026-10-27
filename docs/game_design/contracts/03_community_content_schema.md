# 커뮤니티 콘텐츠 스키마

## 1. 목적과 권위

이 문서는 기사, 게시글, 댓글, 공식 발언, 비공개 대사를 데이터로 작성하고 출력하는 형식을 정의한다.

- 반응 규칙, 공개 범위, 문체, 선택 순서, 수량은 `07_community_narrative_and_templates.md`가 결정한다.
- 입력 사건과 표준 태그는 `02_game_event_contract.md`를 따른다.
- 이 문서는 필드, 관계, 출력 구조를 소유하며 실제 문구를 확정하지 않는다.

아래에서 원문에 직접 없는 구조 보완은 `[가정]`이며 콘텐츠 제작과 구현 검증 중 조정할 수 있다.

## 2. 템플릿 공통 구조

| 필드 | 형식 | 규칙 |
| --- | --- | --- |
| `template_id` | 문자열 | 고유하고 변경에 안정적인 ID |
| `channel` | 열거형 | 3절 참조 |
| `event_family` | 문자열 | 사건 묶음 |
| `persona` | 문자열 | 팬 성향 또는 화자 ID |
| `tone` | 열거형 | `positive`, `negative`, `neutral` |
| `required_tags` | 문자열 배열 | 모두 있어야 선택 가능 |
| `optional_tags` | 문자열 배열 | 있으면 가중치 상승 |
| `forbidden_tags` | 문자열 배열 | 하나라도 있으면 선택 금지 |
| `allowed_opinion_stages` | 문자열 배열 | 허용 여론 단계 |
| `minimum_importance` | 정수 | 사건 중요도 최솟값 |
| `required_slots` | 문자열 배열 | 렌더링 전 반드시 존재 |
| `weight` | 수치 | 기본 선택 가중치 |
| `cooldown` | 정수 | 재사용 대기 반응 횟수 |
| `semantic_group` | 문자열 | 유사 의미 중복 방지 그룹 |
| `safety_class` | 열거형 | `general`, `mockery`, `sensitive` |
| `payload` | 객체 | 채널별 본문 구조 |

`text` 한 필드로 저장한 기존 초안은 읽기 단계에서 채널별 `payload`로 변환할 수 있다. 새 데이터는 `payload`를 사용한다. `[가정]`

## 3. 채널별 구조

| `channel` | `payload` 필드 | 설명 |
| --- | --- | --- |
| `article` | `title`, `summary` | 기사 제목과 요약 |
| `post` | `body` | 커뮤니티 원문 |
| `comment` | `body`, `parent_selector` | 댓글 본문과 부모 출력 선택 규칙 |
| `official_statement` | `speaker_id`, `body`, `sequence_group`, `sequence_order` | 공식 발언과 순서 |
| `private_dialogue` | `speaker_id`, `body`, `sequence_group`, `sequence_order` | 비공개 대사와 순서 |

`private_dialogue`는 공개 커뮤니티 출력이 아니며 `private` 사건만 다룰 수 있는 별도 소비 경로다. `[가정]`

## 4. 출력 구조

```text
ReactionOutput
- output_id
- bundle_id
- template_id
- parent_output_id
- rendered_title
- rendered_summary
- rendered_body
- slot_values
- display_order
- read_state
```

- 댓글의 `parent_selector`는 선택 전 규칙이고, 생성 후에는 실제 `parent_output_id`로 고정한다.
- 해당되지 않는 렌더링 필드는 `null`로 둔다.
- `slot_values`에는 렌더링에 실제 사용한 검증값만 보관한다.
- `read_state`는 표시 계층의 상태이며 템플릿 선택 결과를 바꾸지 않는다. `[가정]`

## 5. 슬롯 규칙

허용 슬롯은 `07_community_narrative_and_templates.md`의 목록만 사용한다.

1. 구조화되고 검증된 값만 삽입한다.
2. 필수 슬롯이 없으면 해당 후보를 제외한다.
3. 선수, 구단, 기록, 구종, 경기 결과를 새로 만들어 채우지 않는다.
4. 내부 능력치, 입력 등급, 정확한 목표점·실제점, 포수의 정확한 사인은 공개 슬롯으로 제공하지 않는다.
5. 한국어 조사는 검증된 조사 선택 함수 또는 조사 포함 슬롯으로 처리한다.
6. 자유 입력 문장을 슬롯으로 전달하지 않는다.

## 6. 선택과 안전 규칙

- `required_tags`, `forbidden_tags`, 공개 수준, 여론 단계, 중요도, 필수 슬롯을 모두 검사한 뒤 가중치를 적용한다.
- 같은 로그와 전용 난수 시드에서는 같은 후보와 출력 순서를 재현한다.
- 최근 사용한 `template_id`와 `semantic_group`은 쿨다운 규칙으로 반복을 줄인다.
- 전용 후보가 없으면 사실을 만들지 않는 안전한 폴백을 사용한다.
- `sensitive` 콘텐츠는 권위 문서가 허용한 사건과 문맥에서만 사용한다.
- 출력 후 기록, 책임, 공개 범위, 금지 표현을 다시 검증한다.

## 7. 구조 예시

다음은 스키마 확인용 임시 예시다. 실제 게임 문구나 승인된 콘텐츠가 아니며, 채널 차이와 무관한 공통 필드는 일부 생략했다.

```yaml
template_id: article_example_001
channel: article
required_tags: [recalled]
required_slots: [player_name, team_name]
payload:
  title: "{player_name} 관련 임시 제목"
  summary: "{team_name} 관련 임시 요약"
```

```yaml
template_id: post_example_001
channel: post
payload:
  body: "검증된 사건만 언급하는 임시 게시글"
```

```yaml
template_id: comment_example_001
channel: comment
payload:
  body: "부모 글의 확인된 내용에 반응하는 임시 댓글"
  parent_selector: "same_event_post"
```

```yaml
template_id: official_example_001
channel: official_statement
payload:
  speaker_id: manager_placeholder
  body: "확인된 결과만 언급하는 임시 공식 발언"
  sequence_group: result_statement
  sequence_order: 1
```

```yaml
template_id: private_example_001
channel: private_dialogue
payload:
  speaker_id: catcher_placeholder
  body: "비공개 정보용 임시 대사"
  sequence_group: mound_dialogue
  sequence_order: 1
```

## 8. 콘텐츠와 스키마의 경계

초기 템플릿 80개와 주요 대사·공식 발언의 실제 문구는 런타임 콘텐츠 데이터로 작성한다. 준비 상태와 필요한 수량은 `../content/CONTENT_REQUIREMENTS.md`에서 관리한다. 이 문서는 문구를 대신하지 않으며 예시를 최종 콘텐츠로 사용하지 않는다.
