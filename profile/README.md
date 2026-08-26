# 🎯 요기픽 (YogiPick)

> **뭐 먹을지 모르겠다면? 스와이프로 3분 만에 결정.**

이 조직은 **2026 요기요 × Oracle 해커톤**에 참가한 **TEAM 08**의 출품작 레포지토리입니다.
개발 기간 2026.07.27 ~ 08.21, OCI(Oracle Cloud Infrastructure) 위에서 개발·배포했습니다.

**요기픽**은 혼자서도, 친구들과 함께서도 — 틴더처럼 메뉴 카드를 스와이프하면
AI가 취향을 학습해서 오늘 먹을 메뉴와 가게를 골라주는 서비스입니다.

> ⚠️ 해커톤 출품용 프로토타입이며, 요기요의 공식 서비스가 아닙니다.

---

## ✨ 핵심 기능

| 기능 | 설명 |
|------|------|
| 🃏 **스와이프 픽** | 메뉴 카드를 PICK/PASS — 반응 속도까지 취향 신호로 학습 |
| 🤖 **AI 추천** | 자연어 한 마디("비 오는데 얼큰한 거") → 28차원 태그 벡터 → 벡터 유사도 추천 |
| 👥 **그룹 픽** | 실시간 동시 스와이프 + Least-Misery 전략으로 전원이 만족하는 메뉴 결정 |
| 🗳️ **매장 투표** | AI 추천 3곳 중 3분 투표로 최종 확정, 공동 장바구니·더치페이까지 |
| 🌦️ **실시간 컨텍스트** | 시간대·날씨(Open-Meteo)가 추천 벡터에 실시간 반영 |

## 🏗️ 아키텍처

```
자연어 입력 → NLU (키워드 룰 1차 + LLM 2차)
           → 28차원 태그 벡터
           → Oracle AI Vector Search (VECTOR_DISTANCE · COSINE)
           → 다양성 리랭킹 → 메뉴 카드 7장 + LLM 추천 이유
```

- **모바일**: React Native (Expo SDK 54)
- **백엔드**: NestJS · Socket.io (그룹 실시간)
- **AI**: OCI Generative AI (meta.llama-3.3-70b) — 키워드 룰 1차로 지연 최소화
- **DB**: Oracle Autonomous Database 26ai — 별도 벡터 DB 없이 내장 Vector Search
- **인프라**: OCI Container Instance · GitHub Actions → Docker Hub CI/CD

## 📦 레포지토리

| 레포 | 내용 |
|------|------|
| [`yogipick-frontend`](https://github.com/yogipick/yogipick-frontend) | Expo 모바일 앱 (스와이프 UI · 그룹 WS) |
| [`yogipick-backend`](https://github.com/yogipick/yogipick-backend) | NestJS API · 벡터 추천 엔진 · WebSocket 게이트웨이 |

## 📑 발표자료

[**요기픽 발표자료 (PDF)**](https://github.com/yogipick/.github/blob/main/profile/assets/yogipick-presentation.pdf)
