# LLM Wiki 스키마 (단일 계약)

이 문서는 본 디렉터리에서 **LLM이 지켜야 하는 형식과 역할**을 정의한다. Karpathy의 LLM wiki 패턴을 따른다: 원문은 보존하고, **컴파일된 지식은 `pages/` 아래 마크다운**에만 둔다.

**주인장의 목적·톤**은 형식이 아니라 [`INTENT.md`](./INTENT.md)에 적는다. 비어 있으면 일반적인 스키마만 따른다.

---

## 1. 디렉터리 계약

| 경로 | 역할 | LLM 편집 |
|------|------|----------|
| `sources/` | 원천 자료(아래 §1a 참고) | **금지**: 기존 파일 내용 수정·삭제. 사용자가 “이 소스 추가”라고 한 경우에만 **새 파일 추가** 가능. |
| `pages/<주제>/` | 주제별 위키 본문 | **허용**: 생성·수정·이름 변경 시 교차 링크 정리. |
| `_meta/` | 운영 메타 | **허용**: `ingest-log.md` append, 필요 시 점검 기록. |

루트 `_index.md`만 색인·허브용으로 `pages/` 밖에 둔다.

### 1a. `sources/` 안 자료 종류 (현재 + 확장 계획)

| 단계 | 내용 |
|------|------|
| **지금 (기본)** | `.md`, `.txt` 위주. 클립·붙여넣기·변환 텍스트를 여기에 둔다. |
| **나중에 (확장)** | PDF·이미지 등 바이너리를 같은 `sources/` 트리에 둘 수 있다. 예: `sources/papers/논문.pdf`, `sources/assets/그림.png`. 규칙은 동일: **올린 원본은 LLM이 수정하지 않는다.** 위키에서는 `sources:` 필드에 **상대 경로**로만 적어 근거를 남긴다. |
| **확장 시 유의** | PDF·이미지 **내용**은 에이전트가 항상 읽을 수 있는 것은 아니다. 필요하면 사용자가 같은 주제로 `.md` 요약본을 같이 두거나, 추출 텍스트를 별도 `.md`로 두는 식으로 보완한다(형식은 추후 이 섹션에 구체화 가능). |

---

## 2. 주제별 폴더 (`pages/<topic>/`)

- 위키 페이지는 **`pages/<topic-slug>/파일명.md`** 에 둔다.  
  - `<topic-slug>`: kebab-case (예: `ml`, `work`, `reading`).
- **파일명(확장자 제외)은 `pages/` 전 트리에서 중복되면 안 된다.**  
  → 서로 다른 주제 폴더에 `notes.md` 두 개 금지. 그래야 Obsidian·링크가 `[[파일명]]` 한 가지로 통한다.
- **슬러그** = 그 **파일명**에서 `.md` 를 뺀 것. 위키 링크는 **`[[슬러그]]`** (예: `[[transformer-attention]]`).
- 같은 개념은 새 파일 만들지 말고 **기존 페이지를 고친다.**

---

## 3. Obsidian (사용한다고 가정)

- **설치 여부**: vault는 이 폴더(`llm-wiki`)를 Obsidian에서 열어 쓰면 된다. Cursor만 써도 되고, 읽기·그래프용으로 Obsidian을 같이 써도 된다.
- **태그**: 본문에 `#태그` 를 쓰거나, 아래 frontmatter의 `tags:` 를 쓴다. **한 노트 안에서는 한 방식으로 통일**하는 것을 권장한다.

---

## 4. Frontmatter (위키 페이지 필수)

`pages/**` 및 루트 `_index.md`에 다음 YAML 블록을 둔다.

```yaml
---
title: "화면에 보일 제목"
type: entity | concept | synthesis | source-summary | note | index
updated: YYYY-MM-DD
sources: []   # 선택. 근거가 된 sources/ 내 상대 경로 문자열 배열
tags: []      # 선택. Obsidian·검색용 (문자열 배열)
---
```

- **type**: `entity` | `concept` | `synthesis` | `source-summary` | `note` | `index` (의미는 이전과 동일).
- **sources**: 비우거나, `sources/...` 상대 경로만.
- **tags**: 선택. Obsidian과 호환되게 배열로 적는다.

---

## 5. 링크

- vault 안에서는 **`[[슬러그]]`** (파일명 기준, §2).
- 외부는 `[텍스트](url)`.

---

## 6. 인제스트 로그 (`_meta/ingest-log.md`)

소스를 반영할 때마다 **시간순 append**로 블록을 추가한다.

```text
## YYYY-MM-DD — <한 줄 설명>
- source: sources/<상대경로>
- touched pages: topic/slug-a, topic/slug-b, ...
- notes: (선택) 모순·보류·사용자 확인 필요
```

`touched pages`에는 `pages/` 기준으로 **주제폴더/파일명(확장자 제외)** 를 적는다 (예: `ml/transformer-attention`).

---

## 7. 작업 우선순위 (LLM)

1. 답하기 전에 **`_index.md`**, 관련 **`pages/<topic>/`**, 필요 시 **`sources/`** 를 읽는다.
2. 새 정보는 **같은 슬러그 페이지가 있으면 갱신**, 없을 때만 새 파일 생성.
3. 원문과 충돌하면 페이지에 “모순/불확실”을 적고, **`sources/`는 수정하지 않는다.**

---

## 8. Git 저장소

- 위키는 **이 프로젝트와 같은 Git 저장소**에 둔다(모노레포). 별도 submodule은 쓰지 않는 것을 기본으로 한다.
- 로컬에서 아직 `git init` 이 안 된 폴더라면, 사용자가 원격(GitHub 등)과 연결할 때까지 **형식만 이 트리를 따르면 된다.**
