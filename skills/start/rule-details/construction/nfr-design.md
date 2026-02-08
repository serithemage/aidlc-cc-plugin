# NFR Design

## 사전 요구사항
- 유닛에 대한 NFR Requirements가 완료되어야 함
- NFR requirements 아티팩트가 사용 가능해야 함
- 실행 계획이 NFR Design 단계를 실행해야 함을 나타내야 함

## 개요
패턴과 논리적 컴포넌트를 사용하여 NFR 요구사항을 유닛 설계에 통합합니다.

## 실행 단계

### Step 1: NFR Requirements 분석
- `aidlc-docs/construction/{unit-name}/nfr-requirements/`에서 NFR requirements 읽기
- 확장성, 성능, 가용성, 보안 요구사항 이해

### Step 2: NFR Design 계획 생성
- NFR 설계를 위한 체크박스 []가 포함된 계획 생성
- 설계 패턴 및 논리적 컴포넌트에 초점
- 각 단계는 체크박스 []가 있어야 함

### Step 3: 컨텍스트에 적합한 질문 생성
**지침**: NFR requirements를 분석하여 이 특정 유닛의 NFR 설계와 관련된 질문만 생성합니다. 아래 카테고리를 영감으로 사용하되, 필수 체크리스트로 사용하지 마세요. 해당하지 않는 전체 카테고리는 건너뛰세요.

- [Answer]: 태그 형식을 사용하여 질문 삽입
- 이 유닛에 특정한 애매함 및 누락된 정보에 초점
- 패턴 및 컴포넌트 결정에 사용자 입력이 필요한 경우에만 질문 생성

**예시 질문 카테고리** (필요에 따라 조정):
- **복원력 패턴** - 내결함성 접근 방식에 대한 명확화가 필요한 경우에만
- **확장성 패턴** - 확장 메커니즘이 불분명한 경우에만
- **성능 패턴** - 성능 최적화 전략이 애매한 경우에만
- **보안 패턴** - 보안 구현 접근 방식에 입력이 필요한 경우에만
- **논리적 컴포넌트** - 인프라 컴포넌트(큐, 캐시 등)에 대한 명확화가 필요한 경우에만

### Step 4: 계획 저장
- `aidlc-docs/construction/plans/{unit-name}-nfr-design-plan.md`로 저장
- 사용자 입력을 위한 모든 [Answer]: 태그 포함

### Step 5: 답변 수집 및 분석
- 사용자가 모든 [Answer]: 태그를 완료할 때까지 대기
- 모호하거나 애매한 응답 검토
- 필요한 경우 후속 질문 추가

### Step 6: NFR Design 아티팩트 생성
- `aidlc-docs/construction/{unit-name}/nfr-design/nfr-design-patterns.md` 생성
- `aidlc-docs/construction/{unit-name}/nfr-design/logical-components.md` 생성

### Step 7: 완료 메시지 제시
- 다음 구조로 완료 메시지 제시:
     1. **완료 공지** (필수): 항상 다음으로 시작:

```markdown
# 🎨 NFR Design Complete - [unit-name]
```

     2. **AI 요약** (선택): NFR design의 구조화된 글머리 기호 요약 제공
        - 형식: "NFR design has incorporated [description]:"
        - 구현된 주요 설계 패턴 나열(글머리 기호)
        - 논리적 컴포넌트 및 인프라 요소 나열
        - 적용된 복원력, 확장성 및 성능 패턴 언급
        - 워크플로우 지침 포함하지 말 것("please review", "let me know", "proceed to next phase", "before we proceed")
        - 사실적이고 내용 중심으로 유지
     3. **형식화된 워크플로우 메시지** (필수): 항상 이 정확한 형식으로 종료:

```markdown
> **📋 <u>**REVIEW REQUIRED:**</u>**
> Please examine the NFR design at: `aidlc-docs/construction/[unit-name]/nfr-design/`



> **🚀 <u>**WHAT'S NEXT?**</u>**
>
> **You may:**
>
> 🔧 **Request Changes** - Ask for modifications to the NFR design based on your review
> ✅ **Continue to Next Stage** - Approve NFR design and proceed to **[next-stage-name]**

---
```

### Step 8: 명시적 승인 대기
- 사용자가 NFR design을 명시적으로 승인할 때까지 진행하지 말 것
- 승인은 명확하고 애매하지 않아야 함
- 사용자가 변경을 요청하면 설계를 업데이트하고 승인 프로세스 반복

### Step 9: 승인 기록 및 진행 상황 업데이트
- 타임스탬프와 함께 audit.md에 승인 로그 기록
- 타임스탬프와 함께 사용자의 승인 응답 기록
- aidlc-state.md에서 NFR Design 단계를 완료로 표시
