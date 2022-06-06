---
layout: post
title:  "Typescript Decorators"
date:   2022-05-22 00:00:00 +0800
categories: Typescript
---

## Decorators


1. 多个 `Decorators` 执行顺序

```typescript

function Logger(logString: string) {
    console.log('1. LOGGER FACTORY');
    return function(constructor: Function) {
        console.log(`4. Logger decorator ${logString}`);
        console.log(constructor);
    };
}

function WithTemplate(template: string, hookId: string) {
    console.log('2. TEMPLATE FACTORY');
    return function(constructor: any) {
        console.log('3. WithTemplatedecorator');
        const hookEl = document.getElementById(hookId);
        const p = new constructor();
        if (hookEl) {
            hookEl.innerHTML = template;
            hookEl.querySelector('h1')!.textContent = p.name;
        }
    }
}

@Logger('LOGGING')
@WithTemplate('<h1>My Person Object</h1>', 'app')
class Person {
    name = 'Max';

    constructor() {
        console.log('Creating person object...');
    }
}

const pers = new Person();

// [LOG]: "1. LOGGER FACTORY"

// [LOG]: "2. TEMPLATE FACTORY"

// [LOG]: "3. WithTemplatedecorator"

// [LOG]: "Creating person object..."

// [LOG]: "4. Logger decorator LOGGING"

// [LOG]: class Person {
//     constructor() {
//         this.name = 'Max';
//         console.log('Creating person object...');
//     }
// }

// [LOG]: "Creating person object..."
```


2. `Decorators` 作用在 `Property` `Accessor` `Method` `Parameter` `Class`

```typescript

function PropertyDecorator(target: any, name: string | symbol) {
    console.log('-------------------Property decorator---------------------');
    console.log('target', target); // target {}
    console.log('propertyName', name); // name title
    console.log('-------------------Property decorator---------------------\n\n\n');
}

function AccessorDecorator(target: any, name: string, descriptor: PropertyDescriptor) {
    console.log('-------------------Accessor decorator---------------------');
    console.log('target', target); // target {}
    console.log('name', name); // name price
    console.log('descriptor', descriptor);
    // descriptor {
    //   get: undefined,
    //   set: [Function: set price],
    //   enumerable: false,
    //   configurable: true
    // }
    console.log('-------------------Accessor decorator---------------------\n\n\n');
}

function MethodDecorator(target: any, name: string | symbol, descriptor: PropertyDescriptor) {
    console.log('-------------------Method decorator---------------------');
    console.log('target', target); // target {}
    console.log('name', name); // name getPriceWithTax
    console.log('descriptor', descriptor);
    // descriptor {
    //   value: [Function: getPriceWithTax],
    //   writable: true,
    //   enumerable: false,
    //   configurable: true
    // }
    const method = descriptor.value;
    descriptor.value = function (...args) {
        console.log('args', args);
        return method.apply(this, args);
    };
    console.log('-------------------Method decorator---------------------\n\n\n');
}

function ParameterDecorator(target: any, name: string | symbol, position: number) {
    console.log('-------------------Parameter decorator---------------------');
    console.log('target', target); // target {}
    console.log('name', name); // name getPriceWithTax
    console.log('position', position); // position 0
    console.log('-------------------Parameter decorator---------------------\n\n\n');
}

function ClassDecorator(target) {
    console.log('-------------------Class decorator---------------------');
    console.log('target', target); // target [class Product]
    console.log('-------------------Class decorator---------------------\n\n\n');
    return class extends target {
        constructor() {
            console.log('arguments', arguments);
            super(...arguments);
        }
    };
}

// @ts-ignore
@ClassDecorator
class Product {
    @PropertyDecorator
    title: string;
    private _price: number;

    @AccessorDecorator
    set price(val: number) {
        if (val > 0) {
            this._price = val;
        } else {
            throw new Error('Invalid price - should be positive!');
        }
    }

    constructor(t: string, p: number) {
        this.title = t;
        this._price = p;
    }

    @MethodDecorator
    getPriceWithTax(@ParameterDecorator tax: number) {
        return this._price * (1 + tax);
    }
}
const p1 = new Product('Book', 20);

const finallyPrice = p1.getPriceWithTax(0.1);

console.log('finallyPrice', finallyPrice);

```


3. validator 通过 把`[target.constructor.name` `propName` 加到global `registeredValidators` 里面

```typescript

const registeredValidators = {};

function Required(target: any, propName: string) {
  registeredValidators[target.constructor.name] = {
    ...registeredValidators[target.constructor.name],
    [propName]: ['required'],
  };
}

function PositiveNumber(target: any, propName: string) {
  registeredValidators[target.constructor.name] = {
    ...registeredValidators[target.constructor.name],
    [propName]: ['positive'],
  };
}

function validate(obj: any) {
  const objValidatorConfig = registeredValidators[obj.constructor.name];
  if (!objValidatorConfig) {
    return true;
  }
  let isValid = true;
  for (const prop in objValidatorConfig) {
    for (const validator of objValidatorConfig[prop]) {
      switch (validator) {
        case 'required':
          isValid = isValid && !!obj[prop];
          break;
        case 'positive':
          isValid = isValid && obj[prop] > 0;
          break;
      }
    }
  }
  return isValid;
}

class Course {
  @Required
  title: string;
  @PositiveNumber
  price: number;

  constructor(t: string, p: number) {
    this.title = t;
    this.price = p;
  }
}

const createdCourse = new Course('title', 1);

const result = validate(createdCourse);

console.log('result', result);

const createdCourse2 = new Course('', -1);

const result2 = validate(createdCourse2);

console.log('result2', result2);


```
