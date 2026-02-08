# Build and Test

**목적**: 모든 유닛을 빌드하고 포괄적인 테스트 전략을 실행합니다

## 사전 요구사항
- 모든 유닛에 대한 Code Generation이 완료되어야 함
- 모든 코드 아티팩트가 생성되어야 함
- 프로젝트가 빌드 및 테스트 준비가 되어 있어야 함

---

## Step 1: 테스트 요구사항 분석

적절한 테스트 전략을 결정하기 위해 프로젝트를 분석합니다:
- **Unit tests**: 코드 생성 중 유닛별로 이미 생성됨
- **Integration tests**: 유닛/서비스 간 상호작용 테스트
- **Performance tests**: 부하, 스트레스 및 확장성 테스트
- **End-to-end tests**: 완전한 사용자 워크플로우
- **Contract tests**: 서비스 간 API 계약 검증
- **Security tests**: 취약성 스캐닝, 침투 테스트

---

## Step 2: 빌드 지침 생성

`aidlc-docs/construction/build-and-test/build-instructions.md` 생성:

```markdown
# Build Instructions

## Prerequisites
- **Build Tool**: [도구 이름 및 버전]
- **Dependencies**: [필요한 모든 의존성 나열]
- **Environment Variables**: [필요한 환경 변수 나열]
- **System Requirements**: [OS, 메모리, 디스크 공간]

## Build Steps

### 1. Install Dependencies
\`\`\`bash
[의존성을 설치하는 명령]
# 예: npm install, mvn dependency:resolve, pip install -r requirements.txt
\`\`\`

### 2. Configure Environment
\`\`\`bash
[환경을 설정하는 명령]
# 예: export variables, configure credentials
\`\`\`

### 3. Build All Units
\`\`\`bash
[모든 유닛을 빌드하는 명령]
# 예: mvn clean install, npm run build, brazil-build
\`\`\`

### 4. Verify Build Success
- **Expected Output**: [성공적인 빌드 출력 설명]
- **Build Artifacts**: [생성된 아티팩트 및 위치 나열]
- **Common Warnings**: [허용 가능한 경고 주의]

## Troubleshooting

### Build Fails with Dependency Errors
- **Cause**: [일반적인 원인]
- **Solution**: [단계별 수정 방법]

### Build Fails with Compilation Errors
- **Cause**: [일반적인 원인]
- **Solution**: [단계별 수정 방법]
```

---

## Step 3: Unit Test 실행 지침 생성

`aidlc-docs/construction/build-and-test/unit-test-instructions.md` 생성:

```markdown
# Unit Test Execution

## Run Unit Tests

### 1. Execute All Unit Tests
\`\`\`bash
[모든 unit tests를 실행하는 명령]
# 예: mvn test, npm test, pytest tests/unit
\`\`\`

### 2. Review Test Results
- **Expected**: [X] tests pass, 0 failures
- **Test Coverage**: [예상 커버리지 백분율]
- **Test Report Location**: [테스트 보고서 경로]

### 3. Fix Failing Tests
테스트가 실패하는 경우:
1. [위치]에서 테스트 출력 검토
2. 실패하는 테스트 케이스 식별
3. 코드 문제 수정
4. 모든 테스트가 통과할 때까지 재실행
```

---

## Step 4: Integration Test 지침 생성

`aidlc-docs/construction/build-and-test/integration-test-instructions.md` 생성:

```markdown
# Integration Test Instructions

## Purpose
유닛/서비스 간 상호작용을 테스트하여 올바르게 함께 작동하는지 확인합니다.

## Test Scenarios

### Scenario 1: [Unit A] → [Unit B] Integration
- **Description**: [무엇을 테스트하는지]
- **Setup**: [필요한 테스트 환경 설정]
- **Test Steps**: [단계별 테스트 실행]
- **Expected Results**: [예상 결과]
- **Cleanup**: [테스트 후 정리 방법]

### Scenario 2: [Unit B] → [Unit C] Integration
[유사한 구조]

## Setup Integration Test Environment

### 1. Start Required Services
\`\`\`bash
[서비스를 시작하는 명령]
# 예: docker-compose up, start test database
\`\`\`

### 2. Configure Service Endpoints
\`\`\`bash
[엔드포인트를 구성하는 명령]
# 예: export API_URL=http://localhost:8080
\`\`\`

## Run Integration Tests

### 1. Execute Integration Test Suite
\`\`\`bash
[integration tests를 실행하는 명령]
# 예: mvn integration-test, npm run test:integration
\`\`\`

### 2. Verify Service Interactions
- **Test Scenarios**: [주요 integration test 시나리오 나열]
- **Expected Results**: [예상 결과 설명]
- **Logs Location**: [로그 확인 위치]

### 3. Cleanup
\`\`\`bash
[테스트 환경을 정리하는 명령]
# 예: docker-compose down, stop test services
\`\`\`
```

---

## Step 5: Performance Test 지침 생성(해당되는 경우)

`aidlc-docs/construction/build-and-test/performance-test-instructions.md` 생성:

```markdown
# Performance Test Instructions

## Purpose
부하 하에서 시스템 성능을 검증하여 요구사항을 충족하는지 확인합니다.

## Performance Requirements
- **Response Time**: [Y]%의 요청에 대해 < [X]ms
- **Throughput**: [X] 요청/초
- **Concurrent Users**: [X] 동시 사용자 지원
- **Error Rate**: < [X]%

## Setup Performance Test Environment

### 1. Prepare Test Environment
\`\`\`bash
[성능 테스트를 설정하는 명령]
# 예: scale services, configure load balancers
\`\`\`

### 2. Configure Test Parameters
- **Test Duration**: [X] 분
- **Ramp-up Time**: [X] 초
- **Virtual Users**: [X] 사용자

## Run Performance Tests

### 1. Execute Load Tests
\`\`\`bash
[load tests를 실행하는 명령]
# 예: jmeter -n -t test.jmx, k6 run script.js
\`\`\`

### 2. Execute Stress Tests
\`\`\`bash
[stress tests를 실행하는 명령]
# 예: gradually increase load until failure
\`\`\`

### 3. Analyze Performance Results
- **Response Time**: [실제 vs 예상]
- **Throughput**: [실제 vs 예상]
- **Error Rate**: [실제 vs 예상]
- **Bottlenecks**: [식별된 병목 현상]
- **Results Location**: [성능 보고서 경로]

## Performance Optimization

성능이 요구사항을 충족하지 않는 경우:
1. 테스트 결과에서 병목 현상 식별
2. 코드/쿼리/설정 최적화
3. 개선 사항을 검증하기 위해 테스트 재실행
```

---

## Step 6: 추가 테스트 지침 생성(필요에 따라)

프로젝트 요구사항에 따라 추가 테스트 지침 파일 생성:

### Contract Tests(마이크로서비스용)
`aidlc-docs/construction/build-and-test/contract-test-instructions.md` 생성:
- 서비스 간 API 계약 검증
- Consumer-driven contract 테스트
- 스키마 검증

### Security Tests
`aidlc-docs/construction/build-and-test/security-test-instructions.md` 생성:
- 취약성 스캐닝
- 의존성 보안 검사
- 인증/권한 부여 테스트
- 입력 검증 테스트

### End-to-End Tests
`aidlc-docs/construction/build-and-test/e2e-test-instructions.md` 생성:
- 완전한 사용자 워크플로우 테스트
- 서비스 간 시나리오
- UI 테스트(해당되는 경우)

---

## Step 7: 테스트 요약 생성

`aidlc-docs/construction/build-and-test/build-and-test-summary.md` 생성:

```markdown
# Build and Test Summary

## Build Status
- **Build Tool**: [도구 이름]
- **Build Status**: [Success/Failed]
- **Build Artifacts**: [아티팩트 나열]
- **Build Time**: [소요 시간]

## Test Execution Summary

### Unit Tests
- **Total Tests**: [X]
- **Passed**: [X]
- **Failed**: [X]
- **Coverage**: [X]%
- **Status**: [Pass/Fail]

### Integration Tests
- **Test Scenarios**: [X]
- **Passed**: [X]
- **Failed**: [X]
- **Status**: [Pass/Fail]

### Performance Tests
- **Response Time**: [실제] (Target: [예상])
- **Throughput**: [실제] (Target: [예상])
- **Error Rate**: [실제] (Target: [예상])
- **Status**: [Pass/Fail]

### Additional Tests
- **Contract Tests**: [Pass/Fail/N/A]
- **Security Tests**: [Pass/Fail/N/A]
- **E2E Tests**: [Pass/Fail/N/A]

## Overall Status
- **Build**: [Success/Failed]
- **All Tests**: [Pass/Fail]
- **Ready for Operations**: [Yes/No]

## Next Steps
[모두 통과한 경우]: 배포 계획을 위한 Operations 단계로 진행 준비 완료
[실패한 경우]: 실패한 테스트를 해결하고 재빌드
```

---

## Step 8: 상태 추적 업데이트

`aidlc-docs/aidlc-state.md` 업데이트:
- Build and Test 단계를 완료로 표시
- 현재 상태 업데이트

---

## Step 9: 사용자에게 결과 제시

포괄적인 메시지 제시:

```
"🔨 Build and Test Complete!

**Build Status**: [Success/Failed]

**Test Results**:
✅ Unit Tests: [X] passed
✅ Integration Tests: [X] scenarios passed
✅ Performance Tests: [Status]
✅ Additional Tests: [Status]

**Generated Files**:
1. ✅ build-instructions.md
2. ✅ unit-test-instructions.md
3. ✅ integration-test-instructions.md
4. ✅ performance-test-instructions.md (해당되는 경우)
5. ✅ [필요에 따른 추가 테스트 파일]
6. ✅ build-and-test-summary.md

aidlc-docs/construction/build-and-test/build-and-test-summary.md에서 요약 검토

**배포 계획을 위한 Operations 단계로 진행할 준비가 되었습니까?**"
```

---

## Step 10: 상호작용 로그

**필수**: `aidlc-docs/audit.md`에 단계 완료를 로그 기록:

```markdown
## Build and Test Stage
**Timestamp**: [ISO timestamp]
**Build Status**: [Success/Failed]
**Test Status**: [Pass/Fail]
**Files Generated**:
- build-instructions.md
- unit-test-instructions.md
- integration-test-instructions.md
- performance-test-instructions.md
- build-and-test-summary.md

---
```
