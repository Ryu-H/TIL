# Lifecycle Hooks

Angular에선 Component가 생성, 렌더링, 폐기되는 수명주기가 있고 Component가 관련된 Interface를 구현하게 함으로써 특정 주기에 어떤 동작을 수행하도록 할 수 있다.

```typescript
import { Component, OnInit } from '@angular/core';

export class ProductListComponent implements OnInit {

  // ...

  ngOninit(): void {
    console.log('In OnInit');
  }
}
```

실제로는 `implements OnInit` 부분은 필수는 아니라고 한다. 어차피 JavaScript 내부적으로는 인터페이스의 개념이 아직까진 없기 때문에 TypeScript에서 트랜스파일 될 때 저 부분은 사라진다. 그러나 이러한 유형의 것들이 늘 그렇듯 비록 동작할 때는 필수가 아니더라도 명시적으로 표기하는 것이 좋은 습관이 되겠다.
