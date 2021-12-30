# JavaScript - 이벤트

## 설명

### 이벤트 객체

- 이벤트가 발생하면 이벤트에 관련한 다양한 정보를 담고 있는 이벤트 객체가 동적으로 생성된다.
- 생성된 이벤트 객체는 이벤트 핸들러의 첫 번째 인수로 전달된다.
```js
const $msg = document.querySelector('.message');
// 클릭 이벤트에 의해 생성된 이벤트 객체는 이벤트 핸들러의 첫 번째 인수로 전달된다.
function showCoords(e){
    $msg.textContent = `clientX: ${e.clientX}, clientY: ${e.clientY}`;
}
document.onclick = showCoords;
```
- 이벤트 객체를 전달받으려면 이벤트 핸들러를 정의할 때 이벤트 객체를 전달받을 매개변수를 명시적으로 선언해야 한다.
- 이벤트 핸들러 어트리뷰트 방식의 경우 이벤트 객체를 전달받으려면 이벤트 핸들러의 첫 번째 매개변수 이름이 반드시 event이어야 한다.

### 이벤트 전파

- DOM 트리 상에 존재하는 DOM 요소 노드에서 발생한 이벤트는 DOM 트리를 통해 전파된다.
- 이를 이벤트 전파라고 한다.
- 생성된 이벤트 객체는 이벤트를 발생시킨 DOM 요소인 이벤트 타깃을 중심으로 DOM 트리를 통해 전파된다.
- 이벤트 전파는 이벤트 객체가 전파되는 방향에 따라 다음과 같이 3단계로 구분할 수 있다.
  - 캡처링 단계: 이벤트가 상위 요소에서 하위 요소 방향으로 전파
  - 타깃 단계: 이벤트가 이벤트 타깃에 도달
  - 버블링 단계: 이벤트가 하위 요소에서 상위 요소 방향으로 전파
```html
<!DOCTYPE html>
<html>
<body>
    <ul id="fruits">
        <li id="apple">Apple</li>
        <li id="banana">Banana</li>
        <li id="orange">Orange</li>
    </ul>
<script>
    const $fruits = document.getElmentById('fruits');
    $fruits.addEventListener('click',e=>{
        console.log(`이벤트 단계: ${e.eventPhase}`); // 3: 버블링 단계
        console.log(`이벤트 타깃: ${e.target}`); // [object HTMLLIElement]
        console.log(`커런트 타깃: ${e.currentTarget}`); // [object HTMLULListElement]
    })
</script>
</body>
</html>
```
- li 요소를 클릭하면 클릭 이벤트가 발생하여 클릭 이벤트 객체가 생성되고 클릭된 li 요소가 이벤트 타깃이 된다.
- 이때 클릭 이벤트 객체는 window에서 시작해서 이벤트 타깃 방향으로 전파된다. 이것이 캡처링 단계다.
- 이후 이벤트 객체는 이벤트를 발생시킨 이벤트 타깃에 도달한다. 이것이 타겟 단계다.
- 이후 이벤트 객체는 이벤트 타깃에서 시작해서 window 방향으로 전파된다. 이것이 버블링 단계다.
- 이벤트 핸들러 어트리뷰트/프로퍼티 방식으로 등록한 이벤트 핸들러는 타깃 단계와 버블링 단계의 이벤트만 캐치할 수 있다.
- 하지만 addEventListner 메서드 방식으로 등록한 이벤트 핸들러는 타깃 단계와 버블링 단계뿐만 아니라 캡처링 단계의 이벤트도 선별적으로 캐치할 수 있다.
  - 3번째 인수로 true를 전달할 때
- 이처럼 이벤트는 이벤트를 발생시킨 이벤트 타깃은 물론 상위 DOM 요소에서도 캐치할 수 있다.

### 이벤트 위임

- 이벤트 위임은 여러 개의 하위 DOM 요소에 각각 이벤트 핸들러를 등록하는 대신 하나의 상위 DOM 요소에 이벤트 핸들러를 등록하는 방법을 말한다.
- 이벤트는 이벤트 타깃은 물론 상위 DOM 요소에서도 캐치할 수 있다.
- 이벤트 위임을 통해 상위 DOM 요소에 이벤트 핸들러를 등록하면 여러 개의 하위 DOM 요소에 이벤트 핸들러를 등록할 필요가 없다.
- 또한 동적으로 하위 DOM 요소를 추가하더라도 일일이 추가된 DOM 요소에 이벤트 핸들러를 등록할 필요가 없다.
- 주의할 점은 상위 요소에 이벤트 핸들러를 등록하기 때문에 이벤트 타깃, 즉 이벤트를 실제로 발생시킨 DOM 요소가 개발자가 기대한 DOM 요소가 아닐 수도 있다는 것이다.

### DOM 요소의 기본 동작 조작

- 이벤트 객체의 preventDefault 메서드는 DOM 요소의 기본 동작을 중단시킨다.
- 이벤트 객체의 stopPropagation 메서드는 이벤트 전파를 중지시킨다.
- stopPropagation 메서드는 하위 DOM 요소의 이벤트를 개별적으로 처리하기 위해 이벤트의 전파를 중단시킨다.

### 이벤트 핸들러 내부의 this

- 이벤트 핸들러 어트리뷰트 방식
    ```html
    <body>
        <button onClick="handleClick()">Click me</button>
        <script>
            function handleClick(){
                console.log(this); // window
            }
        </script>
    </body>
    ```
    - 일반 함수로서 호출되는 함수 내부의 this는 전역 객체를 가리키므로 handleClick 함수 내부의 this는 전역 객체 window를 가리킨다.
    - 단, 이벤트 핸들러를 호출할 때 인수로 전달한 this는 이벤트를 바인딩한 DOM 요소를 가리킨다.
    ```html
    <body>
        <button onClick="handleClick(this)">Click me</button>
        <script>
            function handleClick(button){
                console.log(button); // 이벤트를 바인딩한 button 요소
                console.log(this); // window
            }
        </script>
    </body>`
    ```
- 이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식
    - 이벤트 핸들러 프로퍼티 방식과 addEventListener 메서드 방식 모두 이벤트 핸들러 내부의 this는 이벤트를 바인딩한 DOM 요소를 가리킨다.
    - 즉, 이벤트 핸들러 내부의 this는 이벤트 객체의 currentTarget 프로퍼티와 같다.

