---
title: vant按需引入无法引入Toast的样式
published: 2024-07-21
description: ''
image: ''
tags: [各类问题, vant]
category: '各类问题'
draft: false 

---







+ 使用`vant`时，若配置按需引入样式，某些组件的样式无法引入，如`Toast`，可以单独在`main.ts`中引入，具体如下：

```typescript
import 'vant/es/toast/style'
```

