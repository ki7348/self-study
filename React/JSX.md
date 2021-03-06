# React - JSX란?

## 설명

### JSX란?

- JSX(JavaScript XML)는 JavaScript에 XML을 추가한 확장 문법입니다.
  - XML은 다른 특수한 목적을 갖는 마크업 언어를 만드는데 사용하도록 권장하는 다목적 마크업 언어입니다.
- 브라우저에서 실행하기 전에 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환됩니다.
  - 즉, JSX는 HTML처럼 보이는 코드를 작성할 수 있게 해주는 자바스크립트 문법의 확장이라고 할 수 있습니다.

### JSX의 장점

- JSX는 하나의 파일에 자바스크립트와 HTML을 동시에 작성하여 편리합니다.

### JSX 문법

- 반드시 부모 요소 하나가 감싸는 형태여야 합니다.
  - Virtual DOM에서 컴포넌트 변화를 감지할 때 효율적으로 비교할 수 있도록 컴포넌트 내부는 하나의 DOM 트리 구조로 이루어져야 한다는 규칙이 있기 때문입니다.
- 자바스크립트 표현식
  - JSX 안에서도 자바스크립트 표현식을 사용할 수 있습니다.
  - 자바스크립트 표현식을 작성하려면 JSX 내부에서 코드를 {}로 감싸주면 됩니다.
  - if 구문과 for 루프는 JavaScript 표현식이 아니기 때문에 JSX 내부 자바스크립트 표현식에는 사용할 수 없습니다.
- React DOM은 HTML 어트리뷰트 이름 대신에 camelCase 프로퍼티 명명 규칙을 사용합니다.

  - JSX 스타일링
    - JSX에서 자바스크립트 문법을 쓰려면 {}를 써야 하기 때문에, 스타일을 적용할 때에도 객체 형태로 넣어 주어야 합니다.
    - 카멜 표기법으로 작성해야 합니다.
  - class 대신 className
    - JSX에서는 class가 아닌 className을 사용합니다.

- 개발자가 JSX를 작성하기만 하면, 리액트 엔진은 JSX를 기존 자바스크립트로 해석하여 줍니다.
  - 이를 '선언형 화면' 기술이라 합니다.
