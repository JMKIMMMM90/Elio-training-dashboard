# Elio INITIAN Training Program

엘리오앤컴퍼니 신입교육(2026.9.2 ~ 10.1, 4주) 진척도·평가 관리 대시보드.

- **배포 주소**: https://jmkimmmm90.github.io/Elio-training-dashboard/
- **스택**: 단일 `index.html` (React 18 UMD + Babel CDN, 빌드 없음) + Firebase Realtime Database(데이터) + Firebase Storage(제출 파일) + GitHub Pages(호스팅)
- **배포**: `index.html` 수정 → commit → push → 1~2분 내 자동 반영

## 주요 기능

- **신입(INITIAN)**: 홈(오늘의 할 일·실시간 점수·제출함) / 교육안내(목적·룰·평가기준·커리큘럼) / 목표관리(달력·주차별 목표 세팅) / 내 평가(점수 상세)
- **평가 체계**: 총 500점 = 주차 100점 × 4 + FINAL PPT TEST 100점. 달성률·제출 가점은 자동 집계, 담당자는 정성 4항목만 입력
- **관리자·교육담당자**: 전체 현황(전원 실시간) / 평가 입력 / 관리 센터(총량·과제명·담당자·FINAL 설정)

## 저장소 구조

| 경로 | 용도 |
|---|---|
| `index.html` | 앱 전체 (이 파일 하나만 수정하면 됨) |
| `CLAUDE.md` | Claude Code 작업 규칙·기술 스펙 — 수정 전 반드시 읽을 것 |
| `docs/개발일지.md` | 굵직한 변경 이력 (사람용) |
| `docs/회고.md` | 작업 방식·배운 점 회고 (성과 공유용) |
| `.claude/skills/` | Claude Code 스킬 (신입평가·PPT 검증 등, 추가 예정) |

## 주의

- 이 저장소는 **공개(public)** 입니다. 회사 원본 자료(쉐도잉 원본 PPT, 신입 제출물 등)는 절대 저장소에 넣지 마세요.
- 데이터 구조(Firebase 경로)를 바꾸면 사용 중인 기록이 깨질 수 있습니다 — `CLAUDE.md`의 스키마 설명을 먼저 확인하세요.
