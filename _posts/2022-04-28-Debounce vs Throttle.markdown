---
layout: post
title:  "Debounce vs Throttle"
date:   2022-04-28 00:37:48 +0800
categories: jekyll update
---

![img.png](/assets/img.png)

1. Debounce 在一定时间内只响应最后一次触发的事件

```html
<!DOCTYPE html>
<html lang="en">
<body>
<button id="btn">click</button>
</body>

<script>
    function debounce(fn, delay) {
        let timer
        return function (...args) {
            if (timer) clearTimeout(timer)
            timer = setTimeout(() => fn.apply(this, args), delay)
        }
    }
    document.getElementById('btn').addEventListener('click', debounce(function () {
        console.log('1111')
    }, 1000))
</script>

</html>
```

2. Throttle 在一定时间内只响应第一次触发的事件

```html
<!DOCTYPE html>
<html lang="en">
<body>
<button id="btn">click</button>
</body>

<script>
    function throttle(fn, wait) {
        let timerId = null;
        return function() {
            if (timerId == null) {
                fn();
                timerId = setTimeout(() => {
                    timerId = null;
                }, wait);
            }
        };
    }
    document.getElementById('btn').addEventListener('click', throttle(function () {
        console.log('1111')
    }, 1000))
</script>

</html>
```
