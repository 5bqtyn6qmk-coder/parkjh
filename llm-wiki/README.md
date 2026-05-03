# llm-wiki

Karpathy 스타일 **LLM 유지 마크다운 위키**용 폴더다.

- **형식·역할의 단일 기준**: [`WIKI_SCHEMA.md`](./WIKI_SCHEMA.md)
- **원문**: `sources/` (기본은 `.md`/`.txt`, PDF·이미지는 확장 계획은 스키마 §1a)
- **본문**: `pages/<주제>/` (파일명은 전체에서 유일하게)
- **인제스트 로그**: `_meta/ingest-log.md`

**Obsidian**: 이 `llm-wiki` 폴더를 vault로 열면 된다. 안 써도 되고, 그래프·읽기용으로 쓸 수 있다. 태그·링크 규칙은 `WIKI_SCHEMA.md` §3·§5.

Cursor에서는 같은 폴더를 연 채로 에이전트가 읽고 고친다.
