---
description: "how-to-work 현황 확인. 현재 이터레이션과 단계 진행 상태를 보여준다."
allowed-tools: Bash, Read, Glob
---

# 현황 확인

## 컨텍스트

- 버전 목록: !`ls -d docs/work/v*/ 2>/dev/null || echo "NO_VERSIONS"`
- 현재 버전: !`cat docs/work/.current 2>/dev/null || echo "NO_CURRENT"`
- 현재 산출물: !`ls docs/work/$(cat docs/work/.current 2>/dev/null)/ 2>/dev/null || echo "NO_FILES"`

## 지시사항

`docs/work/` 디렉토리를 확인하고 현재 진행 상태를 보고한다.

### 디렉토리가 없는 경우
"아직 시작되지 않았습니다. `/tf:0`으로 0단계(문제 정의)부터 시작하세요." 라고 안내한다.

### 디렉토리가 있는 경우

1. 전체 이터레이션 목록을 보여준다 (v0, v1, ...).
2. 현재 이터레이션(`.current` 파일이 가리키는 버전)의 진행 상태를 아래 표로 출력한다:

| 단계 | 스킬 | 파일 | 상태 |
|------|------|------|------|
| 0. 문제 정의 | `/tf:0` | `0-problem-definition.md` | 완료/미완료 |
| 1. 목표 정의 | `/tf:1` | `1-goals.md` | 완료/미완료 |
| 2. 요구사항 정리 | `/tf:2` | `2-requirements.md` | 완료/미완료 |
| 3. 설계 | `/tf:3` | `3-design.md` | 완료/미완료 |
| 4. 작업 분해 | `/tf:4` | `4-task-breakdown.md` | 완료/미완료 |
| 5. MVP 구현 | `/tf:5` | `5-mvp.md` | 완료/미완료 |
| 6. 검증 | `/tf:6` | `6-verification.md` | 완료/미완료 |
| 7. 마무리 | `/tf:7` | `7-wrap-up.md` | 완료/미완료 |

3. 다음 진행할 단계를 안내한다: "다음 단계: `/tf:N`으로 진행하세요."

### 현재 이터레이션이 모두 완료된 경우
"현재 이터레이션(vN)이 완료되었습니다. 새 이터레이션을 시작하시겠습니까?" 라고 질문한다.
사용자가 승인하면:
1. 다음 버전 디렉토리를 생성한다 (예: `docs/work/v1/`).
2. `docs/work/.current` 파일을 새 버전 이름으로 갱신한다.
3. "새 이터레이션 v1이 시작되었습니다. `/tf:0`으로 시작하세요." 라고 안내한다.

### 별칭 안내
스킬 목록 하단에 아래 별칭 표를 보여준다:

| 숫자 | 별칭 |
|------|------|
| `/tf:0` | `/tf:define` |
| `/tf:1` | `/tf:goal` |
| `/tf:2` | `/tf:req` |
| `/tf:3` | `/tf:design` |
| `/tf:4` | `/tf:task` |
| `/tf:5` | `/tf:mvp` |
| `/tf:6` | `/tf:verify` |
| `/tf:7` | `/tf:wrapup` |
