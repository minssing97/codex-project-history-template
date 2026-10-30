# Codex 프로젝트 개발 이력 템플릿

VS Code + Codex에서 **사용자 프롬프트와 주요 작업 결과만** 프로젝트별로 기록하고, GitHub를 통해 다른 PC에서도 개발 맥락을 이어가기 위한 경량 템플릿입니다.

> **핵심 원칙:** Codex 전체 세션이나 `CODEX_HOME`을 옮기지 않습니다. 소스코드와 함께 `CODEX_HISTORY.md`를 Git에 저장합니다.

## 1. 파일 구성

```text
project-name/
├── .gitignore                  # 비밀정보 및 로컬 파일 Git 제외
├── AGENTS.md                   # Codex의 상시 개발·기록 규칙
├── CODEX_HISTORY.md           # 프롬프트 / 결과 / 테스트 / 후속 작업
├── README.md                  # 템플릿 및 사용법(프로젝트에 맞게 변경)
└── prompts/
    ├── SESSION_START.md       # 새 PC/새 대화에서 작업 재개
    ├── SESSION_END.md         # 작업 종료 시 기록 검토
    └── IMPORT_EXISTING.md     # 기존 프로젝트에 처음 적용
```

## 2. 기존 개발 프로젝트에 적용

1. 이 템플릿의 `AGENTS.md`, `CODEX_HISTORY.md`, `prompts/`를 기존 프로젝트 루트에 복사합니다.
2. 기존 프로젝트에 이미 `AGENTS.md`가 있으면 **덮어쓰지 말고** 이 템플릿의 개발 이력 규칙을 병합합니다.
3. `.gitignore`가 이미 있으면 이 템플릿의 보안 제외 규칙을 추가합니다.
4. VS Code로 프로젝트 폴더를 열고 Codex를 실행합니다.
5. 기존 작업을 정리하려면 `prompts/IMPORT_EXISTING.md`의 프롬프트를 사용합니다.
6. 변경 내용을 검토하고 Git에 커밋·푸시합니다.

## 3. 새 프로젝트 시작

GitHub에서 이 저장소를 Template repository로 지정한 뒤 **Use this template → Create a new repository**를 선택합니다.

새 저장소를 PC로 가져옵니다.

```powershell
git clone https://github.com/<OWNER>/<NEW_REPOSITORY>.git
cd <NEW_REPOSITORY>
code .
```

프로젝트 목적 및 실행 방법에 맞게 이 `README.md`와 필요 시 `AGENTS.md`를 수정합니다.

## 4. 여러 PC에서 작업 이어가기

**작업을 마치는 PC**

1. Codex 작업이 완료될 때 `CODEX_HISTORY.md`에 주요 프롬프트와 결과가 기록되었는지 확인합니다.
2. `git status`로 변경 파일을 확인합니다.
3. 커밋하고 푸시합니다.

```powershell
git status
git add .
git commit -m "docs: record Codex development progress"
git push
```

**작업을 이어갈 PC**

1. 처음이면 `git clone`, 이미 복제한 프로젝트면 `git pull`을 실행합니다.
2. VS Code에서 프로젝트 루트를 엽니다.
3. `prompts/SESSION_START.md`를 Codex에 입력합니다.
4. Codex가 변경 상태와 남은 작업을 확인하면 개발을 이어갑니다.

```powershell
git pull
code .
```

> 두 PC에서 동시에 같은 브랜치/파일을 편집하지 않는 것이 안전합니다. 커밋·푸시 전에 충돌과 비밀정보 포함 여부를 확인하세요.

## 5. CODEX_HISTORY.md 기록 예시

아래는 **예시이며 실제 개발 이력이 아닙니다.** 실제 기록은 `CODEX_HISTORY.md`의 `## 작업 기록` 아래에 추가하세요.

```markdown
### 2026-10-30 | 작업 #001 | 엑셀 업로드 기능

**사용자 프롬프트**
> 엑셀 파일을 업로드하고 계획량과 실적량을 표시해 줘.

**주요 결과**
- 엑셀 파일 선택 UI 추가
- 데이터 파싱 함수 구현

**변경 파일**
- `index.html`
- `src/excel.js`

**검증 결과**
- 코드 정적 검토 완료
- 브라우저 실행 테스트는 미실시

**미해결 / 다음 작업**
- 잘못된 파일 형식에 대한 오류 메시지 추가
```

## 6. 중요한 제한과 보안

- `AGENTS.md`는 **Codex에 기록을 요청하는 지침**입니다. 운영체제 수준의 자동 녹화/로깅 기능이 아닙니다. Codex가 작업을 중단하거나 파일을 수정하지 못하면 기록이 누락될 수 있습니다.
- Codex가 접근할 수 없는 이전 대화는 복원할 수 없습니다. 기존 이력을 정리할 때 추정 내용을 사실처럼 작성하지 않습니다.
- 프롬프트에 API 키, 토큰, 개인정보 또는 비밀번호가 있으면 기록 전 비식별화합니다.
- `.env`, `.codex`, `.codex-home`, 세션 파일, 로컬 DB와 인증정보를 GitHub에 올리지 않습니다.
- `CODEX_HISTORY.md`는 실제 로그 파일이 아닌 **개발 이력 요약 문서**입니다.

## 7. 이 저장소를 GitHub 템플릿으로 등록하는 방법

1. GitHub에서 새 저장소를 만듭니다(예: `codex-project-history-template`).
2. 이 폴더 **안의 파일과 폴더**를 저장소에 업로드합니다. ZIP 파일 자체를 업로드하지 않습니다.
3. 해당 저장소에서 **Settings → General → Template repository**에 체크합니다.
4. 다음 프로젝트부터 **Use this template → Create a new repository**를 이용합니다.

### PowerShell에서 최초 업로드 (빈 GitHub 저장소를 만든 후)

```powershell
cd <TEMPLATE_FOLDER>
git init -b main
git add .
git commit -m "Initial Codex project history template"
git remote add origin https://github.com/<OWNER>/codex-project-history-template.git
git push -u origin main
```

**주의:** GitHub에서 저장소를 만들 때 README 등 초기 파일을 추가하지 않은 빈 저장소로 만드는 것이 위 명령의 충돌을 피하기 쉽습니다.
