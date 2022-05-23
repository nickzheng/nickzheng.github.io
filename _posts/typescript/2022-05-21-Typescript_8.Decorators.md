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


