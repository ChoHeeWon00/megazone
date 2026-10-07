# VS Code 터미널 글자 크기 조정 방법

## 1. 설정 화면에서 변경 (권장)

1. `Ctrl + ,` (Mac: `Cmd + ,`)로 설정을 엽니다.
2. 검색창에 `terminal font size`를 입력합니다.
3. **Terminal › Integrated: Font Size** 값을 원하는 숫자로 바꿉니다. 예: 14, 16

## 2. settings.json에 직접 입력

`Ctrl + Shift + P` → **Preferences: Open User Settings (JSON)**을 열고 아래 줄을 추가합니다.

```json
"terminal.integrated.fontSize": 16
```

## 3. 명령으로 잠깐만 확대/축소

명령 팔레트(`Ctrl + Shift + P`)에서 다음 명령을 실행합니다.

| 명령 | 동작 |
|---|---|
| `Terminal: Increase Font Size` | 터미널 글자 확대 |
| `Terminal: Decrease Font Size` | 터미널 글자 축소 |
| `Terminal: Reset Font Size` | 원래 크기로 복원 |

자주 쓴다면 단축키를 지정해 두면 편리합니다.

> **참고:** `Ctrl + +` / `Ctrl + -`는 터미널만이 아니라 VS Code 전체 화면을 확대/축소합니다.
