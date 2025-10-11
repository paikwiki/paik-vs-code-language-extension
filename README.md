# Paik language extension for Visual Studio Code

Visual Studio Code(VS Code)에서 "paik" 문법을 사용하기 위해 생성한 간단한 Language extension(언어 확장팩)입니다. 이 README는 스크래치 단계인 확장팩에 대한 간단한 메모입니다.

## 개요

"paik"은 간단하게 작성한 메모를 들여쓰기 레벨로 계층화하기 위해 만든 간단한 언어 포맷입니다. 마크업도, 마크다운도 아닌 일반 텍스트(plain text)를 기반으로 하며, YAML과 Python을 흉내내어, 들여쓰기 기반으로 데이터를 구조화하는 방식을 사용합니다. 이 익스텐션은 현재 문법에 대한 아무런 정의도 포함하고 있지 않습니다. 그럼에도 익스텐션을 제작한 이유는 다음과 같습니다.

- 언어 확장팩이 있어야만 VS Code에서 확장자와 Language Mode(언어 모드)를 매칭할 수 있습니다.
  - 확장팩이 없을 경우 `.paik` 확장자를 가진 파일을 `plain text`나 `YAML`처럼 "paik"의 들여쓰기와 유사한 포맷과 매칭해서 사용해야 합니다. 이 경우, 의도하지 않은 문법 하이라이팅이나 오류 알림이 발생할 수 있습니다. 또한 자동 포매팅 기능으로 인해 의도와 다르게 포맷이 변경될 수 있습니다.
- 이후 문법 오류나 자동 포매팅과 같은 기능을 지원하기 위해서는 언어 확장팩이 있어야 합니다.
  - 이 기능들에 대한 일정 계획은 없으나, 필요하다고 판단했을 때 쉽게 개발에 착수할 수 있도록 일종의 템플릿을 만들어 두기 위함힙니다.

## 지원 파일 확장자

이 확장팩은 다음의 파일 확장자를 지원합니다:

- `.paik.txt` - 다른 에디터에서도 일반 텍스트 파일로 인식되도록 하기 위한 확장자 (권장)
- `.paik` - paik 전용 확장자

`.paik.txt` 확장자를 사용하면 VS Code가 설치되지 않은 환경에서도 일반 텍스트 편집기로 파일을 열 수 있습니다.

## 사용법

### 설치

- `paik` 폴더를 VS Code 익스텐션 폴더에 추가합니다.
  - 익스텐션 폴더 위치(Mac): `/Applications/Visual Studio Code.app/Contents/Resources/app/extensions`
- VS Code를 재시작합니다.

### 들여쓰기 레벨별 색상 적용

이 확장팩은 들여쓰기 레벨(0~10)을 인식하여 각각 다른 scope를 부여합니다. 들여쓰기 레벨마다 다른 색상을 적용하려면 VS Code의 `settings.json`에 다음과 같이 설정을 추가하세요:

1. VS Code에서 `Command Palette` 열기 (`Cmd+Shift+P` 또는 `Ctrl+Shift+P`)
2. `Preferences: Open User Settings (JSON)` 선택
3. **최상위 레벨**에 다음 설정 추가 (**주의:** `[paik]` 같은 언어별 설정 섹션 안에 넣으면 안 됩니다):

```jsonc
{
  // 기존 설정들...
  "editor.tokenColorCustomizations": {
    "textMateRules": [
      {
        "scope": "meta.indent.level0.paik",
        "settings": {
          "foreground": "#7F8C8D"
        }
      },
      {
        "scope": "meta.indent.level1.paik",
        "settings": {
          "foreground": "#9B59B6"
        }
      },
      {
        "scope": "meta.indent.level2.paik",
        "settings": {
          "foreground": "#3498DB"
        }
      },
      {
        "scope": "meta.indent.level3.paik",
        "settings": {
          "foreground": "#1ABC9C"
        }
      },
      {
        "scope": "meta.indent.level4.paik",
        "settings": {
          "foreground": "#2ECC71"
        }
      },
      {
        "scope": "meta.indent.level5.paik",
        "settings": {
          "foreground": "#F1C40F"
        }
      },
      {
        "scope": "meta.indent.level6.paik",
        "settings": {
          "foreground": "#F39C12"
        }
      },
      {
        "scope": "meta.indent.level7.paik",
        "settings": {
          "foreground": "#E67E22"
        }
      },
      {
        "scope": "meta.indent.level8.paik",
        "settings": {
          "foreground": "#E74C3C"
        }
      },
      {
        "scope": "meta.indent.level9.paik",
        "settings": {
          "foreground": "#C0392B"
        }
      },
      {
        "scope": "meta.code-block.content.paik",
        "settings": {
          "foreground": "#999999"
        }
      },
      {
        "scope": "punctuation.definition.code-block.paik",
        "settings": {
          "foreground": "#666666"
        }
      }
    ]
  },

  // 다른 설정들...
  "[paik]": {
    "editor.tabSize": 2
  }
}
```

**참고:**
- 위 색상 코드는 예시이며, 원하는 색상으로 자유롭게 변경할 수 있습니다.
- 들여쓰기는 공백 2칸을 기준으로 합니다 (level 1 = 2칸, level 2 = 4칸, ...)
- 최대 레벨은 10입니다 (20칸 이상의 들여쓰기는 모두 level 10으로 표시)
- 코드 블록(```` ``` ````)으로 감싼 영역은 들여쓰기와 무관하게 회색(#999999)으로 표시됩니다

### 예시

다음과 같은 `example.paik.txt` 파일을 만들어 테스트해볼 수 있습니다:

```
프로젝트 관리
  할 일
    기능 개발
      로그인 기능
      회원가입 기능
    버그 수정
      레이아웃 깨짐
  완료된 작업
    설계
    환경 설정
  코드 샘플
    ```
    function hello() {
      console.log("Hello, Paik!");
    }
    ```
```

**색상 표시:**
- 각 줄의 들여쓰기 레벨에 따라 다른 색상으로 표시됩니다
- ```` ``` ```` 구분자로 감싼 코드 블록은 들여쓰기와 무관하게 회색으로 표시됩니다

## 앞으로의 계획

- 문법을 정리해서 문서화합니다.
  - 문서화한 문법은 문법 유효성 검사, 자동 포매팅에 사용합니다.
- 현재 제작 중인 [`paikwiki/paik2json`](https://github.com/paikwiki/paik2json)을 얼마나 더 진행하느냐에 이 패키지의 운명이 결정됩니다.

## 기타

- 이 언어팩은 "Log" 파일에 대한 언어팩을 참고하여 제작했습니다.
  - 이 과정에서 일부 설정 데이터를 삭제한 후, 빈 값으로 남겨둔 상태입니다.
  - 참고: https://github.com/microsoft/vscode/tree/83b909c39f0ce5368d3a41a30c609de86a2e106e/extensions/log
