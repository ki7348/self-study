# React - 리액트 라이프 사이클

## 설명

### 리액트 라이프 사이클이란?

- 리액트는 컴포넌트 기반의 View를 중심으로 한 라이브러리입니다.
- 각각의 컴포넌트에는 라이프 사이클 즉, 컴포넌트의 수명 주기가 존재합니다.
- 컴포넌트의 수명은 보통 페이지에서 렌더링되기 전인 준비 과정에서 시작하여 페이지에서 사라질 때 끝이납니다.

### 라이프 사이클의 분류

- 라이프 사이클은 총 9개가 존재합니다.
- 크게 세가지 유형으로 나눌 수 있는데 마운트, 업데이트, 언마운트라고 합니다.
- 마운트는 DOM이 생성되어 웹 브라우저 상에서 나타내는 것을 뜻하고, 언마운트는 DOM에서 제거되는 것을 말합니다.
- 업데이트는 다음과 같은 4가지 상황에서 발생합니다.
  - props가 바뀔 때
  - state가 바뀔 때
  - 부모 컴포넌트가 리렌더링 될 때
  - this.forceUpdate로 강제로 렌더링을 트리거할 때

### 라이프 사이클 메서드

- constructor

  - 컴포넌트를 만들 때 처음으로 실행되고 초기 state를 정할 수 있습니다.

  ```js
   constructor(props) {
    super(props);
    console.log("constructor");
  }
  ```

- getDerivedStateFromProps

  - props로 받아온 것을 state에 넣어주고 싶을 때 사용합니다.
  - 다른 생명주기 메서드와는 달리 static이 필요하고 안에서 this를 조회할 수 없습니다.
  - 특정 객체를 반환하면 해당 객체 안에 있는 내용들이 컴포넌트의 state로 설정이 됩니다.
  - 처음 렌더링 되기 전에 호출되고, 그 이후 렌더링 되기전에도 매번 실행됩니다.

  ```js
   static getDerivedStateFromProps(nextProps, prevState) {
    console.log("getDerivedStateFromProps");
    if (nextProps.color !== prevState.color) {
      return { color: nextProps.color };
    }
    return null;
  }
  ```

- render

  - 컴포넌트를 렌더링하는 메서드

  ```js
  // Class
  class Example extends React.Component {
    render() {
      return <div>컴포넌트</div>;
    }
  }
  ```

- componentDidMount

  - 컴포넌트의 첫번째 렌더링이 마치고 나면 호출되는 메서드입니다.
  - 함수형 컴포넌트의 useEffect를 활용하여 기능을 구현할 수 있습니다.

- shouldComponentUpdate

  - props나 state를 변경했을 때 리렌더링을 할지 말지 결정하는 메서드입니다.
  - 반드시 true나 false를 반환해야 합니다.

  ```js
  shouldComponentUpdate(nextProps, nextState) {
    console.log("shouldComponentUpdate", nextProps, nextState);
    // 숫자의 마지막 자리가 4면 리렌더링하지 않습니다
    return nextState.number % 10 !== 4;
  }
  ```

- getSnapshotBeforeUpdate

  - render에서 만들어진 결과가 브라우저에 실제로 반영되기 직전에 호출됩니다.
  - 다음에 componentDidpdate 메서드가 실행됩니다.

- componentDidUpdate

  - 리렌더링을 완료한 후 실행됩니다.
  - 3번째 파라미터로 getSnapshotBeforeUpdate에서 반환한 값을 조회할 수 있습니다.

- componentWillUnmount

  - 컴포넌트가 화면에서 사라지기 직전에 호출됩니다.
  - useEffect 클린업 함수를 통해 해당 메서드를 구현할 수 있습니다.

- componentDidCatch

  - 컴포넌트 렌더링 도중에 에러가 발생했을 때 어플리케이션이 멈추지 않고 오류 UI를 보여줄 수 있게 해줍니다.

- Mount시점
  - constructor
  - getDerivedStateFromProps
  - render
  - componentDidMount
- Update시점
  - getDerivedStateFromProps
  - shouldComponentUpdate
  - render
  - getSnapshotBeforeUpdate
  - componentDidUpdate
- Unmount시점
  - componentWillUnmount
