# Font Setup

번들 글꼴은 `assets/fonts`의 나눔바른고딕 OTF Regular/Bold이다. 슬라이드 소스와 PPTX에는 내부 글꼴 이름인 `NanumBarunGothicOTF`를 정확히 사용한다.

## 웹 작업 환경

슬라이드 소스를 만들기 전에 현재 스킬 디렉터리를 기준으로 글꼴 파일을 찾고, 호스트의 현재 작업 세션에만 등록한다. 시스템 글꼴 폴더나 영구 사용자 환경은 변경하지 않는다.

Linux 계열의 격리된 웹 호스트에서 셸을 사용할 수 있으면 다음과 동등한 작업을 수행한다. `$SKILL_DIR`은 현재 스킬 디렉터리의 실제 경로로 정한다.

```bash
FONT_ASSET_DIR="$SKILL_DIR/assets/fonts"
FONT_INSTALL_DIR="${XDG_DATA_HOME:-${HOME}/.local/share}/fonts/company-report"
mkdir -p "$FONT_INSTALL_DIR"
cp "$FONT_ASSET_DIR"/NanumBarunGothic*.otf "$FONT_INSTALL_DIR"/
if command -v fc-cache >/dev/null 2>&1; then fc-cache -f "$FONT_INSTALL_DIR"; fi
if command -v fc-match >/dev/null 2>&1; then fc-match "NanumBarunGothicOTF"; fi
```

호스트가 별도의 글꼴 등록 기능을 제공하면 그 기능을 우선 사용한다. 글꼴 파일을 설치할 수 없는 환경에서는 사용자에게 제한을 알리고 대체 글꼴 사용 승인을 받는다.

## 확인

1. 글꼴 파일이 유효한 OTF인지 확인한다.
2. `NanumBarunGothicOTF`가 실제로 조회되는지 확인한다.
3. 한국어 Regular/Bold 표본을 작게 렌더링해 글리프, 굵기, 줄바꿈을 확인한다.
4. 확인에 실패하면 PNG 제작을 계속하지 않는다.

Regular와 Bold만 사용한다. Light와 UltraLight는 번들하지 않았으므로 요청 없이 지정하지 않는다. `NanumBarunGothic`처럼 내부 이름과 다른 표기를 소스에 사용하지 않는다.

## PPTX 전달

현재 프레젠테이션 내보내기가 글꼴 파일 자체의 내장을 보장하지 않으면 PPTX에는 글꼴 이름만 기록된 것으로 간주한다. 최종 전달 때 수신자의 PowerPoint 환경에도 나눔바른고딕 설치가 필요하다고 안내한다. 글꼴을 이미지나 윤곽선으로 바꾸어 편집 가능성을 없애지 않는다.
