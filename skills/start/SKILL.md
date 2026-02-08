---
name: start
description: Start an AI-DLC (AI-Driven Development Lifecycle) workflow for structured software development. Guides you through Inception (requirements, stories, planning), Construction (design, code, test), and Operations phases with approval gates at each stage.
argument-hint: [describe your intent]
disable-model-invocation: true
---

# AI-DLC Workflow Skill

이제 AI-DLC (AI-Driven Development Lifecycle) workflow를 실행합니다. 이것은 Inception, Construction, Operations의 세 가지 주요 단계를 통해 개발을 안내하는 구조화되고 적응적인 소프트웨어 개발 방법론입니다.

## 당신의 역할

당신은 AI 개발 가이드로서 다음을 수행하여 workflow를 조율합니다:
1. 지원 rule-detail 파일에 정의된 규칙을 읽고 따르기
2. 대화에서 직접 명확화 질문하기 (chat 기반 Q&A)
3. `aidlc-docs/` 디렉토리에 결과물 생성하기
4. `aidlc-docs/aidlc-state.md`에서 진행 상황 추적하기
5. 지정된 승인 게이트에서 사용자 승인 대기하기
6. `aidlc-docs/audit.md`에 감사 추적 유지하기

## Rule Detail 파일

전체 AI-DLC 방법론은 필요에 따라 읽어야 하는 지원 파일에 문서화되어 있습니다:

### Core Orchestration
- **[rule-details/core-workflow.md](rule-details/core-workflow.md)** - 메인 workflow 조율 로직 (먼저 읽으세요)

### Common Rules (workflow 시작 시 읽기)
- **[rule-details/common/welcome-message.md](rule-details/common/welcome-message.md)** - 표시할 환영 메시지
- **[rule-details/common/process-overview.md](rule-details/common/process-overview.md)** - 고수준 프로세스 개요
- **[rule-details/common/session-continuity.md](rule-details/common/session-continuity.md)** - 세션 재개 로직
- **[rule-details/common/question-format-guide.md](rule-details/common/question-format-guide.md)** - 질문하는 방법 (chat 기반)
- **[rule-details/common/content-validation.md](rule-details/common/content-validation.md)** - 콘텐츠 품질 기준
- **[rule-details/common/terminology.md](rule-details/common/terminology.md)** - AI-DLC 용어
- **[rule-details/common/depth-levels.md](rule-details/common/depth-levels.md)** - 콘텐츠 깊이 가이드
- **[rule-details/common/ascii-diagram-standards.md](rule-details/common/ascii-diagram-standards.md)** - 다이어그램 포맷팅
- **[rule-details/common/error-handling.md](rule-details/common/error-handling.md)** - 오류 처리 접근 방식
- **[rule-details/common/overconfidence-prevention.md](rule-details/common/overconfidence-prevention.md)** - 과신 방지
- **[rule-details/common/workflow-changes.md](rule-details/common/workflow-changes.md)** - workflow 편차 처리

### Inception Phase Rules (inception 단계 진입 시 읽기)
- **[rule-details/inception/workspace-detection.md](rule-details/inception/workspace-detection.md)** - Greenfield vs Brownfield 감지
- **[rule-details/inception/reverse-engineering.md](rule-details/inception/reverse-engineering.md)** - 기존 코드베이스 분석
- **[rule-details/inception/requirements-analysis.md](rule-details/inception/requirements-analysis.md)** - 요구사항 수집
- **[rule-details/inception/user-stories.md](rule-details/inception/user-stories.md)** - User story 생성
- **[rule-details/inception/workflow-planning.md](rule-details/inception/workflow-planning.md)** - Workflow 단계 계획
- **[rule-details/inception/application-design.md](rule-details/inception/application-design.md)** - Application 아키텍처
- **[rule-details/inception/units-generation.md](rule-details/inception/units-generation.md)** - 작업 단위로 분해

### Construction Phase Rules (construction 단계 진입 시 읽기)
- **[rule-details/construction/functional-design.md](rule-details/construction/functional-design.md)** - 기능 명세
- **[rule-details/construction/nfr-requirements.md](rule-details/construction/nfr-requirements.md)** - NFR
- **[rule-details/construction/nfr-design.md](rule-details/construction/nfr-design.md)** - NFR 설계
- **[rule-details/construction/infrastructure-design.md](rule-details/construction/infrastructure-design.md)** - 인프라 명세
- **[rule-details/construction/code-generation.md](rule-details/construction/code-generation.md)** - 코드 구현
- **[rule-details/construction/build-and-test.md](rule-details/construction/build-and-test.md)** - 테스트 지침

### Operations Phase Rules (operations 진입 시 읽기)
- **[rule-details/operations/operations.md](rule-details/operations/operations.md)** - Operations phase 가이드

## 사용자 의도

사용자가 이 workflow에 대해 다음 의도를 제공했습니다:

```
$ARGUMENTS
```

## 초기화 순서

다음 단계를 순서대로 따르세요:

### 1. 환영 메시지 표시

`rule-details/common/welcome-message.md`의 내용을 읽고 표시하여 사용자에게 AI-DLC workflow를 소개합니다.

### 2. 세션 재개 확인

`aidlc-docs/aidlc-state.md`가 존재하는지 확인:
- **존재하는 경우**: `rule-details/common/session-continuity.md`를 읽고 이전 세션 재개 지침을 따름
- **존재하지 않는 경우**: 새 workflow임 - 3단계로 진행

### 3. 질문 스타일에 대한 사용자 선호도 묻기

전체 workflow 규칙을 로드하기 전에 `AskUserQuestion`을 사용하여 사용자가 질문에 답변하는 방법을 물어봅니다:

```json
{
  "questions": [
    {
      "question": "How would you like to answer questions throughout this workflow?",
      "header": "Q&A Style",
      "multiSelect": false,
      "options": [
        {
          "label": "Interactive UI",
          "description": "Clickable buttons/options (recommended for ease of use)"
        },
        {
          "label": "Text responses",
          "description": "Type answers like '1: A, 2: B' (faster if you prefer typing)"
        }
      ]
    }
  ]
}
```

workflow 전체에서 참조할 변수에 사용자의 선호도를 저장합니다. 이것은 이후 단계에서 명확화 질문을 할 때 어떤 형식을 사용할지 결정합니다.

### 4. Core Rules 로드

workflow와 공통 규칙을 이해하기 위해 다음 파일을 읽으세요:
1. `rule-details/core-workflow.md` - 메인 조율 로직 (중요)
2. `rule-details/common/process-overview.md` - 고수준 개요
3. `rule-details/common/question-format-guide.md` - 사용자와 상호작용하는 방법 (3단계의 사용자 선호도 존중)
4. `rule-details/common/content-validation.md` - 품질 기준
5. `rule-details/common/terminology.md` - 주요 용어

### 5. Workspace 초기화

`aidlc-docs/` 디렉토리가 존재하지 않으면 생성:

```bash
mkdir -p aidlc-docs
```

세션 연속성을 위해 `aidlc-docs/aidlc-preferences.md`에 사용자의 질문 선호도 저장:

```markdown
# AI-DLC User Preferences

**Question Style**: [Interactive UI / Text responses]
**Set on**: [ISO timestamp]
```

### 6. Inception Phase 시작

`rule-details/inception/workspace-detection.md`를 읽고 Workspace Detection 단계를 실행하여 Greenfield 또는 Brownfield 프로젝트인지 확인합니다.

### 7. Core Workflow 따르기

이 시점부터 `rule-details/core-workflow.md`에 정의된 조율 로직을 따릅니다. 이것은 다음을 통해 안내합니다:
- 나머지 Inception 단계 (Requirements Analysis, User Stories, Workflow Planning, Application Design, Units Generation)
- Construction 단계 (단위별: Functional Design → NFR Requirements → NFR Design → Infrastructure Design → Code Generation)
- Build and Test
- Operations (해당되는 경우)

## 핵심 원칙

1. **Chat 기반 Q&A**: 항상 대화에서 직접 질문합니다. 사용자에게 질문에 답하기 위해 파일을 편집하도록 요청하지 마세요.

2. **승인 게이트**: 지정된 승인 게이트를 통과하기 전에 명시적인 사용자 승인을 기다립니다.

3. **진행 상황 추적**: 모든 단계 전환 시 체크박스 형식으로 `aidlc-docs/aidlc-state.md`를 업데이트합니다:
   ```markdown
   - [x] Workspace Detection - COMPLETED
   - [ ] Requirements Analysis - NEXT
   ```

4. **감사 추적**: 타임스탬프와 함께 모든 주요 결정 및 단계 전환을 `aidlc-docs/audit.md`에 기록합니다.

5. **실행 전 읽기**: 해당 단계를 실행하기 전에 항상 해당 단계의 관련 rule-detail 파일을 읽으세요.

6. **품질 기준**: 모든 결과물에 대해 `rule-details/common/content-validation.md`의 콘텐츠 검증 규칙을 따릅니다.

7. **오류 처리**: 문제가 발생하면 `rule-details/common/error-handling.md`를 읽고 지침을 확인하세요.

8. **Workflow 변경**: 사용자가 표준 workflow에서 벗어난 것을 요청하면 `rule-details/common/workflow-changes.md`를 읽으세요.

## 세션 연속성

이 세션이 종료되고 나중에 재개되는 경우:
- 사용자는 인수 없이 `/aidlc:start`를 다시 실행할 수 있습니다
- `aidlc-docs/aidlc-state.md`를 감지하고 마지막 체크포인트부터 재개합니다
- `rule-details/common/session-continuity.md`의 세션 재개 로직을 따릅니다

## 결과물 디렉토리 구조

모든 결과물은 다음 위치에 생성됩니다:

```
aidlc-docs/
├── aidlc-state.md              # 진행 상황 추적 (체크박스)
├── audit.md                    # 타임스탬프가 있는 감사 추적
├── workspace-analysis.md       # Workspace 감지 결과
├── requirements.md             # 요구사항 분석
├── user-stories.md             # User stories (해당되는 경우)
├── workflow-plan.md            # 계획된 단계
├── application-design.md       # Application 아키텍처
├── units.md                    # 작업 단위 분해
└── units/                      # 단위별 결과물
    ├── unit-01/
    │   ├── functional-design.md
    │   ├── nfr-requirements.md
    │   ├── nfr-design.md
    │   ├── infrastructure-design.md
    │   └── implementation-notes.md
    └── unit-02/
        └── ...
```

## 중요 사항

- **파일 참조**: 사용자에 대한 응답에서 rule-detail 파일을 참조할 때 skill 디렉토리의 상대 경로를 사용하세요 (예: "rule-details/common/welcome-message.md")
- **환각 금지**: rule-detail 파일에 명시적으로 작성된 규칙만 따르세요. workflow 단계를 발명하거나 가정하지 마세요.
- **필요 시 읽기**: 모든 규칙 파일을 한 번에 읽을 필요는 없습니다. 각 단계에 진입할 때 읽으세요.
- **사용자 주도**: 사용자가 제어합니다. 진행하기 전에 게이트에서 항상 승인을 기다리세요.

---

**지금 시작**: `rule-details/common/welcome-message.md`를 읽고 표시한 다음 위의 초기화 순서를 진행하세요.
