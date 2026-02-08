---
description: "리서치 오케스트레이터. 여러 전문가 agent를 병렬로 실행하여 주제에 대한 종합 리서치를 수행한다."
user-invocable: true
allowed-tools: Bash, Glob, Grep, Read, Write, Task, AskUserQuestion
argument-hint: "<리서치 주제>"
---

# 리서치 오케스트레이터

## 현재 이터레이션 컨텍스트
- 현재 버전: !`cat docs/work/.current 2>/dev/null || echo "NO_CURRENT"`
- 현재 산출물 목록: !`ls docs/work/$(cat docs/work/.current 2>/dev/null)/ 2>/dev/null || echo "NO_FILES"`

## 사용 가능한 리서치 Agent
1. **web-researcher** — 웹 검색 (기존 솔루션, 라이브러리, 블로그, 기술 문서)
2. **academic-researcher** — 논문, 알고리즘, 학술 자료 조사
3. **codebase-analyzer** — 현재 프로젝트 코드베이스 구조/패턴 분석
4. **competitor-analyst** — 경쟁 제품, 유사 도구, 대안 비교 분석

## 진행 방식

### 1. 주제 확인
- argument로 주제가 전달되면 사용한다.
- 없으면 사용자에게 "어떤 주제를 리서치할까요?" 라고 질문한다.

### 2. Agent 선택
사용자에게 어떤 agent를 사용할지 물어본다:
- "다음 중 어떤 리서치 agent를 실행할까요? (복수 선택 가능)"
  - web-researcher
  - academic-researcher
  - codebase-analyzer
  - competitor-analyst
  - 전체 (4개 모두)

### 3. 병렬 실행
- 선택된 agent들을 **Task 도구를 사용하여 동시에 병렬로 실행**한다.
- 각 agent에게 리서치 주제를 전달한다.
- 모든 Task를 **하나의 메시지에서 동시에** 호출한다.

### 4. 종합
- 모든 agent의 결과를 수집한 후, **research-synthesizer agent를 Task 도구로 실행**한다.
- synthesizer에게 모든 리서치 결과를 전달하고 종합을 요청한다.

### 5. 산출물 통합
- 현재 이터레이션의 가장 최근 단계 산출물 파일을 확인한다.
- 산출물 파일 하단에 `## 리서치 결과` 섹션을 추가한다.
- synthesizer의 종합 결과를 해당 섹션에 기록한다.
- 기록된 내용을 사용자에게 보여주고 확인을 받는다.

## 주의사항
- Agent 선택은 반드시 사용자가 한다. 자동 선택하지 않는다.
- 각 agent의 결과를 그대로 보여주지 말고, synthesizer를 거쳐 종합된 결과만 보여준다.
- 산출물 파일이 없으면 `docs/work/{현재버전}/research-{주제}.md`로 별도 파일을 생성한다.
- 리서치 완료 후 "리서치가 완료되었습니다. 현재 진행 중인 단계로 돌아가세요." 라고 안내한다.
