---
title: "Vault 레이아웃 · Git(Obsidian) 정책"
type: note
updated: 2026-05-03
sources: []
tags:
  - meta
  - git
  - obsidian
---

# Vault 레이아웃 · Git 정책

## 공식 vault 루트

- **하나:** `llm-wiki/` 전체를 Obsidian vault로 연다.
- **`llm-wiki/parkjh/`** 는 중첩된 또 다른 vault 성격이 생긴 상태일 수 있다. 원인 추정·보류는 [`INTENT.md`](../../INTENT.md) 참고.

## `.obsidian` 을 Git에 넣을지

**현재方針:** **`llm-wiki/.obsidian/` 을 커밋한다.** 플러그인·테마·핵심 설정을 기기 간 맞추기 쉽다.

**나중에 커밋에서 빼고 싶을 때 (예상되는 경우)**

| 상황 | 왜 빼는지 |
|------|-----------|
| `workspace.json` 만 줄줄 바뀜 | 창 배치·열린 탭이 기기마다 달라 **매 커밋에 잡다한 diff**가 난다. |
| 여러 PC에서 각자 Obsidian UI만 다르게 쓰고 싶다 | 개인 화면 상태는 공유할 필요가 없다. |
| 협업 시 설정 충돌이 잦다 | 저장소마다 “설정은 각자”로 두고 싶을 때. |

**빼는 방법 예시 (프로젝트 루트 `.gitignore`에 추가)**

```gitignore
# Obsidian — 창 상태만 제외 (설정은 유지)
llm-wiki/.obsidian/workspace.json
llm-wiki/.obsidian/workspace-mobile.json
```

또는 **`.obsidian/` 전체를 무시**하고, 꼭 필요한 설정만 문서로 적어두거나 다른 방식으로 공유한다.

**역방향:** 한동안 무시했던 `.obsidian` 을 다시 추적하려면 `git add -f llm-wiki/.obsidian/...` 등으로 강제 추가할 수 있다(충돌은 수동 해결).

## 같이 볼 것

- [`INTENT.md`](../../INTENT.md)
