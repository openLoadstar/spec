<!--
AI_LOAD_HINT: skip
이 디렉토리는 AI 도구의 컨텍스트 로딩 대상이 아닙니다.
This directory is NOT a context-loading target for AI tools.
-->

# internal/ — 설계 작업 공간 / Design Workspace

이 디렉토리는 **정식 SPEC이 아닙니다.** 의사결정 자료, 검토 드래프트, 브레인스토밍 결과를 보관합니다.

This directory is **not part of the formal SPEC.** It holds decision materials, review drafts, and brainstorming results.

## 로딩 정책 / Loading Policy

- **LOADSTAR 사용자 / Users**: 무시해도 됨 / Safe to ignore
- **AI 도구 / AI tools**: 컨텍스트에 포함하지 말 것 / Do not include in context
- **정식 SPEC / Formal SPEC**: 최상위 `01.*` ~ `09.*` 파일만 / Only top-level `01.*`–`09.*` files

## 보존 이유 / Why Kept in Repo

설계 의사결정의 흔적을 외부 기여자도 참조할 수 있도록 공개합니다. 단, SPEC 본문이 아니므로 도구의 자동 로딩 대상에서는 제외해주세요.

Design decision trails are published so external contributors can reference them. However, since this is not SPEC body, please exclude from automatic tool loading.
