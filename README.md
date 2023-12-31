# Paik language extension for Visual Studio Code

Visual Studio Code(VS Code)에서 "paik" 문법을 사용하기 위해 생성한 간단한 Language extension(언어 확장팩)입니다. 이 README는 스크래치 단계인 확장팩에 대한 간단한 메모입니다.

## 개요

"paik"은 간단하게 작성한 메모를 들여쓰기 레벨로 계층화하기 위해 만든 간단한 언어 포맷입니다. 마크업도, 마크다운도 아닌 일반 텍스트(plain text)를 기반으로 하며, YAML과 Python을 흉내내어, 들여쓰기 기반으로 데이터를 구조화하는 방식을 사용합니다. 이 익스텐션은 현재 문법에 대한 아무런 정의도 포함하고 있지 않습니다. 그럼에도 익스텐션을 제작한 이유는 다음과 같습니다.

- 언어 확장팩이 있어야만 VS Code에서 확장자와 Language Mode(언어 모드)를 매칭할 수 있습니다.
  - 확장팩이 없을 경우 `.paik` 확장자를 가진 파일을 `plain text`나 `YAML`처럼 "paik"의 들여쓰기와 유사한 포맷과 매칭해서 사용해야 합니다. 이 경우, 의도하지 않은 문법 하이라이팅이나 오류 알림이 발생할 수 있습니다. 또한 자동 포매팅 기능으로 인해 의도와 다르게 포맷이 변경될 수 있습니다.
- 이후 문법 오류나 자동 포매팅과 같은 기능을 지원하기 위해서는 언어 확장팩이 있어야 합니다.
  - 이 기능들에 대한 일정 계획은 없으나, 필요하다고 판단했을 때 쉽게 개발에 착수할 수 있도록 일종의 템플릿을 만들어 두기 위함힙니다.

## 사용법

- `paik` 폴더를 VS Code 익스텐션 폴더에 추가합니다.
  - 익스텐션 폴더 위치(Mac): `/Applications/Visual Studio Code.app/Contents/Resources/app/extensions`

## 앞으로의 계획

- 문법을 정리해서 문서화합니다.
  - 문서화한 문법은 문법 유효성 검사, 자동 포매팅에 사용합니다.
- 현재 제작 중인 [`paikwiki/paik2json`](https://github.com/paikwiki/paik2json)을 얼마나 더 진행하느냐에 이 패키지의 운명이 결정됩니다.

## 기타

- 이 언어팩은 "Log" 파일에 대한 언어팩을 참고하여 제작했습니다.
  - 이 과정에서 일부 설정 데이터를 삭제한 후, 빈 값으로 남겨둔 상태입니다.
  - 참고: https://github.com/microsoft/vscode/tree/83b909c39f0ce5368d3a41a30c609de86a2e106e/extensions/log
