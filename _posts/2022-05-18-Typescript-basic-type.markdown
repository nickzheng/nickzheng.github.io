---
layout: post
title:  "Typescript Types"
date:   2022-05-18 00:00:00 +0800
categories: jekyll update
---

## Typescript

### Tuple

```js
const employee: [number, string] = [1, "Steve"];
const person: [number, string, boolean] = [1, "Steve", true];
```

### Enum

```typescript

enum E1 { 
    X,
    Y, 
    Z 
}
// X 0
// Y 1
// Z 2

enum E2 {
    A = 1,
    B,
    C,
}
// A 1
// X 2
// C 3
```


### Union

```typescript
const combine = (input1: number| string, input2: number|string) =>{ }
```

### Literal

```typescript

type Easing = "ease-in" | "ease-out" | "ease-in-out";
 
class UIElement {
  animate(dx: number, dy: number, easing: Easing) {
    if (easing === "ease-in") {
      // ...
    } else if (easing === "ease-out") {
    } else if (easing === "ease-in-out") {
    } else {
      // It's possible that someone could reach this
      // by ignoring your types though.
    }
  }
}
 
let button = new UIElement();
button.animate(0, 0, "ease-in");
button.animate(0, 0, "uneasy"); // error


```


```typescript

interface MapConfig {
  lng: number;
  lat: number;
  tileSize: 8 | 16 | 32;
}
 
setupMap({ lng: -73.935242, lat: 40.73061, tileSize: 16 });

```


### `any` vs `unknown`

https://www.bilibili.com/video/BV1WR4y1P7dw

1. `any` 不在乎他的类型
2. `unknown` 不知道他的类型


```typescript
let value: unknown;
value.foo.var; // error
value.trim(); // error
value(); // error
```

```typescript
let value: any;
value.foo.var; // success
value.trim(); // success
value(); // success
```

### `never`

`void` 表示没有任何类型
`never` 表示永远不存在的值的类型。

当一个函数永不返回时（或者总是抛出错误），它的返回值为 never 类型

```typescript
function foo(x: string | number): boolean {
  if (typeof x === 'string') {
    return true;
  } else if (typeof x === 'number') {
    return false;
  }

  // 如果不是一个 never 类型，这会报错：
  // - 不是所有条件都有返回值 （严格模式下）
  // - 或者检查到无法访问的代码
  // 但是由于 TypeScript 理解 `fail` 函数返回为 `never` 类型
  // 它可以让你调用它，因为你可能会在运行时用它来做安全或者详细的检查。
  return fail('Unexhaustive');
}

function fail(message: string): never {
  throw new Error(message);
}
```
