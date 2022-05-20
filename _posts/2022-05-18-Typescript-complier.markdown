---
layout: post
title:  "Typescript Compiler"
date:   2022-05-18 00:00:00 +0800
categories: jekyll update
---

## Compiler


### Compile the entire Project

- `tsc --init`
- `tsc -w`

### Including & Excluding Files

https://www.tslang.cn/docs/handbook/tsconfig-json.html

1. 不带任何输入文件的情况下调用tsc，编译器会从当前目录开始去查找tsconfig.json文件，逐级向上搜索父目录。

2. 使用`include`和`exclude`属性

"include"和"exclude"属性指定一个文件glob匹配模式列表

- * 匹配0或多个字符（不包括目录分隔符）
- ? 匹配一个任意字符（不包括目录分隔符）
- **/ 递归匹配任意子目录

```json
{
    "include": [
        "src/**/*"
    ],
        "exclude": [
        "node_modules",
        "**/*.spec.ts"
    ]
}
```

如果`files`和`include`都没有被指定，编译器默认包含当前目录和子目录下所有的TypeScript文件（`.ts`, `.d.ts` 和 `.tsx`)
`exclude`默认情况下会排除 `node_modules`，`bower_components`， `jspm_packages` 和 `<outDir>` 目录

3. `target` 生成目标javascript 版本, 指定ECMAScript目标版本 `ES3`（默认）， `ES5`， `ES6`/ `ES2015`， `ES2016`， `ES2017` 或 `ESNext`。

4. `lib` 编译过程中需要引入的库文件的列表。

注意：如果--lib没有指定默认注入的库的列表。默认注入的库为：
► 针对于--target `ES5：DOM，ES5，ScriptHost`
► 针对于--target `ES6：DOM，ES6，DOM.Iterable，ScriptHost`

5. `allowJs` 允许编译.js结尾的文件 

6. `checkJs` 在 .js文件中报告错误。与 `--allowJs`配合使用。

7. `declaration` 生成相应的 .d.ts文件。

8. `sourceMap`

9. `outDir` 输出目录

10. `rootDir`
在 `outDir`: `./dest` 配置情况下，`src/index.ts` 编译后输出位置为 `dest/src/index.js`

输出目录带上了的 `src` 这一层，显然不是那么合理。

解决办法是指定 rootDir: “src”。这样，根目录变成了 src，编译后输出则没有了 src 这一层。


12. `removeComments` 删除所有注释

13. `emitDecoratorMetadata` 给源码里的装饰器声明加上设计类型元数据

14. `experimentalDecorators` 启用实验性的ES装饰器

15. `skipLibCheck` 忽略所有的声明文件（ *.d.ts）的类型检查

16. `noEmitOnError` 报错时不生成输出文件

17. `strict`

启用所有严格类型检查选项。
启用 --strict相当于启用
```bash
--noImplicitAny
--noImplicitThis
--alwaysStrict
--strictNullChecks
-strictFunctionTypes // 禁用函数参数双向协变检查。
--strictPropertyInitialization。
```
