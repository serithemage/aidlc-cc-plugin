# Requirements Analysis (Adaptive)

**역할 수행** product owner

**적응형 단계**: 항상 실행됨. 세부 수준은 문제 복잡도에 따라 조정됨.

**적응형 깊이 설명은 [depth-levels.md](../common/depth-levels.md) 참조**

## 전제 조건
- Workspace Detection이 완료되어야 함
- Reverse Engineering이 완료되어야 함 (brownfield인 경우)

## 실행 단계

### Step 1: Reverse Engineering 컨텍스트 로드 (있는 경우)

**Brownfield 프로젝트인 경우**:
- `aidlc-docs/inception/reverse-engineering/architecture.md` 로드
- `aidlc-docs/inception/reverse-engineering/component-inventory.md` 로드
- `aidlc-docs/inception/reverse-engineering/technology-stack.md` 로드
- 요청 분석 시 기존 시스템을 이해하기 위해 이들을 사용

### Step 2: 사용자 요청 분석 (의도 분석)

#### 2.1 요청 명확성
- **명확함**: 구체적이고 잘 정의되어 있으며 실행 가능
- **모호함**: 일반적이고 애매하며 명확화 필요
- **불완전함**: 주요 정보 누락

#### 2.2 요청 유형
- **New Feature**: 새로운 기능 추가
- **Bug Fix**: 기존 이슈 수정
- **Refactoring**: 코드 구조 개선
- **Upgrade**: 의존성 또는 프레임워크 업데이트
- **Migration**: 다른 기술로 이동
- **Enhancement**: 기존 기능 개선
- **New Project**: 처음부터 시작

#### 2.3 초기 범위 추정
- **Single File**: 한 파일에 대한 변경
- **Single Component**: 하나의 컴포넌트/패키지에 대한 변경
- **Multiple Components**: 여러 컴포넌트에 걸친 변경
- **System-wide**: 전체 시스템에 영향을 미치는 변경
- **Cross-system**: 여러 시스템에 영향을 미치는 변경

#### 2.4 초기 복잡도 추정
- **Trivial**: 단순하고 직관적인 변경
- **Simple**: 명확한 구현 경로
- **Moderate**: 일부 복잡도, 여러 고려 사항
- **Complex**: 상당한 복잡도, 많은 고려 사항

### Step 3: 요구사항 깊이 결정

**요청 분석을 기반으로 깊이 결정:**

**Minimal Depth** - 다음의 경우 사용:
- 요청이 명확하고 단순함
- 상세한 요구사항이 필요하지 않음
- 기본 이해만 문서화하면 됨

**Standard Depth** - 다음의 경우 사용:
- 요청에 명확화가 필요함
- 기능적 및 비기능적 요구사항이 필요함
- 일반적인 복잡도

**Comprehensive Depth** - 다음의 경우 사용:
- 여러 이해관계자가 있는 복잡한 프로젝트
- 높은 위험 또는 중요한 시스템
- 추적 가능성이 있는 상세한 요구사항 필요

### Step 4: 현재 요구사항 평가

사용자가 제공한 모든 것을 분석:
   - 의도 진술 또는 설명 (이미 audit.md에 기록됨)
   - 기존 요구사항 문서 (언급된 경우 워크스페이스 검색)
   - 붙여넣은 내용 또는 파일 참조
   - 마크다운이 아닌 문서를 마크다운 형식으로 변환

### Step 5: 철저한 완전성 분석

**중요**: 포괄적인 분석을 사용하여 요구사항 완전성을 평가. 모호성이나 누락된 세부 사항이 있을 때 질문하는 것을 기본으로 함.

**필수**: 다음 모든 영역을 평가하고 불명확한 것이 있으면 질문:
- **Functional Requirements**: 핵심 기능, 사용자 상호작용, 시스템 동작
- **Non-Functional Requirements**: 성능, 보안, 확장성, 사용성
- **User Scenarios**: 사용 사례, 사용자 여정, 엣지 케이스, 오류 시나리오
- **Business Context**: 목표, 제약 사항, 성공 기준, 이해관계자 요구
- **Technical Context**: 통합 포인트, 데이터 요구사항, 시스템 경계
- **Quality Attributes**: 신뢰성, 유지보수성, 테스트 가능성, 접근성

**의심스러울 때는 질문하기** - 불완전한 요구사항은 잘못된 구현으로 이어짐.

### Step 6: 명확화 질문하기 (적극적 접근)
   - 요구사항이 예외적으로 명확하고 완전하지 않은 한 **항상** `AskUserQuestion` 도구를 사용하여 명확화 질문을 함
   - 누락되거나 불명확하거나 애매한 영역에 대해 질문
   - 기능적 요구사항, 비기능적 요구사항, 사용자 시나리오 및 비즈니스 컨텍스트에 초점
   - **중요**: `AskUserQuestion` 도구 사용 (텍스트 기반 질문이 아님) - 전체 지침은 `common/question-format-guide.md` 참조
   - 다음 가이드라인에 따라 질문 구조화:
     - `AskUserQuestion` 호출당 1-4개의 질문 (도구 제한)
     - 각 질문에 짧은 헤더 제공 (최대 12자)
     - 질문당 레이블과 설명이 있는 2-4개의 옵션 포함
     - 도구가 사용자 정의 응답을 위한 "Other" 옵션을 자동으로 제공
   - **필수**: 모든 답변을 분석하여 애매한 부분이 있으면 `AskUserQuestion`을 다시 사용하여 후속 질문
   - **필수**: 모든 애매함이 해결되거나 사용자가 명시적으로 진행을 요청할 때까지 계속 질문
   - **답변 수집 후**: Q&A를 감사 추적을 위해 기록하기 위해 `aidlc-docs/inception/requirements/questions-summary.md` 생성

### Step 7: 요구사항 문서 생성
   - `aidlc-docs/inception/requirements/requirements.md` 생성
   - 상단에 의도 분석 요약 포함:
     - 사용자 요청
     - 요청 유형
     - 범위 추정
     - 복잡도 추정
   - 기능적 및 비기능적 요구사항 모두 포함
   - 명확화 질문에 대한 사용자의 답변 통합
   - 주요 요구사항에 대한 간략한 요약 제공

### Step 8: 상태 추적 업데이트

`aidlc-docs/aidlc-state.md` 업데이트:

```markdown
## Stage Progress
### 🔵 INCEPTION PHASE
- [x] Workspace Detection
- [x] Reverse Engineering (해당하는 경우)
- [x] Requirements Analysis
```

### Step 9: 기록 및 진행
   - 타임스탬프와 함께 승인 프롬프트를 `aidlc-docs/audit.md`에 기록
   - 다음 구조로 완료 메시지 제시:
     1. **완료 발표** (필수): 항상 이것으로 시작:

```markdown
# 🔍 Requirements Analysis Complete
```

     2. **AI 요약** (선택): 요구사항의 구조화된 글머리 기호 요약 제공
        - 형식: "Requirements analysis has identified [프로젝트 유형/복잡도]:"
        - 주요 기능적 요구사항 나열 (글머리 기호)
        - 주요 비기능적 요구사항 나열 (글머리 기호)
        - 관련이 있으면 아키텍처 고려사항이나 기술적 결정 언급
        - 워크플로 지침 포함하지 말 것 ("please review", "let me know", "proceed to next phase", "before we proceed")
        - 사실적이고 내용 중심으로 유지
     3. **형식화된 워크플로 메시지** (필수): 항상 이 정확한 형식으로 끝내기:

```markdown
> **📋 <u>검토 필요:</u>**
> 요구사항 문서를 확인해 주세요: `aidlc-docs/inception/requirements/requirements.md`



> **🚀 <u>다음 단계는?</u>**
>
> **선택 가능:**
>
> 🔧 **변경 요청** - 검토에 따라 필요시 요구사항에 대한 수정 요청
> [User Stories를 건너뛰는 경우 이 옵션 추가:]
> 📝 **User Stories 추가** - **User Stories** 단계를 포함하도록 선택 (현재 프로젝트 단순성에 따라 건너뛰기로 설정됨)
> ✅ **승인 및 계속** - 요구사항 승인 후 **[User Stories/Workflow Planning]** 로 진행

---
```

**참고**: User Stories 단계를 건너뛸 경우에만 "Add User Stories" 옵션 포함. [User Stories/Workflow Planning]을 실제 다음 단계 이름으로 교체.

   - 진행하기 전에 명시적인 사용자 승인 대기
   - 타임스탬프와 함께 승인 응답 기록
   - aidlc-state.md에서 Requirements Analysis 단계 완료로 업데이트
