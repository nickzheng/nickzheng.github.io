---
layout: post
title:  "React useCallback, useMemo"
date:   2022-03-06 14:00:48 +0800
categories: React
---

### `useCallback` `useMemo` `Memo`

1. `useCallback` 用来缓存一个函数

https://www.w3schools.com/react/react_usecallback.asp


```jsx

const memoizedCallback = useCallback(() => {
    doSomething(a, b);
}, [a, b]);
```



1. `useMemo` vue computed

https://www.w3schools.com/react/react_usememo.asp

`const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);`

```jsx
import React, { useMemo, useState } from "react";

export default () => {
    const [value, setValue] = useState(0);
    const [value2, setValue2] = useState(0);

    const doubleValue = useMemo(() => {
        console.log("useMemo triggered");
        return value * 2;
    }, [value]);

    return (
        <div>
            <div>value1: {value}</div>
            <div>doubleValue: {doubleValue}</div>
            <button onClick={() => setValue(value + 1)}>value +1</button>
            <div>value2: {value2}</div>
            <button onClick={() => setValue2(value2 + 1)}>value2 +1</button>
        </div>
    );
};
```


