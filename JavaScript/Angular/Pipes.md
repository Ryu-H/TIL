# Pipes

Component의 property들이 항상 우리가 UI에 렌더링 하고자 하는 형태가 아닐 경우가 있다. 이럴 때 template에서 Pipe를 통해 우리가 원하는 형식으로 바꿔줄 수 있다. | 이후에 Pipe name, 추가로 들어갈 argument들은 colon으로 구분해 준다.

e.g.
- `{{ product.productName | lowercase }}`
- `{{ product.price | currency:'USD':'1.2-2' }}` - 마지막 argument는 "소수점 앞에 최소 1자리 표시. 소수점 뒤로 최소 2자리, 최대 2자리 표시"라는 의미.

## Built-in Pipes for angular

lowercase, currency 등등

## Custom Pipes

**PipeTransform** 인터페이스를 구현하는 클래스로 Custom Pipe을 만들 수 있다.

- 클래스는 Pipe로 데코레이트 해주고 그 데코레이트의 아규먼트로 넣은 오브젝트의 name이 템플레이트에서 사용하는 pipe의 이름이 된다.
- Pipe와 PipeTransform 둘다 @angular/core에 있다
- 구현한 Custom Pipe를 사용하고자 하는 Component가 들어있는 Module의 데코레이터에 declarations으로 포함돼 있어야 한다.

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {
    transform(value: string, character: string): string {
        return value.replace(character, ' ');
    }
}
```
