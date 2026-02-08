# Reverse Engineering

**목적**: 기존 코드베이스 분석 및 포괄적인 설계 아티팩트 생성

**실행 시기**: Brownfield 프로젝트가 감지된 경우 (워크스페이스에 기존 코드가 발견됨)

**건너뛰기 조건**: Greenfield 프로젝트 (기존 코드 없음)

**재실행 동작**: Brownfield 프로젝트가 감지되면 아티팩트가 존재하더라도 항상 재실행. 이를 통해 아티팩트가 현재 코드 상태를 반영하도록 보장

## Step 1: 다중 패키지 발견

### 1.1 워크스페이스 스캔
- 모든 패키지 (언급된 것뿐만 아니라)
- 설정 파일을 통한 패키지 관계
- 패키지 유형: Application, CDK/Infrastructure, Models, Clients, Tests

### 1.2 비즈니스 컨텍스트 이해
- 시스템이 전반적으로 구현하는 핵심 비즈니스
- 모든 패키지의 비즈니스 개요
- 시스템에 구현된 비즈니스 트랜잭션 목록

### 1.3 인프라 발견
- CDK 패키지 (CDK dependencies가 있는 package.json)
- Terraform (.tf 파일)
- CloudFormation (.yaml/.json 템플릿)
- 배포 스크립트

### 1.4 빌드 시스템 발견
- 빌드 시스템: Brazil, Maven, Gradle, npm
- 빌드 시스템 선언을 위한 설정 파일
- 패키지 간 빌드 의존성

### 1.5 서비스 아키텍처 발견
- Lambda 함수 (핸들러, 트리거)
- 컨테이너 서비스 (Docker/ECS 설정)
- API 정의 (Smithy 모델, OpenAPI 스펙)
- 데이터 저장소 (DynamoDB, S3, 등)

### 1.6 코드 품질 분석
- 프로그래밍 언어 및 프레임워크
- 테스트 커버리지 지표
- Linting 설정
- CI/CD 파이프라인

## Step 1: 비즈니스 개요 문서 생성

`aidlc-docs/inception/reverse-engineering/business-overview.md` 생성:

```markdown
# Business Overview

## Business Context Diagram
[비즈니스 컨텍스트를 보여주는 Mermaid 다이어그램]

## Business Description
- **Business Description**: [시스템이 수행하는 전반적인 비즈니스 설명]
- **Business Transactions**: [시스템이 구현하는 비즈니스 트랜잭션 목록 및 설명]
- **Business Dictionary**: [시스템이 따르는 비즈니스 사전 용어 및 의미]

## Component Level Business Descriptions
### [패키지/컴포넌트 이름]
- **Purpose**: [비즈니스 관점에서 수행하는 작업]
- **Responsibilities**: [주요 책임]
```

## Step 2: 아키텍처 문서 생성

`aidlc-docs/inception/reverse-engineering/architecture.md` 생성:

```markdown
# System Architecture

## System Overview
[시스템에 대한 고수준 설명]

## Architecture Diagram
[모든 패키지, 서비스, 데이터 저장소, 관계를 보여주는 Mermaid 다이어그램]

## Component Descriptions
### [패키지/컴포넌트 이름]
- **Purpose**: [수행하는 작업]
- **Responsibilities**: [주요 책임]
- **Dependencies**: [의존하는 것]
- **Type**: [Application/Infrastructure/Model/Client/Test]

## Data Flow
[주요 워크플로의 Mermaid 시퀀스 다이어그램]

## Integration Points
- **External APIs**: [목적과 함께 나열]
- **Databases**: [목적과 함께 나열]
- **Third-party Services**: [목적과 함께 나열]

## Infrastructure Components
- **CDK Stacks**: [목적과 함께 나열]
- **Deployment Model**: [설명]
- **Networking**: [VPC, 서브넷, 보안 그룹]
```

## Step 3: 코드 구조 문서 생성

`aidlc-docs/inception/reverse-engineering/code-structure.md` 생성:

```markdown
# Code Structure

## Build System
- **Type**: [Maven/Gradle/npm/Brazil]
- **Configuration**: [주요 빌드 파일 및 설정]

## Key Classes/Modules
[Mermaid 클래스 다이어그램 또는 모듈 계층 구조]

### Existing Files Inventory
[목적과 함께 모든 소스 파일 나열 - Brownfield 프로젝트에서 수정 후보]

**예시 형식**:
- `[path/to/file]` - [목적/책임]

## Design Patterns
### [패턴 이름]
- **Location**: [사용 위치]
- **Purpose**: [사용 이유]
- **Implementation**: [구현 방법]

## Critical Dependencies
### [의존성 이름]
- **Version**: [버전 번호]
- **Usage**: [사용 방법 및 위치]
- **Purpose**: [필요한 이유]
```

## Step 4: API 문서 생성

`aidlc-docs/inception/reverse-engineering/api-documentation.md` 생성:

```markdown
# API Documentation

## REST APIs
### [엔드포인트 이름]
- **Method**: [GET/POST/PUT/DELETE]
- **Path**: [/api/path]
- **Purpose**: [수행하는 작업]
- **Request**: [요청 형식]
- **Response**: [응답 형식]

## Internal APIs
### [인터페이스/클래스 이름]
- **Methods**: [시그니처와 함께 나열]
- **Parameters**: [파라미터 설명]
- **Return Types**: [반환 타입 설명]

## Data Models
### [모델 이름]
- **Fields**: [필드 설명]
- **Relationships**: [관련 모델]
- **Validation**: [검증 규칙]
```

## Step 5: 컴포넌트 인벤토리 생성

`aidlc-docs/inception/reverse-engineering/component-inventory.md` 생성:

```markdown
# Component Inventory

## Application Packages
- [패키지 이름] - [목적]

## Infrastructure Packages
- [패키지 이름] - [CDK/Terraform] - [목적]

## Shared Packages
- [패키지 이름] - [Models/Utilities/Clients] - [목적]

## Test Packages
- [패키지 이름] - [Integration/Load/Unit] - [목적]

## Total Count
- **Total Packages**: [개수]
- **Application**: [개수]
- **Infrastructure**: [개수]
- **Shared**: [개수]
- **Test**: [개수]
```

## Step 6: 기술 스택 문서 생성

`aidlc-docs/inception/reverse-engineering/technology-stack.md` 생성:

```markdown
# Technology Stack

## Programming Languages
- [언어] - [버전] - [사용처]

## Frameworks
- [프레임워크] - [버전] - [목적]

## Infrastructure
- [서비스] - [목적]

## Build Tools
- [도구] - [버전] - [목적]

## Testing Tools
- [도구] - [버전] - [목적]
```

## Step 7: 의존성 문서 생성

`aidlc-docs/inception/reverse-engineering/dependencies.md` 생성:

```markdown
# Dependencies

## Internal Dependencies
[패키지 의존성을 보여주는 Mermaid 다이어그램]

### [패키지 A]가 [패키지 B]에 의존
- **Type**: [Compile/Runtime/Test]
- **Reason**: [의존성이 존재하는 이유]

## External Dependencies
### [의존성 이름]
- **Version**: [버전]
- **Purpose**: [사용 이유]
- **License**: [라이선스 유형]
```

## Step 8: 코드 품질 평가 생성

`aidlc-docs/inception/reverse-engineering/code-quality-assessment.md` 생성:

```markdown
# Code Quality Assessment

## Test Coverage
- **Overall**: [백분율 또는 Good/Fair/Poor/None]
- **Unit Tests**: [상태]
- **Integration Tests**: [상태]

## Code Quality Indicators
- **Linting**: [설정됨/설정 안됨]
- **Code Style**: [일관적/불일치]
- **Documentation**: [Good/Fair/Poor]

## Technical Debt
- [문제 설명 및 위치]

## Patterns and Anti-patterns
- **Good Patterns**: [나열]
- **Anti-patterns**: [위치와 함께 나열]
```

## Step 9: 타임스탬프 파일 생성

`aidlc-docs/inception/reverse-engineering/reverse-engineering-timestamp.md` 생성:

```markdown
# Reverse Engineering Metadata

**Analysis Date**: [ISO timestamp]
**Analyzer**: AI-DLC
**Workspace**: [워크스페이스 경로]
**Total Files Analyzed**: [개수]

## Artifacts Generated
- [x] architecture.md
- [x] code-structure.md
- [x] api-documentation.md
- [x] component-inventory.md
- [x] technology-stack.md
- [x] dependencies.md
- [x] code-quality-assessment.md
```

## Step 10: 상태 추적 업데이트

`aidlc-docs/aidlc-state.md` 업데이트:

```markdown
## Reverse Engineering Status
- [x] Reverse Engineering - [timestamp]에 완료
- **Artifacts Location**: aidlc-docs/inception/reverse-engineering/
```

## Step 11: 사용자에게 완료 메시지 제시

```markdown
# 🔍 Reverse Engineering Complete

[분석에서 나온 주요 발견 사항에 대한 AI 생성 요약을 글머리 기호 형식으로]

> **📋 <u>검토 필요:</u>**
> reverse engineering 아티팩트를 확인해 주세요: `aidlc-docs/inception/reverse-engineering/`

> **🚀 <u>다음 단계는?</u>**
>
> **선택 가능:**
>
> 🔧 **변경 요청** - 필요시 reverse engineering 분석에 대한 수정 요청
> ✅ **승인 및 계속** - 분석 승인 후 **Requirements Analysis** 로 진행
```

## Step 12: 사용자 승인 대기

- **필수**: 사용자가 명시적으로 승인할 때까지 진행하지 않음
- **필수**: 사용자의 응답을 완전한 원본 입력과 함께 audit.md에 기록
