# llm-wiki

Karpathy 스타일 **LLM 유지 마크다운 위키**용 폴더다.

- **형식·역할의 단일 기준**: [`WIKI_SCHEMA.md`](./WIKI_SCHEMA.md)
- **왜 이 vault를 쓰는지**: [`INTENT.md`](./INTENT.md) (비어 있어도 됨 — 나중에 채움)
- **원문**: `sources/` (기본은 `.md`/`.txt`, PDF·이미지는 확장 계획은 스키마 §1a)
- **본문**: `pages/<주제>/` (파일명은 전체에서 유일하게)
- **인제스트 로그**: `_meta/ingest-log.md`
- **대화를 위키에 남기기**: [`FILING.md`](./FILING.md) (트리거 문구 + 에이전트 절차)

**Obsidian**: 이 `llm-wiki` 폴더를 vault로 열면 된다. 안 써도 되고, 그래프·읽기용으로 쓸 수 있다. 태그·링크 규칙은 `WIKI_SCHEMA.md` §3·§5.

Cursor에서는 같은 폴더를 연 채로 에이전트가 읽고 고친다.
