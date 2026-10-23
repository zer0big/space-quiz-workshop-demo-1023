# Copilot 지침

## 명령어

- 빌드, 테스트, 린트 스크립트가 설정되어 있지 않습니다. 퀴즈를 실행하려면 브라우저에서 `index.html`을 직접 여세요.

## 아키텍처

- 앱은 자체 완결형 한국어 웹 페이지입니다. HTML, CSS, 퀴즈 데이터, JavaScript가 모두 `index.html`에 있으며, 런타임 의존성이나 서버가 필요하지 않습니다.
- `questions` 배열이 퀴즈 데이터의 원본입니다. `renderIntro`, `renderQuestion`, `renderResult`가 `#screen`에 각 화면을 렌더링하고, `selectAnswer`가 점수와 피드백을 갱신하며, `nextQuestion`이 다음 문항으로 진행합니다.
- 퀴즈 상태(`current`, `score`, `locked`)는 스크립트의 IIFE 내부 메모리에 보관됩니다. 상단 점수 표시는 렌더링된 화면과 별도로 갱신됩니다.

## 규칙

- 앱은 `index.html` 안에서 자체 완결형으로 유지하세요. 번들러나 모듈 시스템은 없습니다.
- 퀴즈 문항은 `questions` 배열에 추가하세요. 각 문항은 `question`, 네 개의 `options`, 0부터 시작하는 `answer` 인덱스, 짧은 `fact`로 구성합니다. 퀴즈 문항 수는 `questions.length`에서 가져옵니다.
- 동적으로 표시되는 화면의 마크업과 이벤트 리스너는 해당 렌더링 함수 안에 함께 두세요. 키보드 및 스크린 리더 피드백에는 기본 버튼, 명시적인 포커스 이동, 라이브 영역을 사용합니다.
- 화면을 변경할 때 한국어 UI와 기존 CSS 사용자 지정 속성 테마, `prefers-color-scheme` 라이트/다크 모드 스타일, `prefers-reduced-motion` 설정에 따른 동작을 유지하세요.
- 코드 변경 후 브라우저에서 퀴즈 시작, 답 선택, 다음 문항 이동, 결과 화면, 다시 시작, 키보드 조작을 확인하세요.
