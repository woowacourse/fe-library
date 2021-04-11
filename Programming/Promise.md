# Promise

## 관련 아티클

- [JavaScript Promise](https://www.hanbit.co.kr/store/books/look.php?p_code=E5027975256)

- [비동기 함수 반환하기 - How to return the result of an asynchronous function in JavaScript](https://flaviocopes.com/how-to-return-result-asynchronous-function)

- [await vs return vs return await](https://jakearchibald.com/2017/await-vs-return-vs-return-await)

- [Async-Await 로 단순화하기 - Async-Await ≈ Generators + Promises | Hacker Noon ](https://hackernoon.com/async-await-generators-promises-51f1a6ceede2)

- [Async-Await 로 단순화하기 - Async/Await Will Make Your Code Simpler](https://blog.patricktriest.com/what-is-async-await-why-should-you-care)

- [Promise Chaining은 죽음 - Promise chaining is dead. Long live async/await - LogRocket Blog](https://blog.logrocket.com/promise-chaining-is-dead-long-live-async-await-445897870abc)


## Q. Macro Task Queue, Micro Task Queue, Event Loop
```jsx
const myPromise = Promise.resolve('Promise !');
const func1 = () => {
   myPromise.then(res => console.log(res + ' 1')); 
   setTimeout(() => console.log('Timeout 1!'), 0); 
   console.log('Last line 1!');
}
const func2 = async () => {
   console.log(await myPromise + ' 2');
   setTimeout(() => console.log('Timeout 2!'), 0);
   console.log('Last line 2!');
}
func1();
func2();
// Output: 
// Last Line 1! Promise 1! Promise 2! Last Line 2! Timeout 1! Timeout 2!
```

### 지그(송지은): @콜린(이수연) 과 스터디 중 풀리지 않는 문제가 있어서 질문 드립니다!
1. func1이 호출되고 func1 내부의 myPromise는 microTaskQueue 로, setTimeout은 macroTaskQueue로 이동한다.
2. func1의 “Last line 1!“이 출력된다.
3. JS call stack이 비워진다. (콜린 생각)
4. call stack이 empty 상태이므로 event loop에 의해 microTask인 myPromise가 실행되어 Promise 1을 출력한다.
5. 이 시점에서, macroTask인 func1의 setTimeout 콜백 함수가 실행되어 “Timeout 1!“이 찍혀야 할 것 같은데,
6. 왜 func2가 먼저 담겨 “Promise 2!“를 먼저 출력할까요?

### A. 카일(임광열)  
1. func1 - myPromise ⇒ micro task queue
2. func1 - setTimeout ⇒ macro task queue
3. console.log()
4. func2 - myPromise ⇒ micro task queue (후순위 로직 await)
5. 스크립팅 문 종료 (한 개의 macro task 종료)
6. microtask 처리 (func1 myPromise, func2 myPromise)
7. func2 - setTimeout ⇒ macro task queue
8. console.log()
9. macrotask 처리 (func1 setTimeout, func2 setTimeout)
macro task - micro task 순으로 태스크를 처리할 때, 5. 스크립팅 문의 실행도 하나의 macro task 로 간주되기 때문에 해당 함수가 모두 호출되고 콜스택이 비워지는 것을 시점으로 파악하는 게 더 아웃풋과 연결 될 것 같아요!

https://ko.javascript.info/event-loop 여기서 요약 섹션에 있는 이벤트 루프 알고리즘을 읽어보면 더 파악하기 쉬울 듯 합니다 
