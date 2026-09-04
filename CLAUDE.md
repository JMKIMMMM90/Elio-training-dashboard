# Elio INITIAN Training Program (Elio-training-dashboard)

## 프로젝트 개요
엘리오앤컴퍼니 신입교육(2026.9.2~10.1, 4주) 진척도 관리 대시보드.
프로그램 공식 명칭 "Elio INITIAN Training Program", 진행률 카드 제목 "Road to INITIAN".
GitHub Pages로 배포되어 신입들이 URL로 접속해 사용한다.
- 배포 주소: https://jmkimmmm90.github.io/Elio-training-dashboard/

## 파일 구조
- index.html — 앱 전체가 담긴 단일 파일. 이 파일 하나만 수정하면 된다.
  React 18 UMD + Babel standalone CDN 방식, 빌드 도구 없음.
  수정 후 push하면 GitHub Pages가 1~2분 내 자동 반영.

## 배포 방법 (수정 후 반드시 수행)
git add → commit → push. 별도 배포 명령 없음.

## 앱 구조
- 회사 디자인 시스템 적용(디자인팀 "생각의 열매" 스타일 기준): 라이트 기본,
  딥그린 #214c45 주색 + 오렌지 #f87209 경고색, radius 8px 플랫 카드(1px 라인 보더),
  시스템 폰트 스택, 알약형 세그먼트 탭. THEMES 상수에 팔레트(다크는 그린 톤 재해석,
  토글로 유지). 주차 구분색은 w1~w4 토큰(차분한 4색).
- 데이터는 Firebase Realtime Database에 사람별로 실시간 저장.
  - 경로: users/<이름>/{checks, logs, goals, joinedAt}. 경로/구조를 바꾸면 전원의 기록이
    깨지므로 변경은 신중히.
  - goals: 하루 목표(신입 자율 입력). goals/<dayKey>/<ppt|proj|book> = 목표 배열.
    수량형 {text, target, actual}(초과달성 가능, 집계는 100% 캡) / 체크형 {text, done}.
    목표가 있는 영역은 목표 평균으로, 없으면 기존 checks 체크로 점수 계산(taskScore).
  - config 노드(전원 실시간 반영): targets/w<주차>/<영역>=주차 총량,
    weeks/w<주차>/{ppt,project,book}=과제명 덮어쓰기(없으면 코드 기본값, mergeWeeks),
    staff/<이름>=true 담당자 명단.
  - 권한 2단계: ADMIN_NAMES 상수(김재민) = "⚙ 관리" 탭(총량·과제명·담당자 명단·신입별
    담당자 지정) + 평가. config/staff에 등록된 담당자 = "📝 평가" 탭. 로그인이 없으므로
    편의상 숨김이지 보안 아님. 관리자·담당자는 전체 현황 목록에서 제외.
  - 평가: users/<신입>/reviews/{w1~w4,final} = {score(10점 만점), comment, by, at}.
    저장 즉시 신입 본인 화면의 "교육 평가" 카드에 공개됨. users/<신입>/mentor = 담당자명.
  - 총량이 설정된 영역은 주차 화면에 누적 게이지 / 계획 합계 검증(부족·일치·초과) /
    페이스 점검(오늘까지 계획 누적 vs 실제)이 표시됨. 전체 현황에도 사람별 누적·페이스 표시.
  - firebaseConfig는 index.html 상단에 있음 (프로젝트: elio-training, 소유: 대표님 구글 계정).
  - localStorage는 이름(training-dashboard-2026-name)·테마(-theme)만 기기별 저장.
    예전 키(training-dashboard-2026)의 기록은 최초 접속 시 온라인으로 1회 자동 이전.
- 첫 화면: 접속할 때마다 항상 표시(자동 로그인 없음). 드롭다운으로 역할 선택 —
  INITIAN(신입: 명단 선택 또는 새 이름 등록) / 관리자·교육담당자(ADMIN_NAMES+staff
  등록 이름만 선택 가능, 새 등록 불가).
- 신입 새 이름 등록 시 입사일(달력 date input)·직급(RANKS 상수: 위원/팀장) 필수 →
  users/<이름>/{joinDate("YYYY-MM-DD"), rank}. 이름 표기는 항상 "민지홍 위원 (26.9.1 입사)"
  형식(직급 있으면 님 대신 직급) — 첫 화면·헤더 인사말·전체 현황·평가 선택·관리 탭 공통.
- 화면: 전체 진행률 / GROUND RULES / 달력 뷰(기본) / 주차별 체크 뷰 / 전체 현황 뷰(전원 진행률, 실시간).

## 교육 일정 (WEEKS 상수)
- 1주차 9/2(수)~9/8(화): PPT 기초 쉐도잉 / [비전전략]울산대병원 / 병원에서 일하는 이유
- 2주차 9/9~9/15: 쉐도잉 AI 전환 / [개원]평택아주대병원 / 병원경영 실전전략
- 3주차 9/16~9/22: 심화과제 연습 / [성과급]울산대병원 / 중소병원 생존전략
- 4주차 9/23~10/1: PPT 테스트 대비 / [프로세스]울산대 검사실 / 경영의 명의
- 추석 연휴 9/24~9/26 휴무 제외(HOLIDAYS 상수).

## GROUND RULES (변경 시 GROUND_RULES 상수와 과제 time 필드 동시 수정)
- 주별 계획 공유: 주차 첫날(수) 오전 11시까지
- 커뮤니케이션: 상시
- 제출물(PPT 작성본·독후감): 주차 마지막 날 오전 10시까지
- TEST(프로젝트·도서, 4주차 PPT 포함): 주차 마지막 날 오후 4시

## 작업 규칙
- 답변·커밋 메시지는 한국어. 사용자는 비전공자이므로 왕초보 수준으로 설명.
- 수정 후 반드시: 문법 확인 → commit & push → 배포 주소에서 확인 안내.
- Toss 스타일(다크 기본, 라운드 카드) 톤 유지.
