---
layout: post
title:  "Typescript Class Interface"
date:   2022-05-21 00:00:00 +0800
categories: jekyll update
---

## Class Interface

### `private` `public`

1. 默认为 `public`
2. 当成员被标记成 `private时`，它就不能在声明它的类的外部访问
3. `protected`修饰符与 `private`修饰符的行为很相似，但有一点不同， `protected`成员在派生类中仍然可以访问

```typescript

class Department {
    name: string;
    private employees: string [] = [];

    constructor(n: string) {
        this.name = n;
    }

    describe() {
        console.log('Department' + this.name)
    }

    addEmployee(employee: string) {
        this.employees.push(employee);
    }


    printEmployeeInfo() {
        console.log('this.employees.length', this.employees.length);
        console.log('this.employees', this.employees);
    }

}

const accounting = new Department('Accounting')

console.log('accounting', accounting);

accounting.describe();

accounting.addEmployee('1')
accounting.addEmployee('2')
accounting.printEmployeeInfo();

accounting.employees[2] = '3' // error


```

### `Shorthand Init`

```typescript

class Department {
  // private id: string;
  // private name: string;

  constructor(private id: string, public name: string) {
    // this.id = id;
    // this.name = n;
  }

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }
}

const accounting = new Department('d1', 'Accounting');


```


### `readonly`

```typescript

class Octopus {
    readonly name: string;

    constructor(theName: string) {
        this.name = theName;
    }

    change() {
        this.name = '423424234'; // error
    }
}

let dad = new Octopus("Man with the 8 strong legs");


```

### Inheritance


### `protect`

