# Company Report Plugin

ChatGPT Work와 Codex에서 회사 보고용 16:9 슬라이드를 만드는 스킬 전용 플러그인입니다. 요구사항 정리, 구조 승인, PNG 시안 승인, 편집 가능한 PPTX 제공을 순서대로 수행합니다.

## 지원 환경

| 환경 | 지원 | 비고 |
| --- | --- | --- |
| ChatGPT 웹 Work 모드 | 지원 | 설치 또는 공유된 플러그인 사용 |
| ChatGPT 데스크톱 Work/Codex | 지원 | 로컬·GitHub 마켓플레이스 설치 가능 |
| Codex CLI | 지원 | `/plugins`에서 설치 |
| 일반 Chat 모드·모바일 | 미지원 | 현재 플러그인 실행 표면이 아님 |

플러그인은 로컬 서버, MCP 서버, 외부 API를 요구하지 않습니다. 레퍼런스, 범용 PowerPoint 템플릿, 나눔바른고딕 OTF Regular/Bold는 플러그인에 포함되며, 사용자 회사 템플릿과 근거 자료는 대화 첨부 파일로 받습니다.

## 주요 동작

- 기본 결과물은 1페이지 요약 1장입니다.
- 필요한 경우에만 백데이터 슬라이드를 제안합니다.
- 구조를 먼저 텍스트로 제시하고 명시적 승인을 받습니다.
- 같은 편집 가능한 원본에서 PNG와 PPTX를 생성합니다.
- PNG 승인 전에는 최종 PPTX를 제공하지 않습니다.
- 웹에서는 PNG와 PPTX를 대화에서 열 수 있는 첨부 파일로 제공합니다.
- 웹 작업 세션에 번들 글꼴을 등록하고 실제 글꼴 이름을 확인한 뒤 렌더링합니다.
- 번들 템플릿은 표지 없이 6개의 범용 조합 레시피 장표로 구성하며, 단일 과제 장표는 개선 요약·일정과 실제 수행 단계·입력·처리·산출을 한 화면에 함께 설명합니다. 실제 회사 로고, 고객 정보, 사내 화면은 포함하지 않습니다.
- 각 템플릿 장표의 객체 이름과 ID를 분리해 웹 미리보기에서 과제 밴드, 화살표, 노드가 다른 장에 섞이지 않도록 구성합니다.
- 보고 상황에 맞는 의미 기반 컴포넌트 조합 레시피를 선택하고, 번들 템플릿을 완성 형태의 시각 기준으로 사용합니다.
- 생성 시 핵심 구문·밑줄·영역 테두리는 빨강, 첨부 참고자료는 초록 `※`, 부가 설명은 작은 회색 문구로 구분합니다. 필요한 도식·flowchart·화면 캡처 자료가 없으면 편집 가능한 사각형 자리만 확보하며, 해당 요소들은 템플릿에 상시 자리표시자로 두지 않습니다.

## 글꼴 동작

웹 호스트에서는 스킬의 `assets/fonts`에 포함된 나눔바른고딕을 현재 작업 세션의 사용자 글꼴 영역에 등록합니다. 영구 시스템 설치는 요구하지 않습니다. 등록이나 확인 기능이 없는 호스트에서는 임의 대체하지 않고 사용자에게 제한을 알립니다.

PPTX 내보내기가 글꼴 파일 자체의 내장을 보장하지 않으므로, 파일을 받은 PC에서도 나눔바른고딕을 설치해야 승인된 PNG와 같은 모양을 유지할 수 있습니다. 글꼴은 SIL Open Font License 1.1에 따라 재배포하며 전문과 고지문을 `assets/fonts/OFL.txt`에 포함합니다.

## ChatGPT 웹에서 사용

ChatGPT 웹 사용자는 Work 모드의 **Plugins**에서 설치된 플러그인을 사용합니다. 로컬 파일 경로를 웹 브라우저에 연결할 필요는 없습니다.

### 워크스페이스 내부 배포

관리자 또는 제작자가 한 번만 다음 절차를 수행합니다.

1. 이 저장소를 GitHub에 게시합니다.
2. ChatGPT 데스크톱 또는 Codex CLI에서 GitHub 마켓플레이스를 등록합니다.

```bash
codex plugin marketplace add OWNER/REPOSITORY --ref main
```

3. ChatGPT 데스크톱의 Work 또는 Codex에서 **Plugins**를 열어 `Company Report`를 설치합니다.
4. 플러그인 상세 화면에서 워크스페이스 구성원이나 그룹에 공유합니다.

웹 사용자는 다음 단계만 수행합니다.

1. ChatGPT 웹에서 Work 모드로 전환합니다.
2. **Plugins → Shared with me**에서 `Company Report`를 설치합니다.
3. 새 Work 대화를 열고 `@`로 플러그인을 선택합니다.

```text
경영진용 1페이지 진행 보고서를 만들어줘.
```

### 공개 Plugins Directory 배포

불특정 ChatGPT 웹 사용자가 검색·설치하게 하려면 OpenAI Platform의 플러그인 제출 포털에서 **Skills only** 유형으로 제출합니다.

- 제출 포털: <https://platform.openai.com/plugins>
- 공식 안내: <https://learn.chatgpt.com/docs/submit-plugins>

공개 제출에는 검증된 개발자·사업자 정보, 로고, 웹사이트, 지원 URL, 개인정보처리방침, 이용약관, 시작 프롬프트, 테스트 케이스가 추가로 필요합니다. 이 저장소에는 임의의 신원이나 URL을 넣지 않았습니다.

## 로컬 설치와 테스트

GitHub 게시 전에는 저장소 루트를 로컬 마켓플레이스로 등록할 수 있습니다.

```bash
codex plugin marketplace add .
codex plugin add company-report@company-report-marketplace
```

설치 또는 업데이트 후에는 반드시 새 대화나 새 CLI 세션에서 테스트합니다.

## 저장소 구조

```text
.
├── README.md
├── LICENSE
├── .gitignore
├── .agents/plugins/marketplace.json
└── plugins/company-report
    ├── .codex-plugin/plugin.json
    └── skills/company-report
        ├── SKILL.md
        ├── agents/openai.yaml
        ├── references/component-system.md
        ├── references/design-system.md
        ├── references/font-setup.md
        ├── references/report-types.md
        └── assets
            ├── template.pptx
            └── fonts
                ├── NanumBarunGothic.otf
                ├── NanumBarunGothicBold.otf
                └── OFL.txt
```

## 공개 전 확인

- `plugin.json`의 작성자 이름을 실제 배포 주체에 맞게 수정합니다.
- 공개 제출용 웹사이트, 지원, 개인정보처리방침, 이용약관 URL을 준비합니다.
- 템플릿과 문서에 회사명, 로고, 고객명, 이메일, 전화번호, 주소가 없는지 확인합니다.
- 번들 글꼴이 공식 배포본인지, `OFL.txt`와 함께 배포되는지 확인합니다.
- 커밋 기록과 Git 설정에 토큰, 계정명, 내부 경로가 없는지 확인합니다.

## 라이선스

MIT License. 자세한 내용은 [LICENSE](LICENSE)를 확인하세요.
