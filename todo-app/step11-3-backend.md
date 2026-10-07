# STEP 11-3. 서버 틀 만들기 — 주방 만들기 (PLAN P-12)

## 📚 이 단계에서 참고하는 파일

| 참고 파일 | 무엇을 가져오나 | 왜 참고하나 |
|---|---|---|
| ARCHITECTURE.md | 서버 = FastAPI, 실행 위치 | 어떤 기술로, 어느 폴더(backend)에 만들지 정해요. |
| API-SPEC.md | `GET /health` → `{"status":"ok"}` | 오늘 만들 **유일한 주소**예요. 문서에 적힌 대로 만들어요. |
| PLAN.md | 구현 인계, P-12 | 할 일 API와 저장소는 **아직** 만들지 않아요. |
| AGENTS.md | 환경 칸 | 이 단계가 끝나면 **실제 버전과 포트**로 채워요. |

---

## 🧸 쉽게 말하면

요리는 아직 안 하고 **주방 불만 켜요.** "주방 열었어요?" 하고 물으면 "네!"라고 대답하게 만들어요. 이 대답하는 곳이 **`/health`**(건강 확인)예요.

## 🎯 이 단계가 끝나면

- `http://localhost:8000/health` → `{"status": "ok"}`
- `http://localhost:8000/docs` → **서버 설명서 화면** (FastAPI가 자동으로 만들어 줘요)

> 💡 `/docs`는 **주문서 견본집**이에요. 나중에 API가 생기면 여기서 직접 눌러 볼 수 있어요.

---

## 🗣️ AI와 대화하며 진행하기

### 대화 1. 계획 받기

- claude-code 입력
```claude-code
PLAN의 P-12를 "진행 중"으로 바꾸세요.
ARCHITECTURE.md와 API-SPEC.md를 기준으로 backend 폴더에 FastAPI 서버의 기본 틀만 만들려고 합니다.
API-SPEC에 적힌 GET /health 하나만 만들고 {"status": "ok"}를 돌려주게 하세요.
할 일 API와 저장소(SQLite)는 아직 만들지 마세요.
1. 파이썬 도구는 uv를 사용하세요. 실행할 명령과 만들어질 파일을 순서대로 보여 주세요.
2. 서버를 켜는 명령과 확인할 주소를 알려 주세요.
계획만 보여 주고 승인을 기다리세요.
```

**AI 대답 예시**
> 1. `backend` 폴더를 만들고 `uv init`으로 파이썬 프로젝트를 준비합니다.
> 2. `uv add fastapi uvicorn`으로 서버 부품을 받습니다.
> 3. `main.py`에 `/health`를 만듭니다.
> 4. `uv run uvicorn main:app --reload --port 8000`으로 켭니다.

**AI가 만들 코드 예시 (읽기만 해요)**

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/health")          # "주방 열었어요?" 라고 물으면
def health():
    return {"status": "ok"}  # "네!" 라고 대답
```

- [ ] `backend` 폴더 안에만 만드나요?
- [ ] 할 일 API나 저장소를 미리 만들지 않나요?

---

### 대화 2. 실행하고 내 눈으로 확인

> ⚠️ 화면 서버(11-2)는 켜 둔 채로, **새 터미널**에서 서버를 켜요.

- claude-code 입력
```claude-code
계획을 승인합니다. 화면 서버가 켜진 터미널은 그대로 두고, 새 터미널에서 backend 작업을 하세요.
한 단계씩 실행하고 결과를 보여 준 뒤 서버를 켜 두세요.
```

- [ ] `/health`에 `{"status": "ok"}`가 보이나요?
- [ ] `/docs`에 설명서 화면이 보이나요?

```
지금 켜져 있는 것
터미널 1: 화면 서버 (5173)  ← 계속 켜 둠
터미널 2: API 서버 (8000)   ← 계속 켜 둠
```

---

## 🔄 함께 고치기

| 바뀐 것 | 고칠 파일 | 고칠 칸 | 이유 |
|---|---|---|---|
| /health 확인 | PLAN | P-12 상태, 실제 검증 결과, 다음 행동 | 진행 상황 |
| 서버 켜는 명령 실행 | README | 실행 방법 | 실행해 본 명령만 |
| 실제 버전·포트 확정 | **AGENTS** | 환경 | 새 대화 AI가 같은 환경으로 일하게 |
| backend 폴더 생김 | README | 프로젝트 문서 | 폴더 역할 안내 |

- claude-code 입력
```claude-code
/health와 /docs를 확인했습니다. 함께 고칠 곳을 표로 먼저 보여 주고, 확인하면 고치세요.
- PLAN.md: P-12 "완료", 실제 검증 결과에 명령·주소·결과, 다음 행동 "P-13 화면·서버 연결"
- README.md: 실행 방법에 서버를 켜는 방법 추가 (터미널 2개 필요하다는 것도)
- README.md: 프로젝트 문서에 "backend/: 서버(FastAPI)와 저장소" 추가
- AGENTS.md: 환경 칸에 Node.js·Python·uv 실제 버전, 화면 5173·서버 8000 포트, frontend·backend 폴더
```

---

## 😵 막혔을 때

| 보이는 글 | 뜻 | 해결 |
|---|---|---|
| `ModuleNotFoundError: No module named 'fastapi'` | 부품이 설치 안 됐거나 다른 파이썬으로 실행함 | "uv run으로 실행했는지, uv add를 했는지 확인해 주세요" |
| `Address already in use` / `[Errno 10048]` | 8000번 방을 이미 누가 씀 | 다른 터미널의 서버를 끄기 |
| `Could not import module "main"` | 엉뚱한 폴더에서 실행 | backend 폴더 안에서 실행 |
| `{"detail":"Not Found"}` | 주소 오타 | `/health` 철자 확인 |

---

## 💾 저장 기록 남기기

- claude-code 입력
```claude-code
바뀐 파일 목록을 보여 주세요. 파이썬 가상환경 폴더(.venv)와 캐시가 Git에 올라가지 않는지 .gitignore를 확인한 뒤, "chore: add backend skeleton with health" 메시지로 커밋하세요.
```

## ➡️ 다음 단계

**11-4. 화면과 서버 연결하기** (PLAN P-13)
