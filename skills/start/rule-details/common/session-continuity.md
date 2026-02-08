# 세션 연속성 템플릿

## 환영 Prompt 템플릿
사용자가 기존 AI-DLC 프로젝트에서 작업을 계속하기 위해 돌아올 때 이 prompt를 제시합니다:

```markdown
**다시 오신 것을 환영합니다! 진행 중인 기존 AI-DLC 프로젝트가 있는 것을 확인할 수 있습니다.**

aidlc-state.md를 기반으로 현재 상태는 다음과 같습니다:
- **프로젝트**: [project-name]
- **현재 단계**: [INCEPTION/CONSTRUCTION/OPERATIONS]
- **현재 단계**: [단계 이름]
- **마지막 완료**: [마지막으로 완료된 단계]
- **다음 단계**: [작업할 다음 단계]

**오늘 무엇을 작업하시겠습니까?**

A) 중단한 곳에서 계속 ([다음 단계 설명])
B) 이전 단계 검토 ([사용 가능한 단계 표시])
C) 기타 (설명해 주세요)

선택 사항을 알려주세요.
```

## 필수: 세션 연속성 지침
1. **기존 프로젝트를 감지할 때 항상 aidlc-state.md를 먼저 읽습니다**
2. **사용자 선호도 로드** 질문 스타일 선호도를 복원하기 위해 `aidlc-docs/aidlc-preferences.md`에서
3. **현재 상태 파싱** prompt를 채우기 위해 workflow 파일에서
3. **필수: 이전 단계 아티팩트 로드** - 모든 단계를 재개하기 전에 이전 단계의 모든 관련 아티팩트를 자동으로 읽습니다:
   - **Reverse Engineering**: architecture.md, code-structure.md, api-documentation.md 읽기
   - **Requirements Analysis**: requirements.md, requirement-verification-questions.md 읽기
   - **User Stories**: stories.md, personas.md, story-generation-plan.md 읽기
   - **Application Design**: application-design 아티팩트 읽기 (components.md, component-methods.md, services.md)
   - **Design (Units)**: unit-of-work.md, unit-of-work-dependency.md, unit-of-work-story-map.md 읽기
   - **Per-Unit Design**: functional-design.md, nfr-requirements.md, nfr-design.md, infrastructure-design.md 읽기
   - **Code Stages**: 모든 코드 파일, 계획 및 모든 이전 아티팩트 읽기
4. **단계별 스마트 Context 로딩**:
   - **초기 단계 (Workspace Detection, Reverse Engineering)**: workspace 분석 로드
   - **Requirements/Stories**: reverse engineering + requirements 아티팩트 로드
   - **설계 단계**: requirements + stories + 아키텍처 + 설계 아티팩트 로드
   - **코드 단계**: 모든 아티팩트 + 기존 코드 파일 로드
5. **아키텍처 선택 및 현재 단계에 따라 옵션 조정**
6. **일반적인 설명보다 구체적인 다음 단계 표시**
7. **audit.md에 타임스탬프와 함께 연속성 prompt 로그**
8. **Context 요약**: 아티팩트를 로드한 후 사용자 인식을 위해 로드된 내용에 대한 간략한 요약 제공
9. **질문하기**: 항상 대화에서 직접 명확화 또는 사용자 피드백 질문 (chat 기반). 사용자가 편집할 질문 파일을 만들지 마세요.

## 오류 처리
세션 재개 중에 아티팩트가 누락되거나 손상된 경우 복구 절차에 대한 지침은 [error-handling.md](error-handling.md)를 참조하세요.
