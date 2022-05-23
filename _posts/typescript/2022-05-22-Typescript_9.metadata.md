---
layout: post
title:  "Typescript Metadata"
date:   2022-05-22 00:00:00 +0800
categories: Typescript
---

### metadata

[https://jkchao.github.io/typescript-book-chinese/tips/metadata.html#%E5%9F%BA%E7%A1%80](https://jkchao.github.io/typescript-book-chinese/tips/metadata.html#%E5%9F%BA%E7%A1%80)



1. basic

```typescript

function metadata(
  metadataKey: any,
  metadataValue: any
): {
  (target: Function): void;
  (target: Object, propertyKey: string | symbol): void;
};

```

```typescript

@Reflect.metadata('inClass', 'A')
class Test {
  @Reflect.metadata('inMethod', 'B')
  public hello(): string {
    return 'hello world';
  }
}

console.log(Reflect.getMetadata('inClass', Test)); // 'A'
console.log(Reflect.getMetadata('inMethod', new Test(), 'hello')); // 'B'

```

2. 自定义 metadataKey

````typescript

function classDecorator(): ClassDecorator {
  return target => {
    // 在类上定义元数据，key 为 `classMetaData`，value 为 `a`
    Reflect.defineMetadata('classMetaData', 'a', target);
  };
}

function methodDecorator(): MethodDecorator {
  return (target, key, descriptor) => {
    // 在类的原型属性 'someMethod' 上定义元数据，key 为 `methodMetaData`，value 为 `b`
    Reflect.defineMetadata('methodMetaData', 'b', target, key);
  };
}

@classDecorator()
class SomeClass {
  @methodDecorator()
  someMethod() {}
}

Reflect.getMetadata('classMetaData', SomeClass); // 'a'
Reflect.getMetadata('methodMetaData', new SomeClass(), 'someMethod'); // 'b'

````
