---
layout: post
title:  "Typescript Singleton"
date:   2022-05-21 00:00:00 +0800
categories: Typescript
---

## Singleton


```typescript

class Singleton {
    private static instance;

    private constructor() { }

    public static getInstance() {
        if (!this.instance) {
            this.instance = new Singleton();
        }
        return this.instance;
    }
    
    public someBusinessLogic() {
        // ...
    }
}

const s1 = Singleton.getInstance();
const s2 = Singleton.getInstance();

if (s1 === s2) {
    console.log('Singleton works, both variables contain the same instance.');
} else {
    console.log('Singleton failed, variables contain different instances.');
}


```
