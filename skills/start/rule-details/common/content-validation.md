# Content Validation Rules

## 필수: 파일 생성 전 콘텐츠 검증

**중요**: 파싱 오류를 방지하기 위해 생성된 모든 콘텐츠는 파일에 쓰기 전에 검증되어야 합니다.

## ASCII Diagram 표준

**중요**: ASCII 다이어그램이 포함된 파일을 생성하기 전에:

1. **로드** `common/ascii-diagram-standards.md`
2. **검증** 각 다이어그램:
   - 줄당 문자 수 계산 (모든 줄은 동일한 너비여야 함)
   - 오직 `+` `-` `|` `^` `v` `<` `>` 및 공백만 사용
   - Unicode 박스 그리기 문자 사용 금지
   - 공백만 사용 (탭 사용 금지)
3. **테스트** 박스 모서리가 수직으로 정렬되는지 확인하여 정렬 검증

**패턴 및 검증 체크리스트는 `common/ascii-diagram-standards.md`를 참조하세요.**

## Mermaid 다이어그램 검증

### 필수 검증 단계
1. **구문 확인**: 파일 생성 전에 Mermaid 구문 검증
2. **문자 이스케이핑**: 특수 문자가 올바르게 이스케이프되었는지 확인
3. **대체 콘텐츠**: Mermaid 검증 실패 시 텍스트 대안 제공

### Mermaid 검증 규칙
```markdown
## Mermaid 다이어그램이 포함된 파일을 생성하기 전에:

1. 노드 ID의 잘못된 문자 확인 (영숫자 + 밑줄만 사용)
2. 레이블의 특수 문자 이스케이프: " → \" 및 ' → \'
3. 플로우차트 구문 검증: 노드 연결이 유효해야 함
4. 간단한 검증으로 다이어그램 파싱 테스트

## 대체: Mermaid 검증이 실패하면 텍스트 기반 워크플로우 표현 사용
```

### 구현 패턴
```markdown
## Workflow Visualization

### Mermaid Diagram (if syntax valid)
```mermaid
[validated diagram content]
```

### Text Alternative (always include)
```
Phase 1: INCEPTION
- Stage 1: Workspace Detection (COMPLETED)
- Stage 2: Requirements Analysis (COMPLETED)
[continue with text representation]
```

## 일반 콘텐츠 검증

### 생성 전 검증 체크리스트
- [ ] 임베디드 코드 블록 검증 (Mermaid, JSON, YAML)
- [ ] 특수 문자 이스케이핑 확인
- [ ] markdown 구문 정확성 검증
- [ ] 콘텐츠 파싱 호환성 테스트
- [ ] 복잡한 요소에 대한 대체 콘텐츠 포함

### 오류 예방 규칙
1. **파일을 작성하는 tools/commands를 사용하기 전에 항상 검증**: 검증되지 않은 콘텐츠를 절대 작성하지 마세요
2. **특수 문자 이스케이프**: 특히 다이어그램과 코드 블록에서
3. **대안 제공**: 시각적 콘텐츠의 텍스트 버전 포함
4. **구문 테스트**: 복잡한 콘텐츠 구조 검증

## 검증 실패 처리

### 검증이 실패할 때
1. **오류 로그**: 검증 실패 내용 기록
2. **대체 콘텐츠 사용**: 텍스트 기반 대안으로 전환
3. **워크플로우 계속**: 콘텐츠 검증 실패로 차단하지 마세요
4. **사용자에게 알림**: 파싱 제약으로 인해 단순화된 콘텐츠가 사용되었음을 언급
