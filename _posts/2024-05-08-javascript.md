---
title: Javascrpit
author: Jaeuk
date: 2024-05-08
category: Jekyll
layout: post
configuration in `_config.yml`:

---



CallbackFunction
-------------
함수가 다른 함수의 파라미터로 전달되어 호출

```javascript
const words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`]

const result = words.filter(word => word.length > 6);
//expected output: Array ["exuberant", "destruction", "present"]
```


