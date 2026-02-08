# Workspace Detection

**목적**: 워크스페이스 상태 확인 및 기존 AI-DLC 프로젝트 존재 여부 확인

## Step 1: 기존 AI-DLC 프로젝트 확인

`aidlc-docs/aidlc-state.md` 파일 존재 여부 확인:
- **존재하는 경우**: 마지막 단계부터 재개 (이전 단계의 컨텍스트 로드)
- **존재하지 않는 경우**: 새 프로젝트 평가 계속 진행

## Step 2: 워크스페이스에서 기존 코드 스캔

**워크스페이스에 기존 코드가 있는지 판단:**
- 소스 코드 파일 검색 (.java, .py, .js, .ts, .jsx, .tsx, .kt, .kts, .scala, .groovy, .go, .rs, .rb, .php, .c, .h, .cpp, .hpp, .cc, .cs, .fs, 등)
- 빌드 파일 확인 (pom.xml, package.json, build.gradle, 등)
- 프로젝트 구조 지표 확인
- 워크스페이스 루트 디렉토리 식별 (aidlc-docs/가 아님)

**발견 사항 기록:**
```markdown
## Workspace State
- **Existing Code**: [Yes/No]
- **Programming Languages**: [발견된 경우 나열]
- **Build System**: [발견된 경우 Maven/Gradle/npm/등]
- **Project Structure**: [Monolith/Microservices/Library/Empty]
- **Workspace Root**: [절대 경로]
```

## Step 3: 다음 단계 결정

**워크스페이스가 비어있는 경우 (기존 코드 없음)**:
- 플래그 설정: `brownfield = false`
- 다음 단계: Requirements Analysis

**워크스페이스에 기존 코드가 있는 경우**:
- 플래그 설정: `brownfield = true`
- `aidlc-docs/inception/reverse-engineering/`에서 기존 reverse engineering 아티팩트 확인
- **reverse engineering 아티팩트가 존재하는 경우**: 로드하고 Requirements Analysis로 건너뛰기
- **reverse engineering 아티팩트가 없는 경우**: 다음 단계는 Reverse Engineering

## Step 4: 초기 상태 파일 생성

`aidlc-docs/aidlc-state.md` 생성:

```markdown
# AI-DLC State Tracking

## Project Information
- **Project Type**: [Greenfield/Brownfield]
- **Start Date**: [ISO timestamp]
- **Current Stage**: INCEPTION - Workspace Detection

## Workspace State
- **Existing Code**: [Yes/No]
- **Reverse Engineering Needed**: [Yes/No]
- **Workspace Root**: [절대 경로]

## Code Location Rules
- **Application Code**: Workspace root (aidlc-docs/에는 절대 안됨)
- **Documentation**: aidlc-docs/만
- **Structure patterns**: code-generation.md Critical Rules 참조

## Stage Progress
[워크플로 진행에 따라 채워짐]
```

## Step 5: 완료 메시지 제시

**Brownfield 프로젝트의 경우:**
```markdown
# 🔍 Workspace Detection Complete

워크스페이스 분석 결과:
• **Project Type**: Brownfield project
• [워크스페이스 발견 사항에 대한 AI 생성 요약을 글머리 기호 형식으로]
• **Next Step**: **Reverse Engineering** 으로 진행하여 기존 코드베이스 분석...
```

**Greenfield 프로젝트의 경우:**
```markdown
# 🔍 Workspace Detection Complete

워크스페이스 분석 결과:
• **Project Type**: Greenfield project
• **Next Step**: **Requirements Analysis** 로 진행...
```

## Step 6: 자동으로 진행

- **사용자 승인 불필요** - 이것은 정보 제공 목적일 뿐임
- 자동으로 다음 단계로 진행:
  - **Brownfield**: Reverse Engineering (기존 아티팩트가 없는 경우) 또는 Requirements Analysis (아티팩트가 존재하는 경우)
  - **Greenfield**: Requirements Analysis
