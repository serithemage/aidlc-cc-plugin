# Code Generation - 상세 단계

## 개요
이 단계는 통합된 두 부분을 통해 각 작업 단위의 코드를 생성합니다:
- **Part 1 - 계획**: 명시적 단계가 포함된 상세 코드 생성 계획 생성
- **Part 2 - 생성**: 승인된 계획을 실행하여 코드, 테스트 및 아티팩트 생성

**참고**: Brownfield 프로젝트의 경우, "생성"은 적절한 경우 기존 파일을 수정하는 것을 의미하며, 중복 생성이 아닙니다.

## 사전 요구사항
- 유닛에 대한 Unit Design Generation이 완료되어야 함
- NFR Implementation(실행된 경우)이 유닛에 대해 완료되어야 함
- 모든 유닛 설계 아티팩트가 사용 가능해야 함
- 유닛이 코드 생성 준비가 되어 있어야 함

---

# PART 1: 계획

## Step 1: 유닛 컨텍스트 분석
- [ ] Unit Design Generation에서 유닛 설계 아티팩트 읽기
- [ ] 할당된 스토리를 이해하기 위해 유닛 스토리 맵 읽기
- [ ] 유닛 의존성 및 인터페이스 식별
- [ ] 유닛이 코드 생성 준비가 되었는지 검증

## Step 2: 상세 유닛 코드 생성 계획 생성
- [ ] `aidlc-docs/aidlc-state.md`에서 작업 공간 루트 및 프로젝트 타입 읽기
- [ ] 코드 위치 결정(구조 패턴은 Critical Rules 참조)
- [ ] **Brownfield만 해당**: 수정할 기존 파일을 위해 역공학 code-structure.md 검토
- [ ] 정확한 경로 문서화(aidlc-docs/ 절대 사용 금지)
- [ ] 유닛 생성을 위한 명시적 단계 생성:
  - Project Structure Setup(greenfield만 해당)
  - Business Logic Generation
  - Business Logic Unit Testing
  - Business Logic Summary
  - API Layer Generation
  - API Layer Unit Testing
  - API Layer Summary
  - Repository Layer Generation
  - Repository Layer Unit Testing
  - Repository Layer Summary
  - Database Migration Scripts(데이터 모델이 존재하는 경우)
  - Documentation Generation(API docs, README 업데이트)
  - Deployment Artifacts Generation
- [ ] 각 단계를 순차적으로 번호 매김
- [ ] 스토리 매핑 참조 포함
- [ ] 각 단계에 대한 체크박스 [ ] 추가

## Step 3: 유닛 생성 컨텍스트 포함
- [ ] 이 유닛에 대해 다음 포함:
  - 이 유닛이 구현하는 스토리
  - 다른 유닛/서비스에 대한 의존성
  - 예상 인터페이스 및 계약
  - 이 유닛이 소유한 데이터베이스 엔티티
  - 서비스 경계 및 책임

## Step 4: 유닛 계획 문서 생성
- [ ] 완전한 계획을 `aidlc-docs/construction/plans/{unit-name}-code-generation-plan.md`로 저장
- [ ] 단계 번호 매김 포함(Step 1, Step 2 등)
- [ ] 유닛 컨텍스트 및 의존성 포함
- [ ] 스토리 추적 가능성 포함
- [ ] 계획이 단계별로 실행 가능한지 확인
- [ ] 이 계획이 Code Generation의 단일 진실 공급원임을 강조

## Step 5: 유닛 계획 요약
- [ ] 사용자에게 유닛 코드 생성 계획 요약 제공
- [ ] 유닛 생성 접근 방식 강조
- [ ] 단계 순서 및 스토리 커버리지 설명
- [ ] 총 단계 수 및 예상 범위 주의

## Step 6: 승인 프롬프트 로그
- [ ] 승인을 요청하기 전에 `aidlc-docs/audit.md`에 타임스탬프와 함께 프롬프트 로그 기록
- [ ] 완전한 유닛 코드 생성 계획에 대한 참조 포함
- [ ] ISO 8601 타임스탬프 형식 사용

## Step 7: 명시적 승인 대기
- [ ] 사용자가 유닛 코드 생성 계획을 명시적으로 승인할 때까지 진행하지 말 것
- [ ] 승인은 전체 계획 및 생성 순서를 포함해야 함
- [ ] 사용자가 변경을 요청하면 계획을 업데이트하고 승인 프로세스 반복

## Step 8: 승인 응답 기록
- [ ] `aidlc-docs/audit.md`에 타임스탬프와 함께 사용자의 승인 응답 로그 기록
- [ ] 정확한 사용자 응답 텍스트 포함
- [ ] 승인 상태를 명확하게 표시

## Step 9: 진행 상황 업데이트
- [ ] `aidlc-state.md`에서 Code Planning을 완료로 표시
- [ ] "Current Status" 섹션 업데이트
- [ ] Code Generation으로 전환 준비

---

# PART 2: 생성

## Step 10: 유닛 코드 생성 계획 로드
- [ ] `aidlc-docs/construction/plans/{unit-name}-code-generation-plan.md`에서 완전한 계획 읽기
- [ ] 다음 미완료 단계 식별(첫 번째 [ ] 체크박스)
- [ ] 해당 단계의 컨텍스트 로드(유닛, 의존성, 스토리)

## Step 11: 현재 단계 실행
- [ ] 계획에서 대상 디렉토리 확인(aidlc-docs/ 절대 사용 금지)
- [ ] **Brownfield만 해당**: 대상 파일이 존재하는지 확인
- [ ] 현재 단계가 설명하는 것을 정확히 생성:
  - **파일이 존재하는 경우**: 제자리에서 수정(`ClassName_modified.java`, `ClassName_new.java` 등 생성 금지)
  - **파일이 존재하지 않는 경우**: 새 파일 생성
- [ ] 올바른 위치에 작성:
  - **애플리케이션 코드**: 프로젝트 구조에 따라 작업 공간 루트
  - **문서화**: `aidlc-docs/construction/{unit-name}/code/`(markdown만)
  - **빌드/설정 파일**: 작업 공간 루트
- [ ] 유닛 스토리 요구사항 준수
- [ ] 의존성 및 인터페이스 존중

## Step 12: 진행 상황 업데이트
- [ ] 유닛 코드 생성 계획에서 완료된 단계를 [x]로 표시
- [ ] 관련 유닛 스토리의 생성이 완료되면 [x]로 표시
- [ ] `aidlc-docs/aidlc-state.md` 현재 상태 업데이트
- [ ] **Brownfield만 해당**: 중복 파일이 생성되지 않았는지 확인(예: `ClassName.java`와 함께 `ClassName_modified.java`가 없음)
- [ ] 생성된 모든 아티팩트 저장

## Step 13: 생성 계속 또는 완료
- [ ] 더 많은 단계가 남아 있으면 Step 10으로 돌아가기
- [ ] 모든 단계가 완료되면 완료 메시지 제시로 진행

## Step 14: 완료 메시지 제시
- 다음 구조로 완료 메시지 제시:
     1. **완료 공지** (필수): 항상 다음으로 시작:

```markdown
# 💻 Code Generation Complete - [unit-name]
```

     2. **AI 요약** (선택): 구조화된 글머리 기호 요약 제공
        - **Brownfield**: 수정된 파일 vs 생성된 파일 구분(예: "• Modified: `src/services/user-service.ts`", "• Created: `src/services/auth-service.ts`")
        - **Greenfield**: 경로와 함께 생성된 파일 나열(예: "• Created: `src/services/user-service.ts`")
        - 경로와 함께 테스트, 문서화, 배포 아티팩트 나열
        - 사실적으로 유지, 워크플로우 지침 없음
     3. **형식화된 워크플로우 메시지** (필수): 항상 이 정확한 형식으로 종료:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**
> Please examine the generated code at:
> - **Application Code**: `[actual-workspace-path]`
> - **Documentation**: `aidlc-docs/construction/[unit-name]/code/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the generated code based on your review
> ✅ **Continue to Next Stage** - Approve code generation and proceed to **[next-unit/Build & Test]**

---
```

## Step 15: 명시적 승인 대기
- 사용자가 생성된 코드를 명시적으로 승인할 때까지 진행하지 말 것
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 코드를 업데이트하고 승인 프로세스 반복

## Step 16: 승인 기록 및 진행 상황 업데이트
- 타임스탬프와 함께 audit.md에 승인 로그 기록
- 타임스탬프와 함께 사용자의 승인 응답 기록
- 이 유닛에 대해 aidlc-state.md에서 Code Generation 단계를 완료로 표시

---

## Critical Rules

### 코드 위치 규칙
- **애플리케이션 코드**: 작업 공간 루트만(aidlc-docs/ 절대 사용 금지)
- **문서화**: aidlc-docs/만(markdown 요약)
- **코드 생성 전** aidlc-state.md에서 작업 공간 루트 읽기

**프로젝트 타입별 구조 패턴**:
- **Brownfield**: 기존 구조 사용(예: `src/main/java/`, `lib/`, `pkg/`)
- **Greenfield single unit**: 작업 공간 루트에 `src/`, `tests/`, `config/`
- **Greenfield multi-unit (microservices)**: `{unit-name}/src/`, `{unit-name}/tests/`
- **Greenfield multi-unit (monolith)**: `src/{unit-name}/`, `tests/{unit-name}/`

### Brownfield 파일 수정 규칙
- 생성하기 전에 파일이 존재하는지 확인
- 존재하는 경우: 제자리에서 수정(`ClassName_modified.java`와 같은 복사본 생성 금지)
- 존재하지 않는 경우: 새 파일 생성
- 생성 후 중복 파일이 없는지 확인(Step 12)

### 계획 단계 규칙
- 모든 생성 활동에 대한 명시적이고 번호가 매겨진 단계 생성
- 계획에 스토리 추적 가능성 포함
- 유닛 컨텍스트 및 의존성 문서화
- 생성 전에 명시적 사용자 승인 받기

### 생성 단계 규칙
- **하드코딩된 로직 없음**: 유닛 계획에 작성된 것만 실행
- **계획 정확히 준수**: 단계 순서에서 벗어나지 말 것
- **체크박스 업데이트**: 각 단계 완료 후 즉시 [x]로 표시
- **스토리 추적 가능성**: 기능이 구현되면 유닛 스토리를 [x]로 표시
- **의존성 존중**: 유닛 의존성이 충족된 경우에만 구현

## 완료 기준
- 완전한 유닛 코드 생성 계획이 생성되고 승인됨
- 유닛 코드 생성 계획의 모든 단계가 [x]로 표시됨
- 계획에 따라 모든 유닛 스토리가 구현됨
- 모든 코드 및 테스트가 생성됨(테스트는 Build & Test 단계에서 실행됨)
- 배포 아티팩트가 생성됨
- 빌드 및 검증을 위한 완전한 유닛 준비 완료
