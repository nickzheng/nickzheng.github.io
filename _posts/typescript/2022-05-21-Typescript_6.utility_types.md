---
layout: post
title:  "Typescript Utility Types"
date:   2022-05-21 00:00:00 +0800
categories: Typescript
---


## Utility Types

https://www.typescriptlang.org/docs/handbook/utility-types.html


1. `Partial<Type>` 把所以变量变成 optional
![Partial.png](/assets/Partial.png)

```typescript

interface Todo {
    title: string;
    description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
    return {...todo, ...fieldsToUpdate};
}

const todo1 = {
    title: "organize desk",
    description: "clear clutter",
};

const todo2 = updateTodo(todo1, {description: "throw out trash"});


```

2. `Required<Type>` 把所以变量变成 required

![Required.png](/assets/Required.png)

3. `Readonly<Type>` 把所以变量变成 Readonly

![Readonly.png](/assets/Readonly.png)


4. `Record<Keys, Type>`

```typescript

interface CatInfo {
  age: number;
  breed: string;
}
 
type CatName = "miffy" | "boris" | "mordred";
 
const cats: Record<CatName, CatInfo> = {
  miffy: { age: 10, breed: "Persian" },
  boris: { age: 5, breed: "Maine Coon" },
  mordred: { age: 16, breed: "British Shorthair" },
};
 
cats.boris;

```

5. `Pick<Type, Keys>` 选取需要的keys

![Pick.png](/assets/Pick.png)

```typescript

interface Todo {
    title: string;
    description: string;
    completed: boolean;
}

type TodoPreview = Pick<Todo, "title" | "completed">;

const todo: TodoPreview = {
    title: "Clean room",
    completed: false,
};

console.log('todo', todo);

```

6. `Omit<Type, Keys>` 选取需要的keys

![Omit.png](/assets/Omit.png)

```typescript

interface Todo {
    title: string;
    description: string;
    completed: boolean;
    createdAt: number;
}

type TodoInfo = Omit<Todo, "completed" | "createdAt">;

const todoInfo: TodoInfo = {
    title: "Pick up kids",
    description: "Kindergarten closes at 5pm",
};
```

