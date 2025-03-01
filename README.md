# Claude Code 사용 매뉴얼

> Anthropic의 터미널 기반 AI 코딩 도우미 Claude Code 설치 및 사용 가이드

## 목차

- [소개](#소개)
- [요구사항](#요구사항)
- [설치 과정](#설치-과정)
- [기본 사용법](#기본-사용법)
- [주요 명령어](#주요-명령어)
- [작업 예시](#작업-예시)
- [문제 해결](#문제-해결)
- [고급 사용법](#고급-사용법)
- [비용 및 청구](#비용-및-청구)

## 소개

Claude Code는 Anthropic에서 개발한 터미널 기반 AI 코딩 도우미입니다. 코드베이스를 분석하고, 버그를 찾고, 코드를 작성하는 등의 다양한 개발 작업을 도와줍니다.

- **연구 미리보기(Research Preview) 상태**: 현재 Claude Code는 베타 단계로, 일부 기능에 제한이 있을 수 있습니다.
- **API 기반 과금**: Claude Code는 Anthropic Console 계정을 통해 API 사용량에 따라 과금됩니다.

## 요구사항

Claude Code를 사용하기 위해 필요한 요구사항:

- **운영체제**: Mac OS, Linux (Windows의 경우 WSL 필요)
- **Node.js**: 버전 16 이상
- **npm**: 최신 버전
- **Anthropic 계정**: API 키 생성 및 결제 설정 필요

## 설치 과정

### Windows에서 설치하기 (WSL 사용)

Claude Code는 현재 Windows를 직접 지원하지 않습니다. Windows Subsystem for Linux(WSL)를 통해 사용해야 합니다.

#### 1. WSL 설치

1. 관리자 권한으로 PowerShell을 실행합니다
2. 다음 명령어로 WSL과 Ubuntu를 설치합니다:
   ```powershell
   wsl --install -d Ubuntu
   ```
3. 설치 완료 후 컴퓨터를 재부팅합니다
4. Ubuntu가 자동으로 실행되며 사용자 이름과 비밀번호를 설정합니다

#### 2. Node.js 및 npm 설치

WSL Ubuntu 터미널에서:

```bash
# 패키지 목록 업데이트
sudo apt update

# Node.js와 npm 설치
sudo apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs

# 설치 확인
node -v  # v18.x.x 이상이어야 함
npm -v   # 최신 버전 확인
```

#### 3. Claude Code 설치

```bash
# Claude Code 전역 설치
sudo npm install -g @anthropic-ai/claude-code
```

### Mac/Linux에서 설치하기

터미널에서:

```bash
# Claude Code 전역 설치
npm install -g @anthropic-ai/claude-code
```

## 기본 사용법

### 1. Claude Code 실행

WSL Ubuntu나 터미널에서:

```bash
# 작업할 프로젝트 디렉토리로 이동
cd /프로젝트/경로

# Claude Code 실행
claude-code
```

또는 npx를 사용하여 실행:

```bash
npx @anthropic-ai/claude-code
```

npx로 실행하면 설치된 위치를 찾지 못할 때 유용합니다.

### 2. 계정 로그인

Claude Code를 처음 실행하면 Anthropic 계정으로 로그인해야 합니다:

1. 브라우저가 자동으로 열리지 않으면 표시된 URL로 이동
2. Anthropic 계정으로 로그인
3. API 키 생성 권한 및 사용 약관 동의
4. 표시된 인증 코드를 Claude Code 터미널에 붙여넣기
5. 결제 방법 설정 (처음 사용 시 약 $5 결제)

### 3. 프로젝트 초기화

Claude Code가 처음 실행되면 다음 명령어로 프로젝트를 초기화할 수 있습니다:

```
/init
```

이 명령어는 프로젝트 루트에 `CLAUDE.md` 파일을 생성합니다. 이 파일에 프로젝트에 대한 설명이나 Claude Code에 대한 지침을 작성할 수 있습니다.

## 주요 명령어

Claude Code에서 사용할 수 있는 주요 명령어:

| 명령어 | 설명 |
|--------|------|
| `/help` | 도움말 표시 |
| `/init` | CLAUDE.md 파일 생성 |
| `!` | bash 명령어 모드 전환 |
| `esc` | 명령 실행 취소 |
| `/` | 명령어 모드 활성화 |
| `try "edit <filepath> to..."` | 특정 파일 편집 요청 |

## 작업 예시

### 코드베이스 분석 요청

```
이 프로젝트의 구조와 주요 기능을 설명해줄 수 있나요?
```

### 버그 해결 요청

```
검색 기능이 작동하지 않아요. 검색어를 입력해도 결과가 나오지 않습니다. 이 문제를 해결해주세요.
```

### 코드 수정 요청

```
User.js 파일의 로그인 함수에 이메일 유효성 검사를 추가해주세요.
```

### 새 기능 구현 요청

```
Todo 항목에 마감일을 추가하는 기능을 구현해주세요.
```

## 문제 해결

### Claude Code를 찾을 수 없는 경우

**증상:** `claude-code: command not found` 오류 발생

**해결책:**
1. 글로벌 npm 패키지 경로 확인:
   ```bash
   npm root -g
   ```
2. 설치된 Claude Code 찾기:
   ```bash
   find $(npm root -g) -name "*claude*"
   ```
3. npx로 실행 시도:
   ```bash
   npx @anthropic-ai/claude-code
   ```
4. PATH에 npm 글로벌 바이너리 경로 추가:
   ```bash
   echo 'export PATH="'$(npm root -g)'/../bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ```

### npm 명령어가 없는 경우

**증상:** `npm: command not found`

**해결책:**
```bash
sudo apt update
sudo apt install -y nodejs npm
```

### Windows에서 설치 실패

**증상:** `npm error notsup Unsupported platform for @anthropic-ai/claude-code: wanted {"os":"!win32"}`

**해결책:**
Claude Code는 Windows를 직접 지원하지 않습니다. WSL을 설치하고 Linux 환경에서 실행해야 합니다.

### WSL 접속 문제

**증상:** WSL에 접속할 수 없거나 Docker Desktop WSL만 나타남

**해결책:**
1. WSL 목록 확인:
   ```powershell
   wsl --list --verbose
   ```
2. Ubuntu가 이미 있다면 직접 접속:
   ```powershell
   wsl -d Ubuntu
   ```
3. 새로운 Ubuntu 배포판 설치:
   ```powershell
   wsl --install -d Ubuntu-22.04
   ```
4. 문제가 지속되면 기존 배포판 제거 후 재설치:
   ```powershell
   wsl --unregister Ubuntu
   wsl --install -d Ubuntu
   ```

### 자동 업데이트 실패

**증상:** `X Auto-update failed · Try claude doctor or npm i -g @anthropic-ai/claude-code`

**해결책:**
1. Claude Doctor 실행:
   ```bash
   claude doctor
   ```
2. 또는 재설치:
   ```bash
   npm i -g @anthropic-ai/claude-code
   ```

### 브라우저 인증 문제

**증상:** "Browser didn't open? Use the url below to sign in"

**해결책:**
표시된 URL을 복사하여 브라우저에 붙여넣고 로그인한 후, 인증 코드를 터미널에 복사하세요.

## 고급 사용법

### CLAUDE.md 파일 활용

CLAUDE.md 파일에 프로젝트 설명, 아키텍처, 코딩 스타일 등을 상세히 기록하면 Claude Code가 더 정확한 응답을 제공할 수 있습니다.

예시:
```markdown
# 프로젝트: 할 일 관리 앱

## 기술 스택
- 프론트엔드: React, TypeScript
- 백엔드: Node.js, Express
- 데이터베이스: MongoDB

## 코딩 컨벤션
- 함수는 camelCase 사용
- 컴포넌트는 PascalCase 사용
- 탭 대신 2칸 공백 사용
```

### 프로젝트 디렉토리 최적화

Claude Code는 프로젝트 전체를 분석하므로, 불필요한 파일이나 폴더가 많으면 성능이 저하될 수 있습니다. `.claudeignore` 파일을 생성하여 분석에서 제외할 항목을 지정할 수 있습니다.

예시 `.claudeignore`:
```
node_modules/
dist/
.git/
*.log
```

## 비용 및 청구

Claude Code는 API 사용량에 따라 과금됩니다:

- 초기 사용 시 약 $5를 Anthropic 계정에 충전해야 합니다
- 복잡한 질문이나 큰 코드베이스 분석 시 더 많은 비용이 발생할 수 있습니다
- 비용은 Anthropic Console에서 확인 가능합니다

## 추가 정보

- 공식 문서: [Claude Code 문서](https://docs.anthropic.com/claude/docs/claude-code)
- 최신 업데이트: [Anthropic 블로그](https://www.anthropic.com/blog)

---

이 매뉴얼은 Claude Code의 기본 사용법과 문제 해결 방법을 다루고 있습니다. Claude Code는 계속 발전하고 있으므로, 최신 정보는 Anthropic의 공식 문서를 참조하세요.
