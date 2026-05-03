---
title: "Software 3.0 (프롬프트·자연어 층)"
type: concept
updated: 2026-05-03
sources:
  - sources/karpathy-llm-vibe-coding-notes.md
tags:
  - ai
  - software-3
---

# Software 3.0

Software 2.0(신경망이 먹는 데이터·가중치 층)에 이어, **자연어·프롬프트로 동작을 기술하는 층**으로 자주 언급되는 프레임이다. Karpathy의 공개 강연·인터뷰 맥락을 소스가 요약한다.

## 자주 나오는 말

- **“가장 뜨거운 새 프로그래밍 언어는 영어(자연어)”** — 의도를 말로 옮기는 능력이 중요해진다(2차 정리 인용).
- LLM을 **새 컴퓨터·OS에 비유**하는 설명 — API·문서·에코시스템·오픈/클로즈드 모델 구도. 참고: [Latent Space — Software 3.0](https://www.latent.space/p/s3).

## 잘 활용하려면

- **의도·제약**(보안, 성능, 실패 시 동작)을 말로 **쪼개서** 준다.
- **실행·테스트**로 검증 루프를 돌린다 — 동작 확인 책임은 사람에게 있다는 전제.
- 에러 로그·재현 단계·경로 등 **도구가 읽을 맥락**을 그대로 넘긴다.

## 같이 볼 것

- [[vibe-coding]]
- [[andrej-karpathy]]
- [[karpathy-llm-vibe-ingest]]
