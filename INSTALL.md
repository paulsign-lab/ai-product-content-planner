# 설치 매뉴얼 - Windows와 Mac 모두

이 문서는 강의에서 시연한 분석을 **여러분 컴퓨터에서 직접** 해 보기 위한 안내입니다. 순서대로만 진행하세요.
준비할 것은 세 가지입니다: ① Claude를 쓸 환경 ② 웹페이지를 읽을 브라우저 도구 ③ 이 저장소의 스킬.

> 도구와 메뉴 이름은 업데이트로 바뀔 수 있습니다. 막히면 각 항목의 공식 문서 링크를 먼저 확인하세요.
> 표시: **[Win]** Windows, **[Mac]** macOS

---

## 0. 미리 준비할 것

| 항목 | 용도 | 비고 |
|---|---|---|
| Claude 유료 구독 (Pro 이상) | Claude Code 사용 | 플랜별 사용 범위는 공식 안내 확인 |
| Node.js 18 이상 | **브라우저 도구(Playwright MCP)를 켜는 데 필요** | nodejs.org에서 LTS 설치. 아래 설명 참고 |
| Git (선택) | 저장소를 직접 내려받을 때만 | ZIP 파일로 받으면 필요 없음 |

> **왜 Node.js가 필요한가요?** Claude 데스크톱 앱 자체는 Node.js 없이 동작합니다. 하지만 리뷰를 읽는 브라우저 도구(Playwright MCP)가 Node.js로 실행되기 때문에 따로 설치해야 합니다. 브라우저 도구를 쓰지 않고 리뷰를 직접 붙여 넣는 방식(`USAGE.md` 참고)으로도 쓸 수 있으니, Node 설치가 어렵다면 그 방식으로 시작하세요.

유료 분석 도구(Semrush 등)는 필요 없습니다.

---

## STEP 1 - Claude를 쓸 환경 고르기 (둘 중 하나)

### 경로 A. Claude 데스크톱 앱의 **Code 탭** (비개발자 권장)
1. Claude 데스크톱 앱을 설치하고 로그인한 뒤 **Code** 탭을 엽니다. (공식: https://code.claude.com/docs/en/desktop-quickstart)
2. 바탕화면이나 문서 폴더에 작업 폴더를 하나 만듭니다. 예) `content-planner`
3. 입력창 아래의 **프로젝트 폴더**에서 그 폴더를 고릅니다.

### 경로 B. 통합개발환경(VS Code, Antigravity 등) + Claude Code
1. 통합개발환경을 설치하고 내장 **터미널**을 엽니다.
2. 공식 설치 안내를 따라 Claude Code를 설치하고 로그인합니다. Windows 요건은 공식 문서에 적혀 있으니 먼저 확인하세요. (공식: https://code.claude.com/docs/en/quickstart)
3. 작업 폴더를 만들고 그 폴더에서 `claude`를 실행합니다.
   - **[Mac]** `mkdir ~/content-planner && cd ~/content-planner && claude`
   - **[Win]** PowerShell: `mkdir $HOME\content-planner; cd $HOME\content-planner; claude`

---

## STEP 2 - 스킬 설치

> Claude Code는 스킬을 **`.claude/skills/`** 폴더에서 찾습니다. 그냥 `skills/`에 두면 인식되지 않습니다.
> 폴더 이름이 점(.)으로 시작하면 파일 탐색기에서 **숨겨져** 있을 수 있습니다.
> - **[Win]** 탐색기 위쪽 `보기` > `표시` > `숨긴 항목`을 켭니다.
> - **[Mac]** Finder에서 `Command + Shift + .`(마침표)를 누르면 숨김 파일이 보입니다.

### 방법 A. ZIP 파일로 직접 복사 (가장 확실, 권장)
강사가 준 `ai-product-content-planner.zip`을 사용합니다. 저장소가 비공개이면 이 방법을 쓰세요.
1. ZIP 파일의 압축을 풉니다.
2. 작업 폴더 안에 `.claude` 폴더를, 그 안에 `skills` 폴더를 만듭니다.
3. 압축을 푼 폴더의 **`skills` 안에 있는 폴더들**(content-start, site-scan 등 8개)을 방금 만든 `.claude/skills/`로 복사합니다. (`skills` 폴더 자체가 아니라 그 안의 내용입니다)
   - **터미널로 하려면 [Mac]** `mkdir -p ~/content-planner/.claude/skills && cp -R 내려받은폴더/skills/* ~/content-planner/.claude/skills/`
   - **터미널로 하려면 [Win]** PowerShell: `New-Item -ItemType Directory -Force $HOME\content-planner\.claude\skills; Copy-Item -Recurse 내려받은폴더\skills\* $HOME\content-planner\.claude\skills\`
4. 압축을 푼 폴더의 `templates` 폴더도 작업 폴더에 복사해 두면 편합니다(선택).

> **어느 폴더에서나 쓰고 싶다면** 작업 폴더 대신 사용자 폴더의 `.claude/skills/`(**[Mac]** `~/.claude/skills/`, **[Win]** `C:\Users\내이름\.claude\skills\`)에 복사합니다. 이 경우 모든 프로젝트에서 스킬이 보입니다.

### 방법 B. Claude에게 맡기기 (저장소 접근 권한이 있을 때)
저장소를 볼 수 있는 계정이라면 Claude Code(또는 Code 탭)에 아래처럼 입력합니다. 저장소 주소는 강사가 알려 드립니다.
```
<저장소 주소> 이 레포를 클론하고, 안의 skills 폴더에 있는 스킬들을 .claude/skills/ 에 설치해줘.
```
이 방법은 Git이 설치되어 있어야 하고, 승인창이 여러 번 뜹니다. 설치 후 앱을 한 번 재시작하세요.

### 설치 확인
입력창에 `/`를 입력했을 때 `content-start` 등 **스킬 8개**가 목록에 보이면 성공입니다. 안 보이면 앱을 완전히 종료했다가 다시 여세요.

```
작업폴더/
  .claude/skills/content-start/SKILL.md ... (스킬 8종)
  .mcp.json            <- STEP 3에서 만듭니다
```

---

## STEP 3 - 브라우저 도구 연결 (둘 중 하나, 또는 건너뛰기)

리뷰는 페이지가 열린 뒤에 나타나는 위젯이라 일반 웹 조회로는 읽을 수 없어서, 브라우저를 직접 조작하는 도구가 필요합니다.
**연결하지 않아도 사용할 수 있습니다.** 그 경우 리뷰를 직접 복사해서 붙여 넣는 방식으로 02단계를 진행합니다(`USAGE.md`).

### 선택 1 (기본). Playwright MCP
- **특징:** 항상 **새 브라우저(로그인 안 된 깨끗한 상태)** 로 열립니다. 이 스킬의 원칙(로그인하지 않고 공개 페이지만)과 맞습니다.
- **필요:** Node.js 18 이상 (위 0번 참고)
- **연결 방법 1 (Claude Code 터미널):** `claude mcp add playwright npx @playwright/mcp@latest`
- **연결 방법 2 (파일 이름 바꾸기):** 압축을 푼 폴더의 `.mcp.json.template` 파일을 작업 폴더에 복사하고 이름을 **`.mcp.json`** 으로 바꿉니다.
  - **데스크톱 앱 주의:** 공식 문서상 Code 탭은 `.mcp.json` 같은 설정 파일을 앱 안에서 수정하지 못할 수 있습니다. **Claude에게 만들어 달라고 하지 말고, 파일 탐색기에서 직접** 이름을 바꾸세요.
  - **[Win]** 탐색기에서 이름 바꾸기가 안 되면 PowerShell에서 `Rename-Item .mcp.json.template .mcp.json` (파일이 있는 폴더에서)
  - **[Mac]** 터미널에서 `mv .mcp.json.template .mcp.json`
  - 파일 확장명이 보이지 않으면 **[Win]** `보기` > `표시` > `파일 확장명`을 켭니다.
- **확인:** Claude에서 `/mcp`를 입력해 `playwright`가 연결(connected)로 보이는지 확인합니다.
- 출처: https://github.com/microsoft/playwright-mcp

### 선택 2 (대안). Claude in Chrome
- **특징:** 내 크롬에 확장 프로그램을 설치해 Claude가 크롬 탭을 조작합니다. 설치가 쉬운 대신 **내 브라우저의 로그인 상태를 공유**합니다.
- **반드시:** 쇼핑, 이메일 등에 로그인된 크롬이 아니라, **새 크롬 프로필(아무것도 로그인하지 않은 상태)** 을 만들어 쓰세요.
- **필요:** 크롬(또는 Edge 등 호환 브라우저), Claude in Chrome 확장 프로그램, Anthropic 직접 플랜(Pro, Max 등). `/login`으로 로그인해야 하며 API 키로 인증하면 이 기능은 꺼집니다.
- **연결:** Claude Code 터미널에서 `claude --chrome`으로 실행하거나, 실행 중에 `/chrome`을 입력합니다.
- **`[확인 필요]`** 공식 문서의 Chrome 연동 안내는 터미널(CLI)과 VS Code 확장 기준입니다. **데스크톱 앱 Code 탭에서도 되는지는 확인하지 못했습니다.** 데스크톱 앱을 쓴다면 선택 1을 쓰세요.
- 출처: https://code.claude.com/docs/en/chrome

---

## STEP 4 - 권한(허용) 설정

웹페이지를 읽는 작업이라 실행 중 **허용 여부를 묻는 창**이 여러 번 뜹니다. 처음에는 정상입니다.
- 처음에는 **기본 모드(그때그때 묻는 모드)** 로 시작하세요. 데스크톱 앱의 권한 모드 안내: https://code.claude.com/docs/en/desktop (Choose a permission mode)
- 허용해도 되는 것: **이 작업 폴더의 파일 저장**, **공개 상품 페이지 읽기**
- 허용하면 안 되는 것: 계정, 결제, 로그인이 필요한 화면 열기, 작업 폴더 밖의 파일 수정
- 모든 권한 확인을 건너뛰는 모드(bypass 등)는 쓰지 마세요. 외부 웹페이지를 읽는 작업이라 위험합니다.
- 승인 창에 사이트 단위로 "계속 허용"하는 선택지가 있으면 그것을 고르면 같은 사이트에서 묻는 횟수가 줄어듭니다.

---

## STEP 5 - 실행

작업 폴더에서 Claude(또는 Code 탭)를 열고 입력합니다.
```
콘텐츠 분석 시작하자
```
스킬이 먼저 진행 방식을 묻습니다. **처음이라면 "교육 모드"** 를 고르세요. 단계마다 설명하고 확인한 뒤 넘어갑니다.
처음에는 `examples/paulsign-us-serum/`의 `brand.md`와 `competitors.md`를 작업 폴더에 복사해 두고 흐름을 먼저 익혀도 좋습니다.
자세한 활용법은 [`USAGE.md`](USAGE.md)를 보세요.

---

## 트러블슈팅
- **스킬이 안 보임:** 폴더가 `.claude/skills/<스킬이름>/SKILL.md` 위치인지 확인하고 앱을 완전히 종료 후 다시 여세요. 숨김 폴더 표시를 켜야 폴더가 보입니다.
- **`npx`를 찾을 수 없음:** Node.js를 설치한 뒤 터미널과 앱을 완전히 종료했다가 다시 여세요.
- **`/mcp`에 playwright가 안 보임:** `.mcp.json` 이름과 위치(작업 폴더 바로 아래)를 확인하세요. 안 되면 브라우저 도구 없이 붙여넣기 방식으로 진행하세요.
- **리뷰가 안 읽힘:** 사이트가 막았거나(캡차, 접속 차단) 위젯이 늦게 뜨는 경우입니다. 스킬은 이를 `ACCESS FAILED`로 기록하고 붙여넣기 경로를 제안합니다. 억지로 우회하지 마세요.
- **Chrome 연결 실패:** `/chrome`에서 연결 상태를 확인하고 "Reconnect extension"을 선택하세요.

## 보안과 결과물 취급
- `outputs/`는 내부 기획용입니다. 경쟁사 이름과 리뷰 인용이 들어 있으므로 외부에 게시하거나 공개 저장소에 올리지 마세요.
- 비밀번호, API 키, 개인정보를 이 저장소나 결과물에 넣지 마세요. `.gitignore`가 `/outputs/`와 `.mcp.json`을 제외합니다.
