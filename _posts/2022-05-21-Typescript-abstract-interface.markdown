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
