---
description: "how-to-work 2단계: 요구사항 정리 및 범위 고정."
allowed-tools: Edit, Write, Read, AskUserQuestion, Bash, Glob, Grep, Task
---

# 2단계: 요구사항 정리 (범위 고정)

## 이전 단계 산출물

- 0단계 문제 정의: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/0-problem-definition.md 2>/dev/null || echo "NO_FILE"`
- 1단계 목표: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/1-goals.md 2>/dev/null || echo "NO_FILE"`

## 기존 산출물 확인

- 기존 파일: !`cat docs/work/$(cat docs/work/.current 2>/dev/null)/2-requirements.md 2>/dev/null || echo "NO_FILE"`

## 지시사항

이 단계의 목적은 **범위를 고정하고, 이번에 할 것과 안 할 것을 명확히 나누는 것**이다.

### 전제 조건
- 0~1단계 산출물이 없으면 해당 단계를 먼저 실행하라고 안내하고 중단한다.

### 진행 방식

1. **스킬 시작 즉시** 현재 버전 디렉토리의 `2-requirements.md` 파일을 산출물 파일 형식 템플릿으로 생성한다. 기존 파일이 있으면 이어서 진행한다.

2. 0단계 문제와 1단계 목표를 요약해서 보여준다.

3. "이 목표를 달성하기 위해 어떤 기능/작업이 필요한가요?" 라고 질문한다.

4. 사용자의 답변을 받으면서 아래 세 범주로 분류한다. **각 답변을 받을 때마다** 즉시 파일을 업데이트한다.
   - **Must** — 없으면 의미 없음
   - **Should** — 있으면 확실히 좋음
   - **Nice to have** — 이번 범위에서는 제외

5. **Must 목록 초안이 작성된 후**, 사용자에게 리서치를 제안한다:
   - "요구사항에 대해 기존 구현이나 경쟁 제품을 리서치할까요? (codebase-analyzer, competitor-analyst 추천)"
   - 사용자가 Yes → Task 도구로 선택된 agent를 병렬 실행한다.
   - 사용자가 No → 그대로 진행.

6. 반드시 **"이번에 안 할 것"** 목록을 명시적으로 작성한다. 사용자에게 "이번에 명시적으로 제외할 것이 있나요?" 라고 질문한다.

7. 최종 분류 결과를 사용자에게 보여주고 합의를 구한다.

### 산출물 파일 형식

```markdown
# 2단계: 요구사항 정리

## Must (없으면 의미 없음)
- ...

## Should (있으면 좋음)
- ...

## Nice to have (이번에는 제외)
- ...

## 이번에 안 할 것 (명시적 제외)
- ...
```

### 주의사항
- "이번에 안 할 것"이 비어 있으면 안 된다. 반드시 사용자와 함께 제외 항목을 정한다.
- 범위가 커지려 하면 "이건 Must인가요, Should인가요?" 라고 질문해서 범위를 통제한다.
- 각 답변을 파일에 기록한 후, 기록 내용을 사용자에게 보여주고 확인을 받는다. 확인 전에 다음으로 넘어가지 않는다.
- 이 단계가 완료되면 "다음 단계: `/tf:3`으로 설계를 시작하세요." 라고 안내한다.
