# Functional Design

## 목적
**유닛별 상세 비즈니스 로직 설계**

Functional Design은 다음에 초점을 맞춥니다:
- 유닛의 상세한 비즈니스 로직 및 알고리즘
- 엔티티 및 관계를 포함한 도메인 모델
- 상세한 비즈니스 규칙, 검증 로직 및 제약 조건
- 기술 독립적 설계(인프라 관심사 제외)

**참고**: 이는 Application Design(INCEPTION 단계)의 상위 수준 컴포넌트 설계를 기반으로 합니다

## 사전 요구사항
- Units Generation이 완료되어야 함
- 작업 단위 아티팩트가 사용 가능해야 함
- Application Design 권장(상위 수준 컴포넌트 구조 제공)
- 실행 계획이 Functional Design 단계를 실행해야 함을 나타내야 함

## 개요
유닛의 상세한 비즈니스 로직을 설계하며, 기술 독립적이고 순수하게 비즈니스 기능에 초점을 맞춥니다.

## 실행 단계

### Step 1: 유닛 컨텍스트 분석
- `aidlc-docs/inception/application-design/unit-of-work.md`에서 유닛 정의 읽기
- `aidlc-docs/inception/application-design/unit-of-work-story-map.md`에서 할당된 스토리 읽기
- 유닛 책임 및 경계 이해

### Step 2: Functional Design 계획 생성
- 체크박스 []가 포함된 functional design 계획 생성
- 비즈니스 로직, 도메인 모델, 비즈니스 규칙에 초점
- 각 단계는 체크박스 []가 있어야 함

### Step 3: 컨텍스트에 적합한 질문 생성
**지침**: 유닛 정의 및 functional design 아티팩트를 철저히 분석하여 functional design을 개선할 수 있는 모든 영역을 식별합니다. 포괄적인 이해를 보장하기 위해 적극적으로 질문하세요.

**중요**: 애매함이나 누락된 세부 사항이 functional design 품질에 영향을 줄 수 있는 경우 기본적으로 질문하세요. 잘못된 가정을 하는 것보다 너무 많은 질문을 하는 것이 좋습니다.

- [Answer]: 태그 형식을 사용하여 질문 삽입
- 애매함, 누락된 정보 또는 명확화가 필요한 영역에 초점
- 사용자 입력이 functional design 결정을 개선할 수 있는 모든 곳에서 질문 생성
- **의심스러울 때는 질문하기** - 과신은 나쁜 설계로 이어짐

**고려해야 할 질문 카테고리** (모든 카테고리 평가):
- **비즈니스 로직 모델링** - 핵심 엔티티, 워크플로우, 데이터 변환 및 비즈니스 프로세스에 대해 질문
- **도메인 모델** - 도메인 개념, 엔티티 관계, 데이터 구조 및 비즈니스 객체에 대해 질문
- **비즈니스 규칙** - 의사 결정 규칙, 검증 로직, 제약 조건 및 비즈니스 정책에 대해 질문
- **데이터 흐름** - 데이터 입력, 출력, 변환 및 지속성 요구사항에 대해 질문
- **통합 지점** - 외부 시스템 상호작용, API 및 데이터 교환에 대해 질문
- **오류 처리** - 오류 시나리오, 검증 실패 및 예외 처리에 대해 질문
- **비즈니스 시나리오** - 엣지 케이스, 대체 플로우 및 복잡한 비즈니스 상황에 대해 질문

### Step 4: 계획 저장
- `aidlc-docs/construction/plans/{unit-name}-functional-design-plan.md`로 저장
- 사용자 입력을 위한 모든 [Answer]: 태그 포함

### Step 5: 답변 수집 및 분석
- 사용자가 모든 [Answer]: 태그를 완료할 때까지 대기
- **필수**: 모호하거나 애매한 답변에 대해 모든 응답을 신중하게 검토
- **중요**: 불명확한 응답에 대한 후속 질문 추가 - 애매함이 있는 상태로 진행하지 말 것
- "depends", "maybe", "not sure", "mix of", "somewhere between"과 같은 응답 찾기
- 애매함이 감지되면 명확화 질문 파일 생성
- **모든 애매함이 해결될 때까지 진행하지 말 것**

### Step 6: Functional Design 아티팩트 생성
- `aidlc-docs/construction/{unit-name}/functional-design/business-logic-model.md` 생성
- `aidlc-docs/construction/{unit-name}/functional-design/business-rules.md` 생성
- `aidlc-docs/construction/{unit-name}/functional-design/domain-entities.md` 생성

### Step 7: 완료 메시지 제시
- 다음 구조로 완료 메시지 제시:
     1. **완료 공지** (필수): 항상 다음으로 시작:

```markdown
# 🔧 Functional Design Complete - [unit-name]
```

     2. **AI 요약** (선택): functional design의 구조화된 글머리 기호 요약 제공
        - 형식: "Functional design has created [description]:"
        - 주요 비즈니스 로직 모델 및 엔티티 나열(글머리 기호)
        - 정의된 비즈니스 규칙 및 검증 로직 나열
        - 도메인 모델 구조 및 관계 언급
        - 워크플로우 지침 포함하지 말 것("please review", "let me know", "proceed to next phase", "before we proceed")
        - 사실적이고 내용 중심으로 유지
     3. **형식화된 워크플로우 메시지** (필수): 항상 이 정확한 형식으로 종료:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**
> Please examine the functional design artifacts at: `aidlc-docs/construction/[unit-name]/functional-design/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the functional design based on your review
> ✅ **Continue to Next Stage** - Approve functional design and proceed to **[next-stage-name]**

---
```

### Step 8: 명시적 승인 대기
- 사용자가 functional design을 명시적으로 승인할 때까지 진행하지 말 것
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 설계를 업데이트하고 승인 프로세스 반복

### Step 9: 승인 기록 및 진행 상황 업데이트
- 타임스탬프와 함께 audit.md에 승인 로그 기록
- 타임스탬프와 함께 사용자의 승인 응답 기록
- aidlc-state.md에서 Functional Design 단계를 완료로 표시
