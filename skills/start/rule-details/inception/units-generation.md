# Units Generation - Detailed Steps

## 개요
이 단계는 두 가지 통합된 부분을 통해 시스템을 관리 가능한 작업 단위로 분해:
- **Part 1 - Planning**: 질문이 있는 분해 계획 생성, 답변 수집, 애매함 분석, 승인 받기
- **Part 2 - Generation**: 승인된 계획을 실행하여 단위 아티팩트 생성

**정의**: 작업 단위는 개발 목적을 위한 스토리의 논리적 그룹화. 마이크로서비스의 경우 각 단위는 독립적으로 배포 가능한 서비스가 됨. 모놀리스의 경우 단일 단위는 논리적 모듈이 있는 전체 애플리케이션을 나타냄.

**용어**: 독립적으로 배포 가능한 컴포넌트에는 "Service", 서비스 내 논리적 그룹화에는 "Module", 계획 컨텍스트에는 "Unit of Work" 사용.

## 전제 조건
- Context Assessment가 완료되어야 함
- Requirements Assessment 권장 (기능적 범위 제공)
- Story Development 권장 (스토리가 단위에 매핑됨)
- Application Design 단계 필수 (컴포넌트, 메서드 및 서비스 결정)
- 실행 계획이 Design 단계를 실행하도록 표시해야 함

---

# PART 1: PLANNING

## Step 1: 작업 단위 계획 생성
- 시스템을 작업 단위로 분해하기 위한 체크박스 []가 있는 계획 생성
- 시스템을 관리 가능한 개발 단위로 분해하는 데 초점
- 각 단계와 하위 단계는 체크박스 []를 가져야 함

## Step 2: 계획에 필수 단위 아티팩트 포함
**항상** 단위 계획에 다음 필수 아티팩트를 포함:
- [ ] 단위 정의 및 책임이 있는 `aidlc-docs/inception/application-design/unit-of-work.md` 생성
- [ ] 의존성 매트릭스가 있는 `aidlc-docs/inception/application-design/unit-of-work-dependency.md` 생성
- [ ] 스토리를 단위에 매핑하는 `aidlc-docs/inception/application-design/unit-of-work-story-map.md` 생성
- [ ] **Greenfield만**: `unit-of-work.md`에 코드 조직 전략 문서화 (구조 패턴은 code-generation.md 참조)
- [ ] 단위 경계 및 의존성 검증
- [ ] 모든 스토리가 단위에 할당되었는지 확인

## Step 3: 컨텍스트에 적합한 질문 생성
**지시**: 요구사항, 스토리 및 애플리케이션 설계를 분석하여 이 특정 분해 문제와 관련된 질문만 생성. 아래 카테고리를 영감으로 사용하되, 필수 체크리스트가 아님. 적용되지 않으면 전체 카테고리를 건너뛰기.

- [Answer]: 태그 형식을 사용하여 질문 포함
- 이 컨텍스트에 특정한 애매함 및 누락된 정보에 초점
- 의사 결정에 사용자 입력이 필요한 곳에만 질문 생성

**예시 질문 카테고리** (필요에 따라 조정):
- **Story Grouping** - 여러 스토리가 존재하고 그룹화 전략이 불명확한 경우에만
- **Dependencies** - 여러 단위가 있을 가능성이 있고 통합 접근법이 애매한 경우에만
- **Team Alignment** - 팀 구조 또는 소유권이 불명확한 경우에만
- **Technical Considerations** - 확장성/배포 요구사항이 단위 간에 다른 경우에만
- **Business Domain** - 도메인 경계 또는 bounded contexts가 불명확한 경우에만
- **Code Organization (Greenfield 다중 단위만)** - 배포 모델 및 디렉토리 구조 선호도에 대해 질문

## Step 4: UOW 계획 저장
- `aidlc-docs/inception/plans/unit-of-work-plan.md`로 저장
- 사용자 입력을 위한 모든 [Answer]: 태그 포함
- 계획이 시스템 분해의 모든 측면을 다루는지 확인

## Step 5: 사용자 입력 요청
- 사용자에게 계획 문서에서 직접 [Answer]: 태그를 채우도록 요청
- 분해 결정의 중요성 강조
- [Answer]: 태그 완료에 대한 명확한 지침 제공

## Step 6: 답변 수집
- 사용자가 문서의 [Answer]: 태그를 사용하여 모든 질문에 답변을 제공할 때까지 대기
- 모든 [Answer]: 태그가 완료될 때까지 진행하지 않음
- [Answer]: 태그가 비어 있지 않은지 문서 검토

## Step 7: 답변 분석 (필수)
진행하기 전에 다음에 대해 모든 사용자 답변을 신중하게 검토해야 함:
- **모호하거나 애매한 응답**: "mix of", "somewhere between", "not sure", "depends"
- **정의되지 않은 기준이나 용어**: 명확한 정의 없이 개념에 대한 참조
- **모순되는 답변**: 서로 충돌하는 응답
- **누락된 생성 세부 사항**: 구체적인 지침이 부족한 답변
- **옵션을 결합하는 답변**: 명확한 결정 규칙 없이 다양한 접근법을 병합하는 응답

## Step 8: 필수 후속 질문
7단계의 분석에서 애매한 답변이 드러나면 반드시:
- [Answer]: 태그를 사용하여 계획 문서에 구체적인 후속 질문 추가
- 모든 애매함이 해결될 때까지 승인으로 진행하지 않음
- 필요한 후속 질문의 예:
  - "You mentioned 'mix of A and B' - what specific criteria should determine when to use A vs B?"
  - "You said 'somewhere between A and B' - can you define the exact middle ground approach?"
  - "You indicated 'not sure' - what additional information would help you decide?"
  - "You mentioned 'depends on complexity' - how do you define complexity levels?"

## Step 9: 승인 요청
- 질문: "**Unit of work plan complete. Review the plan in aidlc-docs/inception/plans/unit-of-work-plan.md. Ready to proceed to generation?**"
- 사용자가 확인할 때까지 진행하지 않음

## Step 10: 승인 기록
- 타임스탬프와 함께 프롬프트 및 응답을 audit.md에 기록
- ISO 8601 타임스탬프 형식 사용
- 완전한 승인 프롬프트 텍스트 포함

## Step 11: 진행 상황 업데이트
- aidlc-state.md에서 Units Planning을 완료로 표시
- "Current Status" 섹션 업데이트
- Units Generation으로 전환 준비

---

# PART 2: GENERATION

## Step 12: 작업 단위 계획 로드
- [ ] `aidlc-docs/inception/plans/unit-of-work-plan.md`에서 완전한 계획 읽기
- [ ] 다음 완료되지 않은 단계 식별 (첫 번째 [ ] 체크박스)
- [ ] 해당 단계에 대한 컨텍스트 및 요구사항 로드

## Step 13: 현재 단계 실행
- [ ] 현재 단계가 설명하는 것을 정확히 수행
- [ ] 계획에 지정된 대로 단위 아티팩트 생성
- [ ] Planning에서 승인된 분해 접근법 따르기
- [ ] 계획에 지정된 기준 및 경계 사용

## Step 14: 진행 상황 업데이트
- [ ] 작업 단위 계획에서 완료된 단계를 [x]로 표시
- [ ] `aidlc-docs/aidlc-state.md` 현재 상태 업데이트
- [ ] 생성된 모든 아티팩트 저장

## Step 15: 계속 또는 완료
- [ ] 더 많은 단계가 남아있으면 Step 12로 돌아가기
- [ ] 모든 단계가 완료되면 단위가 설계 단계를 위해 준비되었는지 확인
- [ ] Units Generation 단계를 완료로 표시

## Step 16: 완료 메시지 제시

```markdown
# 🔧 Units Generation Complete

[생성된 단위 및 분해에 대한 AI 생성 요약을 글머리 기호로]

> **📋 <u>검토 필요:</u>**
> units generation 아티팩트를 확인해 주세요: `aidlc-docs/inception/application-design/`

> **🚀 <u>다음 단계는?</u>**
>
> **선택 가능:**
>
> 🔧 **변경 요청** - 필요시 units generation에 대한 수정 요청
> ✅ **승인 및 계속** - 단위 승인 후 **CONSTRUCTION PHASE** 로 진행
```

## Step 17: 명시적 승인 대기
- 사용자가 units generation을 명시적으로 승인할 때까지 진행하지 않음
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 단위를 업데이트하고 승인 프로세스 반복

## Step 18: 승인 응답 기록
- 타임스탬프와 함께 사용자의 승인 응답을 `aidlc-docs/audit.md`에 기록
- 정확한 사용자 응답 텍스트 포함
- 승인 상태를 명확하게 표시

## Step 19: 진행 상황 업데이트
- `aidlc-docs/aidlc-state.md`에서 Units Generation 단계를 완료로 표시
- "Current Status" 섹션 업데이트
- CONSTRUCTION PHASE로 전환 준비

---

## Critical Rules

### Planning Phase Rules
- 컨텍스트와 관련된 질문만 생성
- 모든 질문에 [Answer]: 태그 형식 사용
- 진행하기 전에 애매함에 대한 모든 답변 분석
- 후속 질문으로 모든 애매함 해결
- 생성 전에 명시적인 사용자 승인 받기

### Generation Phase Rules
- **하드코딩된 로직 금지**: 작업 단위 계획에 작성된 것만 실행
- **계획을 정확히 따르기**: 단계 순서에서 벗어나지 말 것
- **체크박스 업데이트**: 각 단계 완료 직후 [x]로 표시
- **승인된 접근법 사용**: Planning의 분해 방법론 따르기
- **완료 검증**: 진행하기 전에 모든 단위 아티팩트가 완료되었는지 확인

## 완료 기준
- 모든 계획 질문에 답변되고 애매함 해결됨
- 계획에 대해 사용자 승인 받음
- 작업 단위 계획의 모든 단계가 [x]로 표시됨
- 계획에 따라 모든 단위 아티팩트 생성됨:
  - 단위 정의가 있는 `unit-of-work.md`
  - 의존성 매트릭스가 있는 `unit-of-work-dependency.md`
  - 스토리 매핑이 있는 `unit-of-work-story-map.md`
- 단위가 검증되고 단위별 설계 단계를 위해 준비됨
