# Company Report Codex Plugin

회사 보고용 16:9 슬라이드를 요구사항 정리부터 구조 승인, PNG 시안 승인, 편집 가능한 PPTX 내보내기까지 순서대로 만드는 Codex 플러그인입니다.

## 주요 동작

- 기본 결과물은 1페이지 요약 1장입니다.
- 필요한 경우에만 백데이터 슬라이드를 제안합니다.
- 구조를 먼저 텍스트로 제시하고 명시적 승인을 받습니다.
- 같은 편집 가능한 원본에서 PNG와 PPTX를 생성합니다.
- PNG 승인 전에는 최종 PPTX를 제공하지 않습니다.
- 번들 템플릿에는 실제 회사 로고, 고객 정보, 사내 화면이 없습니다.

## 설치

저장소를 복제한 뒤 저장소 루트를 로컬 마켓플레이스로 추가합니다.

```bash
git clone <this-repository-url>
cd skill-company-report-maker
codex plugin marketplace add "$PWD"
codex plugin add company-report@company-report-marketplace
```

설치 후 새 Codex 스레드에서 다음처럼 시작합니다.

```text
$company-report를 사용해 경영진용 1페이지 진행 보고서를 만들어줘.
```

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
        ├── references/design-system.md
        ├── references/report-types.md
        └── assets/template.pptx
```

## 공개 전 확인

- `plugin.json`의 작성자 이름을 실제 배포 주체에 맞게 수정합니다.
- README의 `<this-repository-url>`을 실제 GitHub 주소로 바꿉니다.
- 템플릿과 문서에 회사명, 로고, 고객명, 이메일, 전화번호, 주소가 없는지 확인합니다.
- 커밋 기록과 Git 설정에 토큰, 계정명, 내부 경로가 없는지 확인합니다.

## 라이선스

MIT License. 자세한 내용은 [LICENSE](LICENSE)를 확인하세요.
