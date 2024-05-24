---
title: Javascrpit
author: Jaeuk
date: 2024-05-08
category: Javascrpit
layout: post

---
first class citizen    
브라우저 웹서버 페이지 리로드 없이 자바스크립트 이용해서 서로 통신 = ajax


CallbackFunction
-------------
### CallbackFunction이란?
함수가 다른 함수의 파라미터로 전달되어 호출

```javascript
const words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];

const result = words.filter(word => word.length > 6); // word => word.length > 6 (callback function)
//expected output: Array ["exuberant", "destruction", "present"]
```


함수 만들기
```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];
function callback(element){
  return element.length > 6;
};
newWords = words.filter(callback);
//expected output: Array ["exuberant", "destruction", "present"]
```

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


Arrow Function
-------------
```javascript
words = [`spray`, `limit`, `elite`, `exuberant`, `destruction`, `present`];

newWords = words.filter(element =>element.length > 6);
//expected output: Array ["exuberant", "destruction", "present"]
```


Promise
-------------
### Promise란?
표준화된 처리   
Synchronous-순차적으로 실행   
Asynchronous-동시적으로 실행 (통신이 언제 끝날지 모를 때)   
- Jsonplaceholder 이용해보기
```javascript
fetch('http://example.com/movies.json')
    .then(function(response) {
        return response.json();
    })
    .then(function(myJson){
        console.log(JSON.stringify(myJson));
    });
```

```javascript
var fetched =fetch('http://example.com/movies.json'); // promise 리턴
fetched.then(function(result){});// response object 제공
fetched.catch(function(reason){});// false시 이유 제공

// promise chaining
fetch('http://example.com/movies.json')
    .then(function(responese) {
        // Nested promise then안에 then
        // response.json().then(function(data){
        //    console.log('data', data);
        // });
        // console.log('responese', responese); 
        // response.text();
        // response.json(); //promise 리턴 then, catch 사용 가능
       return response.json();
    })
    .catch(function(reason) {
        console.log('reason', reason);
    })
    .then(function(data) {
        console.log('data', data);
    });
```
### Promise 만들기
true, false일 때 둘 다 알려줘야한다
```javascript
function job1() {
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            //resolve('job1 ok!');
            reject('job1 fail!');
        },2000);
    });
};
function job2() {
    return new Promise(function(resolve, reject) {
        setTimeout(function() {
            resolve('job2 ok!');
        },2000);
    });
};
job1().then(function(data) {
    console.log('data', data);
    job2().thne(function(data) {
        console.log('data2', data);
    });
});
//chaining 
job1()
    .then(function(data) {
        console.log('data1', data);
        return job2();
    })
    .catch(function(reason) {
        console.log('reason', reason);
        return Promise.reject(reason);
    })
    .then(function(data) {
        console.log('data' data);
    });
```

### all
배열안에 함수가 모든 끝났을 때(제일 긴 함수가 동작을 마쳤을 때), 배열로 반환
```javascript
console.time('Promise.all');
Promise.all([timer(1000),timer(2000),timer(3000)]).then(function(result) {
    console.log('result', result);
    console.timeEnd('Promise.all');
});
console.timeEnd('Promise.all');
```
### race
배열안에 함수중 실행시간이 가장 짧은 함수가 끝났을 때 실행, 제일 빨린 끝난 함수결과
```javascript
Promise.race([timer(1000),timer(2000),timer(3000)]).then(function(result) {
    console.log('result', result);
    console.timeEnd('Promise.race');
});
```


async/await
-------------
await는 async함수 안에서 사용가능   
async는 promise 리턴하는 비동기적 함수

```javascript
function timer(time) {
    return new Promise(function(resolve) {
        setTimeout(function() {
            resolve(time);
        }, time);
    });
}
// console.log('start');
// timer(1000).then(function(time) {
//     console.log('time'+time);
//     return tmimer(time+1000);
// }).then(function(time) {
//     console.log('time'+time);
//     return tmimer(time+1000);
// }).then(function(time) {
//     console.log('time'+time);
//     console.log('end');
// });
async function run() { 
    console.log('start');
    var time = await timer(1000);
    console.log('time'+time);
    time = await time(time+1000);
    console.log('time'+time);
    time = await time(time+1000);
    console.log('time'+time);
    console.log('end');
    return time; // 리턴값도 가질 수 있다
}
console.log('parent start');
async function run2() {
    var time = await run(); // 비동기적 함수
    console.log('time: ' + time);
    console.log('parent end');
}

console.log('parent parent start');
run2().then(function() {
    console.log('parent parent end');
});
```

정규표현식
-------------
추출, 치환, 값 찾기
```javascript
var pattern = /a/;
var pattern = new RegExp('a');

var pattern = /a./; //.은 하나의 문자

pattern.exec('abcd'); // output: ["ab"];

pattern.test('abcd'); // true
pattern.test('bcd'); // false

var str = "abcdf";
str.match(pattern); // output: ["ab"];

str.replace(pattern, 'AB'); // str = "ABcdf";
```