# thinkfirst — how-to-work workflow plugin for Claude Code

체계적 사고 과정을 강제하여 이해의 부채를 방지하는 Claude Code 플러그인.
리서치 agent team이 각 단계에서 기존 솔루션·논문·코드베이스를 자동 조사합니다.

## 설치

```bash
claude plugin marketplace add https://github.com/cafaddict/cafaddict-claude-marketplace.git
claude plugin install tf@cafaddict-claude-marketplace
```

## 사용법

### 현황 확인

```
/tf:status
```

현재 이터레이션과 단계 진행 상태를 보여줍니다.

### 단계별 진행

| 숫자 | 별칭 | 단계 |
|------|------|------|
| `/tf:0` | `/tf:define` | 문제 정의 — "이걸 왜 하는가?" |
| `/tf:1` | `/tf:goal` | 목표를 측정 가능하게 정의 |
| `/tf:2` | `/tf:req` | 요구사항 정리 (범위 고정) |
| `/tf:3` | `/tf:design` | 설계 (구조, 기술 선택, 불확실성) |
| `/tf:4` | `/tf:task` | 작업 단위 분해 |
| `/tf:5` | `/tf:mvp` | 최소 기능 구현 (MVP/Spike) |
| `/tf:6` | `/tf:verify` | 검증과 피드백 |
| `/tf:7` | `/tf:wrapup` | 정리 및 마무리 |
| `/tf:research` | — | 리서치 오케스트레이터 (아무 시점에서나 호출) |

### 리서치 Agent Team

`/tf:research`를 호출하면 여러 전문가 agent가 병렬로 리서치를 수행합니다:

| Agent | 역할 | 모델 |
|-------|------|------|
| `web-researcher` | 웹 검색 (솔루션, 라이브러리, 블로그) | sonnet |
| `academic-researcher` | 논문, 알고리즘, 학술 자료 조사 | sonnet |
| `codebase-analyzer` | 현재 프로젝트 코드베이스 분석 | sonnet |
| `competitor-analyst` | 경쟁 제품, 대안 비교 분석 | sonnet |
| `research-synthesizer` | 결과 종합, 충돌/모순 정리 | opus |

- 사용자가 **어떤 agent를 실행할지 선택** 가능
- 선택된 agent들이 **병렬 실행** 후 synthesizer가 종합
- 결과는 `docs/work/{버전}/research/{주제}/` 에 파일로 저장
- 해당 단계 산출물에 종합 요약이 자동 연결

각 단계(0, 1, 2, 3, 5) 진행 중에도 적합한 시점에서 리서치를 제안합니다.

### 이터레이션

산출물은 프로젝트의 `docs/work/` 디렉토리에 버전별로 저장됩니다:

```
docs/work/
├── v0/                          ← 첫 번째 사이클
│   ├── 0-problem-definition.md
│   ├── 1-goals.md
│   ├── ...
│   └── research/                ← 리서치 결과
│       └── {주제}/
│           ├── web-researcher.md
│           ├── academic-researcher.md
│           ├── codebase-analyzer.md
│           ├── competitor-analyst.md
│           └── synthesis.md
├── v1/                          ← 두 번째 사이클
│   └── ...
└── .current                     ← "v1" (현재 버전 텍스트 파일)
```

`/tf:status`에서 이터레이션 완료 시 새 버전을 시작할 수 있습니다.

## 핵심 원칙

- **기록 → 확인 → 다음 진행**: 각 단계에서 파일에 기록한 후 사용자 확인을 받아야 다음으로 넘어갑니다.
- **이해의 부채 방지**: 모든 결정과 근거가 문서로 남습니다.
- **불확실성 우선 검증**: 3단계에서 식별한 불확실한 부분을 5단계 MVP에서 최우선으로 검증합니다.
- **측정 가능한 목표**: 1단계에서 정한 수치 목표를 6단계에서 대비 확인합니다.
