---
layout: post
title:  "Typescript Class Interface"
date:   2022-05-21 00:00:00 +0800
categories: Typescript
---

## Class Interface

### `private` `public` `protect`

1. 默认为 `public`
2. 当成员被标记成 `private时`，它就不能在声明它的类的外部访问
3. `protected`修饰符与`private`修饰符的行为很相似，但有一点不同， `protected`成员在派生类中仍然可以访问 (继承)

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

```typescript

class Department {
  private employees: string[] = [];

  constructor(private readonly id: string, public name: string) {
  }

  describe(this: Department) {
    console.log(`Department (${this.id}): ${this.name}`);
  }

  addEmployee(employee: string) {
    this.employees.push(employee);
  }

  printEmployeeInformation() {
    console.log(this.employees.length);
    console.log(this.employees);
  }
}

class ITDepartment extends Department {
  admins: string[];
  constructor(id: string, admins: string[]) {
    super(id, 'IT');
    this.admins = admins;
  }
}

class AccountingDepartment extends Department {
  constructor(id: string, private reports: string[]) {
    super(id, 'Accounting');
  }

  addReport(text: string) {
    this.reports.push(text);
  }

  printReports() {
    console.log(this.reports);
  }
}

const it = new ITDepartment('d1', ['Max']);

it.addEmployee('Max');
it.addEmployee('Manu');

// it.employees[2] = 'Anna';

it.describe();
it.name = 'NEW NAME';
it.printEmployeeInformation();

console.log(it);

const accounting = new AccountingDepartment('d2', []);

accounting.addReport('Something went wrong...');

accounting.printReports();

// const accountingCopy = { name: 'DUMMY', describe: accounting.describe };

// accountingCopy.describe();


```

### `setter` `getter`

```typescript


let passcode = "secret passcode";

class Employee {
    private _fullName: string;

    get fullName(): string {
        return this._fullName;
    }

    set fullName(newName: string) {
        this._fullName = newName;
    }
}

let employee = new Employee();
employee.fullName = "Bob Smith";

const fullname=employee.fullName

console.log(fullname);

```
