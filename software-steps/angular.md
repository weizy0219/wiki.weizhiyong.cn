---
title: Angular
description: angular相关技术
published: true
date: 2021-02-03T14:26:30.441Z
tags: 
editor: undefined
dateCreated: 2021-02-03T14:26:25.055Z
---

# Angular

## Angular 双向绑定前提

要在模块中引入对应包。
```typescript
import { FormsModule }   from '@angular/forms';
```

## Angular 数组遍历项进行双向绑定时丢失焦点的问题
解决思路，增加`trackBy`函数。
在`html`文件中增加
```html
*ngFor="let value of values; trackBy:indexTracker"
```
在`ts`文件中增加
```typescript
indexTracker(index: number, value: any) {
    return index;
}
```