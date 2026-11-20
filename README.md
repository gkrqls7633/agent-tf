# agent-tf

프로젝트 폴더에서 아래 한 줄을 실행하면 그 프로젝트에 팀이 투입됩니다.

```powershell
claude plugin marketplace add https://github.com/gkrqls7633/agent-tf --scope project; claude plugin install agent-tf@agent-tf --scope project
```

그다음 Claude Code 에서 `/agent-tf:lead <맡길 일>` 로 팀장에게 일을 맡깁니다.

- 비공개 저장소입니다. 투입하는 PC 에 이 저장소를 읽을 수 있는 GitHub 인증이 있어야 합니다.
- project 범위로 설치되어 그 프로젝트의 `.claude/settings.json` 에 기록됩니다.
- 새 버전 받기: `claude plugin marketplace update agent-tf`

## 팀

관리자(사용자)는 팀장에게만 말합니다. 팀장은 메인 세션이 따르는 skill 이고, 팀원은 에이전트입니다.

| 팀원 | 하는 일 |
|---|---|
| `planner` | 요구를 완료 기준이 있는 기획안으로 만듭니다. 화면 흐름과 역할(관리자, 사용자)을 정합니다. |
| `backend` | 서버 쪽 검토와 구현. 테스트를 먼저 씁니다. |
| `frontend` | 화면 쪽 검토와 구현. 기존 화면 구성 요소를 먼저 찾아 씁니다. |
| `reviewer` | 바뀐 코드의 버그, 보안, 규칙 위반을 봅니다. 고치지 않고 보고만 합니다. |
| `qa` | 테스트와 서버를 실제로 돌리고 화면과 완료 기준을 확인합니다. |
| `devops` | 프로젝트에 적힌 방법으로 배포합니다. 관리자 승인 뒤에만 실행합니다. |

## 흐름

조각 하나마다 아래를 처음부터 끝까지 거칩니다.

```
1. planner 기획안 초안
2. backend, frontend 검토와 상호 피드백(최대 2회) → 최종 기획안
   [관리자 확인 1] 최종 기획안 승인
3. backend, frontend 구현
4. reviewer 리뷰와 자동 테스트
   [관리자 확인 2] 개발 완료 보고. "다음 진행" 까지 기다림
5. qa 실제 실행과 화면 확인
   [관리자 확인 3] 커밋, push, 배포를 각각 승인
6. devops 배포
```

진행 기록은 조각마다 프로젝트의 `docs/tf/YYYY-MM-DD-<주제>.md` 파일 하나에 남습니다.

## 프로젝트에 적어 둘 것

팀원은 프로젝트마다 다른 것을 그 프로젝트의 `CLAUDE.md` 와 `.claude/rules/` 에서 읽습니다. 없으면 팀장이 처음에 묻습니다.

- 테스트와 실행 명령
- 배포 방법
- 화면과 UX 기준, 코딩 규칙
- 화면 확인 방법(적지 않으면 로컬 Playwright)

## 설계

- [설계 문서](docs/specs/2026-11-20-agent-tf-design.md)
- [구현 계획](docs/plans/2026-11-20-agent-tf.md)
