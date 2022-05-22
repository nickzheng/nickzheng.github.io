---
layout: post
title:  "Typescript Types"
date:   2022-05-18 00:00:00 +0800
categories: Typescript
---

## Operations


1. ??

```typescript

const fetchedUserData = {
    id: 'u1',
    name: 'Max',
    job: {title: 'CEO', description: 'My own company'}
};

console.log(fetchedUserData?.job?.title);

const userInput = undefined;

const storedData = userInput ?? 'DEFAULT';

console.log(storedData);





```

2. ! as

```typescript

const userInputElement = document.getElementById('user-input')! as HTMLInputElement;
userInputElement.value = '111';

```
