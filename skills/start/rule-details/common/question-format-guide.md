# Question Format Guide

## 필수: 먼저 사용자의 질문 선호도 확인

**중요**: 질문하기 전에 `aidlc-docs/aidlc-preferences.md`에서 사용자가 선호하는 질문 스타일을 확인하세요.
- **선호도가 "Interactive UI"인 경우**: `AskUserQuestion` tool 사용 (아래 섹션 A)
- **선호도가 "Text responses"인 경우**: 텍스트 기반 질문 사용 (아래 섹션 B)

---

# 섹션 A: Interactive UI 형식 (AskUserQuestion Tool)

## 사용자가 Interactive UI를 선호하는 경우

### 규칙: Claude Code의 네이티브 질문 도구 사용
**중요**: 질문을 하려면 반드시 `AskUserQuestion` tool을 사용해야 합니다. 이 도구는 쉽게 선택할 수 있는 클릭 가능한 옵션을 제공합니다. 사용자가 채워야 하는 질문 파일을 생성하지 마세요.

### AskUserQuestion Tool 사용하기

#### 사용 시기
- **요구사항 수집**: 사용자 요구사항을 명확히 해야 할 때
- **설계 결정**: 여러 유효한 접근 방식이 존재할 때
- **모호성 해결**: 사용자 응답에 대한 명확화가 필요할 때
- **계획 질문**: inception 또는 construction 계획 단계 중

#### Tool 매개변수

```json
{
  "questions": [
    {
      "question": "What is the primary user authentication method?",
      "header": "Auth Method",
      "multiSelect": false,
      "options": [
        {
          "label": "Username and password",
          "description": "Traditional credentials-based authentication"
        },
        {
          "label": "Social media login",
          "description": "OAuth with Google, Facebook, etc."
        },
        {
          "label": "Single Sign-On (SSO)",
          "description": "Enterprise SSO integration"
        },
        {
          "label": "Multi-factor authentication",
          "description": "Enhanced security with 2FA/MFA"
        }
      ]
    }
  ]
}
```

**중요 가이드라인**:
- `AskUserQuestion` 호출당 1-4개의 질문 요청 (tool 제한)
- 각 질문은 칩으로 표시되는 짧은 `header` (최대 12자) 필요
- 각 질문은 2-4개의 `options` 필요 (tool에서 강제)
- 각 옵션은 `label` (1-5단어)과 `description` (선택 설명) 필요
- 단일 선택 질문은 `multiSelect: false` 설정 (기본값)
- 여러 옵션 선택 가능할 때는 `multiSelect: true` 설정
- tool은 자동으로 사용자 정의 응답을 위한 "Other" 옵션 제공

#### 질문 그룹화 전략

**간단한 세트 (1-4개 질문)**: 단일 `AskUserQuestion` 호출 사용
```
모든 질문을 한 번의 호출로 AskUserQuestion tool 사용
```

**중간 세트 (5-8개 질문)**: 주제별로 2개 그룹으로 분할
```
먼저, 핵심 질문(1-4개)에 대해 AskUserQuestion 사용
그다음, 후속 질문(1-4개)에 대해 AskUserQuestion 사용
```

**대규모 세트 (9개 이상 질문)**: 3개 이상의 논리적 단계로 분할
```
Phase 1: 첫 번째 주제(1-4개 질문)에 대해 AskUserQuestion 사용
Phase 2: 두 번째 주제(1-4개 질문)에 대해 AskUserQuestion 사용
Phase 3: 세 번째 주제(1-4개 질문)에 대해 AskUserQuestion 사용
```

### 완전한 예제

#### 예제 1: 요구사항 명확화 (3개 질문)

```json
{
  "questions": [
    {
      "question": "What is the primary user authentication method?",
      "header": "Auth",
      "multiSelect": false,
      "options": [
        {
          "label": "Username/password",
          "description": "Traditional credentials-based authentication"
        },
        {
          "label": "Social login",
          "description": "OAuth with Google, Facebook, etc."
        },
        {
          "label": "SSO",
          "description": "Enterprise Single Sign-On"
        },
        {
          "label": "MFA",
          "description": "Multi-factor authentication"
        }
      ]
    },
    {
      "question": "Will this be a web or mobile application?",
      "header": "Platform",
      "multiSelect": false,
      "options": [
        {
          "label": "Web application",
          "description": "Browser-based application"
        },
        {
          "label": "Mobile app",
          "description": "iOS/Android native or hybrid"
        },
        {
          "label": "Both",
          "description": "Web and mobile applications"
        }
      ]
    },
    {
      "question": "Is this a new project or existing codebase?",
      "header": "Type",
      "multiSelect": false,
      "options": [
        {
          "label": "Greenfield",
          "description": "New project from scratch"
        },
        {
          "label": "Brownfield",
          "description": "Existing codebase with changes"
        }
      ]
    }
  ]
}
```

#### 예제 2: 다중 선택 질문

```json
{
  "questions": [
    {
      "question": "Which features do you want to enable?",
      "header": "Features",
      "multiSelect": true,
      "options": [
        {
          "label": "User profiles",
          "description": "User account management and profiles"
        },
        {
          "label": "Notifications",
          "description": "Email and push notifications"
        },
        {
          "label": "Analytics",
          "description": "Usage tracking and reporting"
        },
        {
          "label": "API access",
          "description": "Programmatic API for integrations"
        }
      ]
    }
  ]
}
```

### 사용자 응답 처리

`AskUserQuestion` 호출 후, tool은 사용자 답변을 반환합니다. 다음과 같이 처리하세요.

1. **응답 파싱**: `answers` 객체에서 사용자 선택 추출
2. **완성도 검증**: 모든 질문이 답변되었는지 확인
3. **"Other" 확인**: 사용자가 "Other"를 선택한 경우, 사용자 정의 텍스트 제공
4. **모순 분석**: 논리적으로 일관성 없는 답변 확인
5. **필요시 후속 질문**: 명확화를 위해 다른 `AskUserQuestion` 호출 사용

### 감사 추적을 위한 Q&A 기록

모든 답변을 수집한 후, 요약 파일 생성:

**파일**: `aidlc-docs/{phase-name}/questions-summary.md`

**형식**:
```markdown
# [Phase Name] Questions and Answers

**Date**: [ISO timestamp]

## Question 1
**Question**: What is the primary user authentication method?
**Answer**: Single Sign-On (SSO)
**Reasoning**: Enterprise SSO integration

## Question 2
**Question**: Will this be a web or mobile application?
**Answer**: Web application
**Reasoning**: Browser-based application

## Question 3
**Question**: Is this a new project or existing codebase?
**Answer**: Existing codebase (brownfield)
**Reasoning**: Working with existing code

---
**Summary**: User confirmed SSO authentication for a web-based brownfield project.
```

### 오류 처리

#### 답변 누락
질문에 답변이 없는 경우 (tool에서는 발생하지 않아야 하지만 확인):
```
I noticed Question [X] wasn't answered. Let me ask that again.
[해당 질문만으로 AskUserQuestion 사용]
```

#### 모호한 사용자 정의 응답
사용자가 불명확한 "Other" 텍스트를 제공한 경우:
```
Thank you for that context. Let me clarify with a follow-up question.
[명확화 질문으로 AskUserQuestion 사용]
```

### 모순 및 모호성 감지

**필수**: 사용자 응답을 받은 후, 모순과 모호성을 반드시 확인해야 합니다.

#### 모순 감지
논리적으로 일관성 없는 답변 찾기:
- 범위 불일치: "Bug fix"이지만 "Entire codebase affected"
- 위험 불일치: "Low risk"이지만 "Breaking changes"
- 일정 불일치: "Quick fix"이지만 "Multiple subsystems"
- 영향 불일치: "Single component"이지만 "Significant architecture changes"

#### 모호성 감지
불명확하거나 경계선 응답 찾기:
- 여러 분류에 적합할 수 있는 답변
- 구체성이 부족한 응답
- 여러 질문에 걸쳐 상충되는 지표

#### 모순 및 모호성 처리

모순이나 모호성이 감지되면, `AskUserQuestion`을 사용하여 즉시 명확화 질문:

**예제**:
```json
{
  "questions": [
    {
      "question": "I noticed you indicated 'bug fix' but also 'entire codebase affected'. Which better describes the scope?",
      "header": "Scope",
      "multiSelect": false,
      "options": [
        {
          "label": "Isolated bug fix",
          "description": "Small, single-component fix"
        },
        {
          "label": "Multi-component fix",
          "description": "Bug fix requiring changes across components"
        },
        {
          "label": "Large refactoring",
          "description": "Major changes disguised as a bug fix"
        }
      ]
    }
  ]
}
```

#### 명확화 워크플로우

1. **감지**: 모든 응답을 즉시 분석하여 모순/모호성 확인
2. **질문**: 명확화 질문을 바로 제시하기 위해 `AskUserQuestion` 사용
3. **대기**: Tool이 사용자 응답을 자동으로 대기 처리
4. **재검증**: 명확화 후, 일관성 재확인
5. **기록**: questions-summary.md 파일에 명확화 내용 포함
6. **진행**: 모든 모순이 해결된 후에만 진행

### 모범 사례

1. **구체적으로**: 질문은 명확하고 모호하지 않아야 함
2. **포괄적으로**: 모든 필요한 정보를 다루되, 호출당 1-4개 질문 제한 존중
3. **간결하게**: 짧은 header (최대 12자)와 명확한 label (1-5단어) 사용
4. **실용적으로**: 옵션은 현실적이고 실행 가능해야 함
5. **설명적으로**: 각 옵션에 대해 유용한 설명 제공
6. **유연하게**: Tool이 자동으로 "Other" 옵션 제공
7. **철저하게**: 진행하기 전에 항상 모순 확인

### 단계별 예제

#### 예제: 2개 옵션이 있는 요구사항

```json
{
  "questions": [
    {
      "question": "Is this a new project or existing codebase?",
      "header": "Type",
      "multiSelect": false,
      "options": [
        {
          "label": "Greenfield",
          "description": "New project from scratch"
        },
        {
          "label": "Brownfield",
          "description": "Existing codebase"
        }
      ]
    }
  ]
}
```

#### 예제: 3개 옵션이 있는 아키텍처

```json
{
  "questions": [
    {
      "question": "What is the deployment target?",
      "header": "Deploy",
      "multiSelect": false,
      "options": [
        {
          "label": "Cloud",
          "description": "AWS, Azure, or GCP"
        },
        {
          "label": "On-premises",
          "description": "Self-hosted servers"
        },
        {
          "label": "Hybrid",
          "description": "Both cloud and on-premises"
        }
      ]
    }
  ]
}
```

#### 예제: 4개 옵션이 있는 패턴

```json
{
  "questions": [
    {
      "question": "What architectural pattern should be used?",
      "header": "Architecture",
      "multiSelect": false,
      "options": [
        {
          "label": "Monolithic",
          "description": "Single unified application"
        },
        {
          "label": "Microservices",
          "description": "Distributed service architecture"
        },
        {
          "label": "Serverless",
          "description": "Function-as-a-Service approach"
        },
        {
          "label": "Event-driven",
          "description": "Message-based architecture"
        }
      ]
    }
  ]
}
```

---

# 섹션 B: 텍스트 기반 형식

## 사용자가 텍스트 응답을 선호하는 경우

### 규칙: 대화형 텍스트 기반 질문 사용
사용자가 텍스트 응답을 선호하는 경우, 사용자가 문자 선택이나 설명으로 응답할 수 있도록 명확한 번호 형식으로 질문을 제시하세요.

### 텍스트 기반 질문 형식

대화에서 다음 구조로 질문을 명확하게 제시:

```
[stage name] 진행을 위해 [X]개 항목을 명확히 해야 합니다:

**Question 1: [명확하고 구체적인 질문 텍스트]**
A) [첫 번째 의미 있는 옵션]
B) [두 번째 의미 있는 옵션]
C) [필요에 따라 추가 옵션]
D) Other (please describe)

**Question 2: [다음 질문]**
A) [옵션 1]
B) [옵션 2]
C) Other (please describe)

문자 선택(예: "1: A, 2: B")을 제공하거나 "Other" 선택 시 답변을 설명해주세요.
```

**가이드라인**:
- 명확한 번호 형식으로 질문 제시
- 유연성을 위해 항상 마지막 옵션으로 "Other" 포함
- 의미 있는 옵션만 포함 - 빈 칸을 채우기 위해 옵션을 만들지 마세요
- 의미 있는 만큼의 옵션 사용 (최소 2 + Other)
- 간단한 질문(1-3개)은 한 번에 모두 제시
- 복잡한 질문 세트(4개 이상)는 논리적 세트로 그룹화 고려

### 사용자 응답 형식
사용자는 대화에서 직접 답변:

**간결한 형식**:
```
1: C, 2: A, 3: B
```

**상세 형식**:
```
Question 1: C (SSO)
Question 2: A (Web application)
Question 3: B (Brownfield)
```

**"Other"와 혼합**:
```
1: D - We want to use OAuth 2.0 with Google Workspace
2: A
3: B
```

### 사용자 응답 처리
답변을 받은 후:
1. 모든 응답 파싱 및 검증
2. 모순 및 모호성 확인
3. 명확화가 필요한 경우, 즉시 후속 질문
4. 감사 추적을 위해 `aidlc-docs/{phase-name}/questions-summary.md`에 Q&A 요약 기록

### 모순 감지 (섹션 A와 동일)
위 섹션 A에 설명된 것과 동일한 모순 감지 및 해결 프로세스를 따르세요.

---

## 요약

**기억하세요**:
- ✅ 항상 먼저 `aidlc-docs/aidlc-preferences.md`에서 사용자 선호도 확인
- ✅ 사용자가 "Interactive UI"를 선호하면 `AskUserQuestion` 사용
- ✅ 사용자가 "Text responses"를 선호하면 텍스트 기반 질문 사용
- ✅ 즉시 모순에 대한 응답 검증
- ✅ 사용자가 선호하는 동일한 형식을 사용하여 후속 질문
- ✅ 감사 추적을 위해 aidlc-docs/에 Q&A 요약 기록
- ❌ 사용자가 편집할 질문 파일을 절대 생성하지 마세요
- ❌ 답변 없이 절대 진행하지 마세요
- ❌ 해결되지 않은 모순과 함께 절대 진행하지 마세요
- ❌ 모호한 응답에 대해 절대 가정하지 마세요
