# User Stories - Detailed Steps

## 목적
**요구사항을 수락 기준이 있는 사용자 중심 스토리로 변환**

User Stories는 다음에 초점을 맞춤:
- 비즈니스 요구사항을 사용자 중심 내러티브로 번역
- 각 스토리에 대한 명확한 수락 기준 정의
- 다양한 이해관계자 유형을 나타내는 사용자 페르소나 생성
- 팀 간 공유 이해 확립
- 구현을 위한 테스트 가능한 사양 제공

## 전제 조건
- Workspace Detection이 완료되어야 함
- Requirements Analysis 권장 (요구사항이 있으면 참조 가능)
- Workflow Planning이 User Stories 단계를 실행하도록 표시해야 함

## 지능형 평가 가이드라인

**USER STORIES 실행 시기**: 진행하기 전에 이 향상된 평가 사용:

### 높은 우선순위 실행 (항상 실행)
- **New User Features**: 사용자가 직접 상호작용할 새로운 기능
- **User Experience Changes**: 기존 사용자 워크플로 또는 인터페이스 수정
- **Multi-Persona Systems**: 다양한 유형의 사용자를 서비스하는 애플리케이션
- **Customer-Facing APIs**: 외부 사용자 또는 시스템이 소비할 서비스
- **Complex Business Logic**: 여러 시나리오 또는 비즈니스 규칙이 있는 요구사항
- **Cross-Team Projects**: 여러 팀 간 공유 이해가 필요한 작업

### 중간 우선순위 실행 (복잡도 평가)
- **Backend User Impact**: 사용자 경험에 간접적으로 영향을 미치는 내부 변경
- **Performance Improvements**: 사용자가 볼 수 있는 이점이 있는 향상
- **Integration Work**: 사용자 워크플로에 영향을 미치는 시스템 연결
- **Data Changes**: 사용자 데이터, 보고서 또는 분석에 영향을 미치는 수정
- **Security Enhancements**: 사용자 인증 또는 권한에 영향을 미치는 변경

### 복잡도 평가 요소
중간 우선순위의 경우, 다음 중 하나라도 해당되면 user stories 실행:
- **Scope**: 여러 컴포넌트 또는 사용자 터치포인트에 걸친 변경
- **Ambiguity**: 스토리를 통해 명확히 할 수 있는 불명확한 측면이 있는 요구사항
- **Risk**: 높은 비즈니스 영향 또는 오해 가능성
- **Stakeholders**: 요구사항에 여러 비즈니스 이해관계자 관련
- **Testing**: 사용자 수락 테스트 필요
- **Options**: 여러 유효한 구현 접근법 존재

### 단순한 경우에만 건너뛰기
- **Pure Refactoring**: 사용자 영향이 전혀 없는 내부 코드 개선
- **Isolated Bug Fixes**: 명확한 범위의 단순하고 잘 정의된 수정
- **Infrastructure Only**: 사용자 대면 효과가 없는 변경
- **Developer Tooling**: 빌드 프로세스, CI/CD 또는 개발 환경 변경
- **Documentation**: 기능에 영향을 미치지 않는 업데이트

### 기본 결정 규칙
**의심스러울 때는 user stories를 포함하고 명확화 질문을 하기.** 적절한 명확화와 함께 포괄적인 스토리를 만드는 오버헤드는 일반적으로 다음의 이점으로 상쇄됨:
- 더 명확한 요구사항 이해
- 더 나은 팀 정렬
- 개선된 테스트 기준
- 향상된 이해관계자 커뮤니케이션
- 구현 위험 감소
- 개발 중 비용이 많이 드는 변경 감소
- 더 나은 사용자 경험 결과

---

# PART 1: PLANNING

## Step 1: User Stories 필요성 검증 (필수)

**중요**: user stories를 진행하기 전에 이 평가 수행:

### 평가 프로세스
1. **요청 컨텍스트 분석**:
   - 원래 사용자 요청 및 요구사항 검토
   - 사용자 대면 vs 내부 전용 변경 식별
   - 작업의 복잡도 및 범위 평가
   - 비즈니스 이해관계자 관여 평가

2. **평가 기준 적용**:
   - 높은 우선순위 지표 확인 (항상 실행)
   - 중간 우선순위 요소 평가 (복잡도 기반 결정)
   - 건너뛰어야 하는 단순한 경우가 아닌지 확인

3. **평가 결정 문서화**:
   - `aidlc-docs/inception/plans/user-stories-assessment.md` 생성
   - 이 요청에 대해 user stories가 가치 있는 이유에 대한 근거 포함
   - 적용되는 특정 평가 기준 참조
   - 예상되는 이점 설명 (명확성, 테스트, 이해관계자 정렬)

4. **정당화된 경우에만 진행**:
   - User stories는 프로젝트에 명확한 가치를 추가해야 함
   - 평가는 오버헤드를 상쇄하는 구체적인 이점을 보여주어야 함
   - 결정은 프로젝트 이해관계자에게 정당화 가능해야 함

### 평가 문서 템플릿
```markdown
# User Stories Assessment

## Request Analysis
- **Original Request**: [간략한 요약]
- **User Impact**: [Direct/Indirect/None]
- **Complexity Level**: [Simple/Medium/Complex]
- **Stakeholders**: [관련 당사자 나열]

## Assessment Criteria Met
- [ ] High Priority: [적용 가능한 기준 나열]
- [ ] Medium Priority: [복잡도 정당화와 함께 적용 가능한 기준 나열]
- [ ] Benefits: [user stories에서 예상되는 가치]

## Decision
**Execute User Stories**: [Yes/No]
**Reasoning**: [상세한 정당화]

## Expected Outcomes
- [user stories가 제공할 특정 이점 나열]
- [스토리가 프로젝트 성공을 개선하는 방법]
```

## Step 2: 스토리 계획 생성
- product owner 역할 수행
- 스토리 개발을 위한 단계별 실행 체크리스트가 포함된 포괄적인 계획 생성
- 각 단계와 하위 단계는 체크박스 []를 가져야 함
- 요구사항을 user stories로 변환하기 위한 방법론 및 접근법에 초점

## Step 3: 컨텍스트에 적합한 질문 생성
**지시**: 요구사항과 컨텍스트를 철저히 분석하여 스토리 품질과 팀 이해를 개선할 명확화가 필요한 모든 영역을 식별. 포괄적인 user story 개발을 보장하기 위해 질문에 적극적으로 임함.

**중요**: 스토리 품질에 영향을 줄 수 있는 애매함이나 누락된 세부 사항이 있을 때 질문하는 것을 기본으로 함. 불완전하거나 불명확한 스토리를 만드는 것보다 너무 많은 질문을 하는 것이 더 나음.

**전체 질문 형식 규칙은 `common/question-format-guide.md` 참조**

- **중요**: `AskUserQuestion` 도구를 사용하여 질문 준비 (텍스트 기반 질문이 아님)
- 애매함, 누락된 정보 또는 명확화가 필요한 영역에 초점
- 사용자 입력이 스토리 생성 결정을 개선할 수 있는 곳에 질문 생성
- **의심스러울 때는 질문하기** - 과신은 잘못된 스토리로 이어짐

**평가할 질문 카테고리** (모든 카테고리 고려):
- **User Personas** - 사용자 유형, 역할, 특성 및 동기에 대해 질문
- **Story Granularity** - 적절한 세부 수준, 스토리 크기 및 분해 접근법에 대해 질문
- **Story Format** - 형식 선호도, 템플릿 사용 및 문서화 표준에 대해 질문
- **Breakdown Approach** - 조직 방법, 우선순위 지정 및 그룹화 전략에 대해 질문
- **Acceptance Criteria** - 세부 수준, 형식, 테스트 접근법 및 검증 방법에 대해 질문
- **User Journeys** - 사용자 워크플로, 상호작용 패턴 및 경험 흐름에 대해 질문
- **Business Context** - 비즈니스 목표, 성공 지표 및 이해관계자 요구에 대해 질문
- **Technical Constraints** - 기술적 제한, 통합 요구사항 및 시스템 경계에 대해 질문

## Step 4: 계획에 필수 스토리 아티팩트 포함
- **항상** 스토리 계획에 다음 필수 아티팩트를 포함:
  - [ ] INVEST 기준에 따라 user stories가 있는 stories.md 생성
  - [ ] 사용자 원형 및 특성이 있는 personas.md 생성
  - [ ] 스토리가 Independent, Negotiable, Valuable, Estimable, Small, Testable인지 확인
  - [ ] 각 스토리에 대한 수락 기준 포함
  - [ ] 페르소나를 관련 user stories에 매핑

## Step 5: 스토리 옵션 제시
- 계획 문서에 스토리 분해를 위한 다양한 접근법 포함:
  - **User Journey-Based**: 스토리가 사용자 워크플로 및 상호작용을 따름
  - **Feature-Based**: 시스템 기능 및 역량을 중심으로 스토리 조직
  - **Persona-Based**: 다양한 사용자 유형과 그들의 요구에 따라 스토리 그룹화
  - **Domain-Based**: 비즈니스 도메인 또는 컨텍스트를 중심으로 스토리 조직
  - **Epic-Based**: 하위 스토리가 있는 계층적 에픽으로 스토리 구조화
- 각 접근법의 트레이드오프와 이점 설명
- 명확한 결정 기준이 있는 하이브리드 접근법 허용

## Step 6: 스토리 계획 저장
- `aidlc-docs/inception/plans/` 디렉토리에 완전한 스토리 계획 저장
- 파일명: `story-generation-plan.md`
- 계획이 포괄적이고 모든 스토리 개발 측면을 다루는지 확인

## Step 7: AskUserQuestion 도구를 사용하여 질문하기
- **중요**: `AskUserQuestion` 도구 사용 (텍스트 기반 질문이 아님)하여 모든 계획 질문 제시
- 도구 사용에 대한 전체 지침은 `common/question-format-guide.md` 참조
- 다음 가이드라인에 따라 질문 구조화:
  - `AskUserQuestion` 호출당 1-4개의 질문 (도구 제한)
  - 각 질문에 짧은 헤더 제공 (최대 12자)
  - 질문당 레이블과 설명이 있는 2-4개의 옵션 포함
  - 도구가 사용자 정의 응답을 위한 "Other" 옵션을 자동으로 제공
- 감사 추적 및 결정 문서화의 중요성 강조
- 진행하기 전에 모든 질문에 답변해야 함을 설명

## Step 8: AskUserQuestion 도구에서 답변 수집
- `AskUserQuestion` 도구가 사용자 응답 대기 및 수집을 자동으로 처리
- 모든 질문에 답변될 때까지 진행하지 않음 (도구가 이를 강제함)
- 답변 수집 후, 감사 추적을 위해 Q&A를 기록하기 위해 `aidlc-docs/inception/plans/story-questions-summary.md` 생성

## Step 9: 답변 분석 (필수)
진행하기 전에 다음에 대해 모든 사용자 답변을 신중하게 검토해야 함:
- **모호하거나 애매한 응답**: "mix of", "somewhere between", "not sure", "depends", "maybe", "probably"
- **정의되지 않은 기준이나 용어**: 명확한 정의 없이 개념에 대한 참조
- **모순되는 답변**: 서로 충돌하는 응답
- **누락된 생성 세부 사항**: 구현에 대한 구체적인 지침이 부족한 답변
- **옵션을 결합하는 답변**: 명확한 결정 규칙 없이 다양한 접근법을 병합하는 응답
- **불완전한 설명**: 정의하지 않고 외부 요인을 참조하는 답변
- **가정 기반 응답**: 명시적으로 명시되지 않은 지식을 가정하는 답변

## Step 10: 필수 후속 질문
9단계의 분석에서 애매한 답변이 드러나면 반드시:
- 즉시 `AskUserQuestion` 도구를 사용하여 명확화 질문
- 모든 애매함이 완전히 해결될 때까지 승인으로 진행하지 않음
- **중요**: 철저하게 - `AskUserQuestion`을 사용하여 불명확한 모든 응답에 대해 후속 질문
- 필요한 후속 질문의 예:
  - "You mentioned 'mix of A and B' - what specific criteria should determine when to use A vs B?"
  - "You said 'somewhere between A and B' - can you define the exact middle ground approach?"
  - "You indicated 'not sure' - what additional information would help you decide?"
  - "You mentioned 'depends on complexity' - how do you define complexity levels and thresholds?"
  - "You chose 'hybrid approach' - what are the specific rules for when to use each method?"
  - "You said 'probably X' - what factors would make it definitely X vs definitely not X?"
  - "You referenced 'standard practice' - can you define what that standard practice is?"

## Step 11: 구현 세부 사항 피하기
- 스토리 생성 방법론에 초점, 우선순위 지정이나 개발 작업 아님
- 이 단계에서 기술적 생성에 대해 논의하지 않음
- 개발 타임라인이나 스프린트 계획 작성 피함
- 스토리 구조 및 형식 결정에 초점 유지

## Step 12: 승인 프롬프트 기록
- 승인을 요청하기 전에 타임스탬프와 함께 프롬프트를 `aidlc-docs/audit.md`에 기록
- 완전한 승인 프롬프트 텍스트 포함
- ISO 8601 타임스탬프 형식 사용

## Step 13: 계획의 명시적 승인 대기
- 사용자가 스토리 접근법을 명시적으로 승인할 때까지 진행하지 않음
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 계획을 업데이트하고 승인 프로세스 반복

## Step 14: 승인 응답 기록
- 타임스탬프와 함께 사용자의 승인 응답을 `aidlc-docs/audit.md`에 기록
- 정확한 사용자 응답 텍스트 포함
- 승인 상태를 명확하게 표시

---

# PART 2: GENERATION

## Step 15: 스토리 생성 계획 로드
- [ ] `aidlc-docs/inception/plans/story-generation-plan.md`에서 완전한 스토리 계획 읽기
- [ ] 다음 완료되지 않은 단계 식별 (첫 번째 [ ] 체크박스)
- [ ] 해당 단계에 대한 컨텍스트 및 요구사항 로드

## Step 16: 현재 단계 실행
- [ ] 현재 단계가 설명하는 것을 정확히 수행
- [ ] 계획에 지정된 대로 스토리 아티팩트 생성
- [ ] Planning에서 승인된 방법론 및 형식 따르기
- [ ] 계획에 지정된 스토리 분해 접근법 사용

## Step 17: 진행 상황 업데이트
- [ ] 스토리 생성 계획에서 완료된 단계를 [x]로 표시
- [ ] `aidlc-docs/aidlc-state.md` 현재 상태 업데이트
- [ ] 생성된 모든 아티팩트 저장

## Step 18: 생성 계속 또는 완료
- [ ] 더 많은 단계가 남아있으면 Step 14로 돌아가기
- [ ] 모든 단계가 완료되면 스토리가 다음 단계를 위해 준비되었는지 확인
- [ ] 모든 필수 아티팩트가 생성되었는지 확인

## Step 19: 승인 프롬프트 기록
- 승인을 요청하기 전에 타임스탬프와 함께 프롬프트를 `aidlc-docs/audit.md`에 기록
- 완전한 승인 프롬프트 텍스트 포함
- ISO 8601 타임스탬프 형식 사용

## Step 20: 완료 메시지 제시
- 다음 구조로 완료 메시지 제시:
     1. **완료 발표** (필수): 항상 이것으로 시작:

```markdown
# 📚 User Stories Complete
```

     2. **AI 요약** (선택): 생성된 스토리의 구조화된 글머리 기호 요약 제공
        - 형식: "User stories generation has created [설명]:"
        - 생성된 주요 페르소나 나열 (글머리 기호)
        - 생성된 user stories를 카운트 및 조직과 함께 나열
        - 스토리 구조 및 준수 언급 (INVEST 기준, 수락 기준)
        - 워크플로 지침 포함하지 말 것 ("please review", "let me know", "proceed to next phase", "before we proceed")
        - 사실적이고 내용 중심으로 유지
     3. **형식화된 워크플로 메시지** (필수): 항상 이 정확한 형식으로 끝내기:

```markdown
> **📋 <u>검토 필요:</u>**
> user stories 및 페르소나를 확인해 주세요: `aidlc-docs/inception/user-stories/stories.md` 및 `aidlc-docs/inception/user-stories/personas.md`



> **🚀 <u>다음 단계는?</u>**
>
> **선택 가능:**
>
> 🔧 **변경 요청** - 검토에 따라 스토리나 페르소나에 대한 수정 요청
> ✅ **승인 및 계속** - user stories 승인 후 **Workflow Planning** 으로 진행

---
```

## Step 21: 생성된 스토리의 명시적 승인 대기
- 사용자가 생성된 스토리를 명시적으로 승인할 때까지 진행하지 않음
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 스토리를 업데이트하고 승인 프로세스 반복

## Step 22: 승인 응답 기록
- 타임스탬프와 함께 사용자의 승인 응답을 `aidlc-docs/audit.md`에 기록
- 정확한 사용자 응답 텍스트 포함
- 승인 상태를 명확하게 표시

## Step 23: 진행 상황 업데이트
- `aidlc-state.md`에서 User Stories 단계를 완료로 표시
- "Current Status" 섹션 업데이트
- 다음 단계로 전환 준비

---

# CRITICAL RULES

## Planning Phase Rules
- **컨텍스트에 적합한 질문**: 이 특정 컨텍스트와 관련된 질문만 하기
- **필수 답변 분석**: 진행하기 전에 항상 애매함에 대한 답변 분석
- **애매함을 가지고 진행 금지**: 생성 전에 모든 모호한 답변 해결
- **명시적 승인 필요**: 생성 시작 전에 사용자가 계획을 승인해야 함

## Generation Phase Rules
- **하드코딩된 로직 금지**: 스토리 생성 계획에 작성된 것만 실행
- **계획을 정확히 따르기**: 단계 순서에서 벗어나지 말 것
- **체크박스 업데이트**: 각 단계 완료 직후 [x]로 표시
- **승인된 방법론 사용**: Planning의 스토리 접근법 따르기
- **완료 검증**: 진행하기 전에 모든 스토리 아티팩트가 완료되었는지 확인

## 완료 기준
- 모든 계획 질문에 답변되고 애매함 해결됨
- 사용자가 계획을 명시적으로 승인함
- 스토리 생성 계획의 모든 단계가 [x]로 표시됨
- 계획에 따라 모든 스토리 아티팩트 생성됨 (stories.md, personas.md)
- 생성된 스토리를 사용자가 명시적으로 승인함
- 스토리가 검증되고 다음 단계를 위해 준비됨
