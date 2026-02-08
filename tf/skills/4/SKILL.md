---
description: "how-to-work 4단계: 작업 단위 분해. 실행 가능한 작업 목록 생성."
allowed-tools: Edit, Write, Read, AskUserQuestion, Bash, Glob, Grep, Task
---

# 4단계: 작업 단위 분해

## 이전 단계 산출물

- 0단계 문제 정의: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/0-problem-definition.md 2>/dev/null || echo "NO_FILE"`
- 1단계 목표: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/1-goals.md 2>/dev/null || echo "NO_FILE"`
- 2단계 요구사항: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/2-requirements.md 2>/dev/null || echo "NO_FILE"`
- 3단계 설계: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/3-design.md 2>/dev/null || echo "NO_FILE"`

## 기존 산출물 확인

- 기존 파일: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/4-task-breakdown.md 2>/dev/null || echo "NO_FILE"`

## 지시사항

이 단계의 목적은 **설계를 실행 가능한 작업 단위로 쪼개는 것**이다.

### 전제 조건
- 0~3단계 산출물이 없으면 해당 단계를 먼저 실행하라고 안내하고 중단한다.

### 진행 방식

1. **스킬 시작 즉시** 현재 버전 디렉토리의 `4-task-breakdown.md` 파일을 산출물 파일 형식 템플릿으로 생성한다. 기존 파일이 있으면 이어서 진행한다.

2. 3단계 설계를 기반으로 작업 목록 초안을 제안한다.

3. 각 작업에 대해 사용자와 함께 검토한다. **각 작업이 합의될 때마다** 즉시 파일을 업데이트한다.
   - 1~2일 내 끝낼 수 있는 크기인가?
   - 의존성이 명확한가?
   - 병렬 처리 가능한 작업이 있는가?

4. 3단계에서 식별한 **불확실한 부분**을 가장 먼저 검증하도록 순서를 배치한다.

5. 최종 작업 목록을 사용자에게 보여주고 합의를 구한다.

### 산출물 파일 형식

```markdown
# 4단계: 작업 분해

## 작업 목록

| # | 작업 | 설명 | 의존성 | 예상 크기 |
|---|------|------|--------|----------|
| 1 | ... | ... | 없음 | ... |
| 2 | ... | ... | 1 | ... |

## 의존성 관계
(작업 간 순서와 병렬 가능 여부)

## 우선 검증 항목
(3단계에서 식별한 불확실한 부분 → 어느 작업에서 검증하는지)
```

### 주의사항
- 작업이 너무 크면 (2일 이상) 더 잘게 쪼갠다.
- 작업이 너무 작으면 (1시간 미만) 합친다.
- 각 작업을 파일에 기록한 후, 기록 내용을 사용자에게 보여주고 확인을 받는다. 확인 전에 다음 작업으로 넘어가지 않는다.
- 이 단계가 완료되면 "다음 단계: `/tf:5`로 MVP 구현을 시작하세요." 라고 안내한다.
