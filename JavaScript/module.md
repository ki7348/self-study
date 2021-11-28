# JavaScript - Module

## 설명

모듈이란 애플리케이션을 구성하는 개별적 요소로서 재시용 가능한 코드 조각을 말합니다.
모듈이 성립하려면 모듈은 자신만의 파일 스코프를 가질 수 있어야 합니다.
자신만의 파일 스코프를 갖는 모듈의 모든 자산은 캡슐화되어 다른 모듈에서 접근할 수 없습니다.
모듈은 공개가 필요한 자산에 한정하여 명시적으로 선택적 공개가 가능하고 이를 export라 합니다.
모듈이 공개한 자산 중 일부 또는 전체를 선택해 자신의 스코프 내로 불러들여 재사용할 수 있고 이를 import라 합니다.

### 모듈화의 장점

- 코드의 단위를 명확히 분리하여 애플리케이션을 구성할 수 있고 재사용성이 좋아서 개발 효율성과 유지보수성을 높일 수 있습니다.

### 자바스크립트와 모듈

- 자바스크립트는 파일마다 독립적인 파일 스코프를 갖지 않습니다.
  - 자바스크립트 파일을 여러 개의 파일로 분리하여 script 태그로 로드해도 분리된 자바스크립트 파일들은 결국 하나의 자바스크립트 파일 내에 있는 것처럼 동작합니다.
    - 즉 모든 자바스크립트 파일은 하나의 전역을 공유합니다.
        - 분리된 자바스크립트 파일들의 전역 변수가 중복되는 등의 문제가 발생할 수 있습니다.
- 자바스크립트 모듈 시스템은 CommonJS 또는 AMD 진영으로 나뉘게 되었고 Node.js는 CommonJS를 채택했습니다.
  - Node.js는 모듈시스템을 지원하므로 파일별로 독립적인 파일 스코프를 가집니다.

### ES6 모듈(ESM)

- ES6에서는 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능을 추가했습니다.
- ESM은 독자적인 모듈 스코프를 가집니다.
- 모듈 내에서 var로 선언한 변수는 더는 전역 변수가 아니며 window 객체의 프로퍼티도 아닙니다.

### export 키워드

- 모듈 내부에서 선언한 모든 식별자는 기본적으로 해당 모듈 내부에서만 참조할 수 있으므로 선언한 식별자를 외부에 공개하여 다른 모듈들이 재사용할 수 있게 하려면 export 키워드를 사용해야 합니다.
- 모듈에서 하나의 값만 export한다면 default키워드를 사용할 수 있습니다.

### import 키워드

- 다른 모듈에서 공개한 식별자를 자신의 모듈 스코프 내부로 로드하려면 import 키워드를 사용합니다.