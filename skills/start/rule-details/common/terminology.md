# AI-DLC 용어 용어집

## 핵심 용어

### Phase vs Stage

**Phase**: AI-DLC의 세 가지 고수준 생명 주기 단계 중 하나
- 🔵 **INCEPTION PHASE** - 계획 & 아키텍처 (무엇과 왜)
- 🟢 **CONSTRUCTION PHASE** - 설계, 구현 & 테스트 (어떻게)
- 🟡 **OPERATIONS PHASE** - 배포 & 모니터링 (향후 확장)

**Stage**: 단계 내의 개별 workflow 활동
- 예: Context Assessment stage, Requirements Assessment stage, Code Planning stage
- 각 단계는 특정 전제 조건, 단계 및 출력을 가짐
- 단계는 항상 실행 또는 조건부일 수 있음

**사용 예시**:
- ✅ "CONSTRUCTION phase에는 7개의 단계가 포함됩니다"
- ✅ "Code Planning stage는 항상 실행됩니다"
- ✅ "우리는 INCEPTION phase에 있으며 Requirements Assessment stage를 실행 중입니다"
- ❌ "Requirements Assessment phase" ("stage"여야 함)
- ❌ "CONSTRUCTION stage" ("phase"여야 함)

## 3단계 생명 주기

### INCEPTION PHASE
**목적**: 계획 및 아키텍처 결정
**초점**: 무엇을 구축할지와 왜 구축할지 결정
**위치**: `inception/` 디렉토리

**단계**:
- Workspace Detection (항상)
- Reverse Engineering (조건부 - Brownfield만)
- Requirements Analysis (항상 - 적응형 깊이)
- User Stories (조건부)
- Workflow Planning (항상)
- Application Design (조건부)
- Design - Units Planning/Generation (조건부)

**출력**: 요구사항, user stories, 아키텍처 결정, 단위 정의

### CONSTRUCTION PHASE
**목적**: 상세 설계 및 구현
**초점**: 어떻게 구축할지 결정
**위치**: `construction/` 디렉토리

**단계**:
- Functional Design (조건부, 단위별)
- NFR Requirements (조건부, 단위별)
- NFR Design (조건부, 단위별)
- Infrastructure Design (조건부, 단위별)
- Code Planning (항상)
- Code Generation (항상)
- Build and Test (항상)

**출력**: 설계 아티팩트, NFR 구현, 코드, 테스트

### OPERATIONS PHASE
**목적**: 배포 및 운영 준비
**초점**: 어떻게 배포하고 실행할지
**위치**: `operations/` 디렉토리

**단계**:
- Operations (자리 표시자)

**출력**: 빌드 지침, 배포 가이드, 모니터링 설정, 검증 절차

---

## Workflow 단계

### 항상 실행 단계
- **Workspace Detection**: workspace 상태 및 프로젝트 유형의 초기 분석
- **Requirements Analysis**: 요구사항 수집 (깊이는 복잡성에 따라 다름)
- **Workflow Planning**: 실행할 단계에 대한 실행 계획 생성
- **Code Planning**: 코드 생성을 위한 상세한 구현 계획 생성
- **Code Generation**: 계획 및 이전 아티팩트를 기반으로 실제 코드 생성
- **Build and Test**: 모든 단위 빌드 및 포괄적 테스트 실행

### 조건부 단계
- **Reverse Engineering**: 기존 코드베이스 분석 (Brownfield 프로젝트만)
- **User Stories**: user stories 및 personas 생성 (Story Planning 및 Story Generation 포함)
- **Application Design**: application 컴포넌트, 메서드, 비즈니스 규칙 및 서비스 설계
- **Design**: 시스템 컴포넌트 설계 (Units Planning, Units Generation, 단위별 설계 포함)
- **Functional Design**: 기술에 구애받지 않는 비즈니스 로직 설계 (단위별)
- **NFR Requirements**: NFR 결정 및 기술 스택 선택 (단위별)
- **NFR Design**: NFR 패턴 및 논리 컴포넌트 통합 (단위별)
- **Infrastructure Design**: 실제 인프라 서비스에 매핑 (단위별)

## Application Design 용어

- **Component**: 특정 책임을 가진 기능 단위
- **Method**: 정의된 비즈니스 규칙을 가진 컴포넌트 내의 함수 또는 작업
- **Business Rule**: 메서드 동작 및 검증을 관리하는 로직
- **Service**: 컴포넌트 간 비즈니스 로직을 조정하는 조율 레이어
- **Component Dependency**: 컴포넌트 간 관계 및 통신 패턴

## 아키텍처 용어 (인프라)

### Unit of Work
개발 목적을 위한 user stories의 논리적 그룹. 계획 및 분해 중에 사용되는 용어.

**사용**: "시스템을 작업 단위로 분해해야 합니다"

### Service
마이크로서비스 아키텍처에서 독립적으로 배포 가능한 컴포넌트. 각 서비스는 별도의 작업 단위입니다.

**사용**: "Payment Service는 모든 결제 처리를 처리합니다"

### Module
단일 서비스 또는 모놀리스 내의 기능의 논리적 그룹. 모듈은 독립적으로 배포할 수 없습니다.

**사용**: "User Service 내의 인증 모듈"

### Component
서비스 또는 모듈 내의 재사용 가능한 빌딩 블록. 컴포넌트는 특정 기능을 제공하는 클래스, 함수 또는 패키지입니다.

**사용**: "EmailValidator 컴포넌트는 이메일 주소를 검증합니다"

## 용어 지침

### 각 용어를 사용할 때

**Unit of Work**:
- Units Planning 및 Units Generation 단계 중
- 시스템 분해를 논의할 때
- 계획 문서 및 논의에서
- 예: "이것을 작업 단위로 어떻게 분해해야 합니까?"

**Service**:
- 독립적으로 배포 가능한 컴포넌트를 참조할 때
- 마이크로서비스 아키텍처 context에서
- 배포 및 인프라 논의에서
- 예: "Order Service는 ECS에 배포될 것입니다"

**Module**:
- 서비스 내의 논리적 그룹을 참조할 때
- 모놀리스 아키텍처 context에서
- 내부 조직을 논의할 때
- 예: "reporting 모듈은 모든 보고서를 생성합니다"

**Component**:
- 특정 클래스, 함수 또는 패키지를 참조할 때
- 설계 및 구현 논의에서
- 재사용 가능한 빌딩 블록을 논의할 때
- 예: "DatabaseConnection 컴포넌트는 연결을 관리합니다"

## 단계 용어

### Planning vs Generation
- **Planning**: 실행을 위한 질문 및 체크박스가 있는 계획 생성
- **Generation**: 계획을 실행하여 아티팩트 생성

예시:
- Story Planning → Story Generation
- Units Planning → Units Generation
- Unit Design Planning → Unit Design Generation
- NFR Planning → NFR Generation
- Code Planning → Code Generation

### 깊이 수준
- **최소**: 간단한 변경을 위한 빠른 집중 실행
- **표준**: 일반 프로젝트를 위한 표준 아티팩트가 있는 일반 깊이
- **포괄적**: 복잡한/고위험 프로젝트를 위한 모든 아티팩트가 있는 전체 깊이

## 아티팩트 유형

### Plans
실행을 안내하는 체크박스 및 질문이 있는 문서.
- `aidlc-docs/plans/`에 위치
- 예: `story-generation-plan.md`, `unit-of-work-plan.md`

### Artifacts
계획 실행으로 생성된 출력.
- 다양한 `aidlc-docs/` 하위 디렉토리에 위치
- 예: `requirements.md`, `stories.md`, `design.md`

### State Files
workflow 진행 상황 및 상태를 추적하는 파일.
- `aidlc-state.md`: 전체 workflow 상태
- `audit.md`: 모든 상호작용의 완전한 감사 추적

## 일반 약어

- **AI-DLC**: AI-Driven Development Life Cycle
- **NFR**: Non-Functional Requirements
- **UOW**: Unit of Work
- **API**: Application Programming Interface
- **CDK**: Cloud Development Kit (AWS)
