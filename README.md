# Everyday Types

##  원시 타입 : string, number, 그리고 boolean

- `string`은 "Hello, world"와 같은 문자열 값을 나타냅니다
- `number`은 42와 같은 숫자를 나타냅니다. JavaScript는 정수를 위한 런타임 값을 별도로 가지지 않으므로, int 또는 float과 같은 것은 존재하지 않습니다. 모든 수는 단순히 number입니다
- `boolean`은 true와 false라는 두 가지 값만을 가집니다
---
## Array

[1, 2, 3]과 같은 배열의 타입을 지정할 때 `number[]` 구문을 사용할 수 있습니다. 이 구문은 모든 타입에서 사용할 수 있습니다(예를 들어, `string[]`은 문자열의 배열입니다). 위 타입은 `Array<number>`와 같은 형태로 적을 수 있으며, 동일한 의미를 가집니다.

---
## Any

TypeScript는 또한 `any`라고 불리는 특별한 타입을 가지고 있으며, 특정 값으로 인하여 타입 검사 오류가 발생하는 것을 원하지 않을 때 사용할 수 있습니다.

어떤 값의 타입이 `any`이면, 해당 값에 대하여 임의의 속성에 접근할 수 있고(이때 반환되는 값의 타입도 any입니다), 함수인 것처럼 호출할 수 있고, 다른 임의 타입의 값에 할당하거나(받거나), 그 밖에도 구문적으로 유효한 것이라면 무엇이든 할 수 있습니다.

```javascript
let obj: any = { x: 0 };
// 아래 이어지는 코드들은 모두 오류 없이 정상적으로 실행됩니다.
// `any`를 사용하면 추가적인 타입 검사가 비활성화되며,
// 당신이 TypeScript보다 상황을 더 잘 이해하고 있다고 가정합니다.
obj.foo();
obj();
obj.bar = 100;
obj = "hello";
const n: number = obj;
```
---
## Type

```typescript
type Point = {
  x: number;
  y: number;
};
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

타입 별칭을 사용하면 단지 객체 타입뿐이 아닌 모든 타입에 대하여 새로운 이름을 부여할 수 있습니다. 예를 들어, 아래와 같이 유니언 타입에 대하여 타입 별칭을 부여할 수도 있습니다.

```typescript
type ID = number | string;
```
---
## Interface

_인터페이스 선언_은 객체 타입을 만드는 또 다른 방법입니다.

```typescript
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
```

타입 별칭을 사용한 경우와 마찬가지로, 위 예시 코드는 마치 타입이 없는 임의의 익명 객체를 사용하는 것처럼 동작합니다. TypeScript는 오직 printCoord에 전달된 값의 _구조_에만 관심을 가집니다. 즉, 예측된 프로퍼티를 가졌는지 여부만을 따집니다. 이처럼, 타입이 가지는 구조와 능력에만 관심을 가진다는 점은 TypeScript가 구조적 타입 시스템이라고 불리는 이유입니다.

타입 별칭과 인터페이스의 차이점
타입 별칭과 인터페이스는 매우 유사하며, 대부분의 경우 둘 중 하나를 자유롭게 선택하여 사용할 수 있습니다. `interface`가 가지는 대부분의 기능은 `type`에서도 동일하게 사용 가능합니다. 이 둘의 가장 핵심적인 차이는, 타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다는 점입니다.