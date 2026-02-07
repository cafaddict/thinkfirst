---
description: "how-to-work 5단계: MVP/Spike 구현. 최소 기능 구현으로 설계 가설을 검증한다."
allowed-tools: Edit, Write, Read, AskUserQuestion, Bash, Glob, Grep
---

# 5단계: 최소 기능 구현 (MVP / Spike)

## 이전 단계 산출물

- 0단계 문제 정의: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/0-problem-definition.md 2>/dev/null || echo "NO_FILE"`
- 1단계 목표: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/1-goals.md 2>/dev/null || echo "NO_FILE"`
- 2단계 요구사항: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/2-requirements.md 2>/dev/null || echo "NO_FILE"`
- 3단계 설계: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/3-design.md 2>/dev/null || echo "NO_FILE"`
- 4단계 작업 분해: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/4-task-breakdown.md 2>/dev/null || echo "NO_FILE"`

## 기존 산출물 확인

- 기존 파일: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/5-mvp.md 2>/dev/null || echo "NO_FILE"`

## 지시사항

이 단계의 목적은 **완벽함보다 동작을 우선하여, 설계 가설을 빠르게 검증하는 것**이다.

### 전제 조건
- 0~4단계 산출물이 없으면 해당 단계를 먼저 실행하라고 안내하고 중단한다.

### 진행 방식

1. **스킬 시작 즉시** 현재 버전 디렉토리의 `5-mvp.md` 파일을 산출물 파일 형식 템플릿으로 생성한다. 기존 파일이 있으면 이어서 진행한다.

2. 4단계 작업 목록에서 **우선 검증 항목**(3단계에서 식별한 불확실한 부분)을 확인한다.

3. 사용자에게 MVP 범위를 확인한다:
   - "4단계 작업 목록 중 MVP에 포함할 범위는 어디까지인가요?"
   - "하드코딩이나 단순화해도 되는 부분이 있나요?"

4. **합의된 MVP 범위를 파일에 먼저 기록한다.** 파일의 "MVP 범위" 섹션이 채워지기 전에는 절대 구현에 들어가지 않는다.

5. 기록된 파일 내용을 사용자에게 보여주고 **확인을 받는다.** 사용자가 승인하기 전에는 구현에 들어가지 않는다.

6. 사용자 승인 후 구현을 진행한다.
   - 완벽함보다 동작 우선
   - 하드코딩 허용
   - 최적화는 나중에

7. **구현 진행 중 발견 사항이 있을 때마다** 즉시 파일을 업데이트한다:
   - 설계 가설이 맞았는지/틀렸는지
   - 예상 못한 문제
   - 설계 수정이 필요한 부분

8. MVP 구현이 끝나면 결과를 사용자에게 보여주고 합의를 구한다.

### 산출물 파일 형식

```markdown
# 5단계: MVP 구현

## MVP 범위
- 포함: ...
- 제외 (나중에): ...
- 하드코딩/단순화: ...

## 검증 결과

### 불확실했던 부분
| 항목 | 결과 | 비고 |
|------|------|------|
| ... | 검증됨/문제발견 | ... |

### 예상 못한 문제
- ...

### 설계 수정 필요 사항
- ...

## 현재 상태
(MVP가 동작하는지, 어디까지 되는지)
```

### 주의사항
- MVP에서는 완벽한 코드를 기대하지 않는다. 동작 확인이 목적이다.
- 설계 변경이 필요하면 사용자와 합의 후 3단계 산출물도 업데이트한다.
- 구현 중 발견 사항을 파일에 기록한 후, 기록 내용을 사용자에게 보여주고 확인을 받는다.
- 이 단계가 완료되면 "다음 단계: `/tf:6`으로 검증을 진행하세요." 라고 안내한다.
