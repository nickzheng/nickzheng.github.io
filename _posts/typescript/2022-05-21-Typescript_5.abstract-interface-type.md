---
layout: post
title:  "Typescript Class abstract & interface"
date:   2022-05-21 00:00:00 +0800
categories: Typescript
---

## abstract

```typescript

abstract class Department {
    constructor(public name:string) {
    }
    printName(){
        console.log('this.name', this.name);
    }

    abstract printMeeting();
}


class AccountingDepartment extends Department {

    constructor() {
        super('Accounting and Auditing');
    }

    printMeeting(): void {
        console.log('The Accounting Department meets each Monday at 10am.');
    }
}

let department: Department; // 允许创建一个对抽象类型的引用
department = new Department(); // error 错误: 不能创建一个抽象类的实例
department = new AccountingDepartment(); // 允许对一个抽象子类进行实例化和赋值
department.printName();
department.printMeeting();


```


## interface

1. implement
2. index property

```typescript

interface ErrorContainer {
  [prop: string]: string;
}

const errorBag: ErrorContainer = {
  email: 'Not a valid email!',
  username: 'Must start with a capital character!'
};

```

## type 类型别名 vs Interface

https://www.bilibili.com/read/cv16600117?from=note


1. Objects / Functions

```typescript

interface Point {
  x: number;
  y: number;
}

interface SetPoint {
  (x: number, y: number): void;
}
```

```typescript
type Point = {
  x: number;
  y: number;
};

type SetPoint = (x: number, y: number) => void;
```

2. 联合类型, 交叉类型（Intersection Types） 使用 Types

```typescript
// primitive
type Name = string;

// object
type PartialPointX = { x: number; };
type PartialPointY = { y: number; };

// union
type PartialPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];

```


```typescript

type Admin = {
    name: string;
    privileges: string[];
};

type Employee = {
    name: string;
    startDate: Date;
};

type ElevatedEmployee = Admin & Employee;

const e1: ElevatedEmployee = {
    name: 'Max',
    privileges: ['create-server'],
    startDate: new Date()
};


// more examples
type Combinable = string | number;
type Numeric = number | boolean;

type Universal = Combinable & Numeric;

```


3. merge属性

```typescript
// 同名的 interface 会自动合并，而 type 不会

interface Person {
    name: string;
}

interface Person {
    age: number;
}

let user: Person ={
    name: 'nick',
    age: 34,
}

////////////////////////////


type User ={
    name: string;

}
type User ={ // error
    age: number; 
}

```

![img.png](/assets/interface_vs_type.png)

