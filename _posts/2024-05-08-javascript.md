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
const words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];

const result = words.filter(word => word.length > 6);
//expected output: Array ["exuberant", "destruction", "present"]
```

```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];
function callback(element){
  return element.length > 6;
};
newWords = words.filter(callback);
//expected output: Array ["exuberant", "destruction", "present"]
```
Anonymous function
```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];

newWords = words.filter(function callback(element){
  return element.length > 6;
};);
//expected output: Array ["exuberant", "destruction", "present"]
```
Arrow function
```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];

newWords = words.filter(element =>element.length > 6);
//expected output: Array ["exuberant", "destruction", "present"]
```
함수 만들기
```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];
//newWords = words.filter(element =>element.length > 6);
function myfilter(origin, callback) {
    var result = [];
    for(var i=0; i<origin.length; i++) {
        var current = origin[i];
        if(callback(current)) {
            result.push(current);
        }
    }
    return result;
}
newWords = myfilter(words, element =>element.length > 6);
//expected output: Array ["exuberant", "destruction", "present"]
```



