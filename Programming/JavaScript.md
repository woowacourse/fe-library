## 🍒 JavaScript Q&A

### 두 배열의 비교는 어떻게 하나요?

```
console.log(['a'] === ['a']); // false
이런 경우를 어떻게 처리하는 게 좋을까요?? 저는 다음과 같은 방식으로 처리했어요.
const expectedArray = ['a','b','c'];
  expectedArray.forEach((val,index) => console.log(val === others[index])
)
```

- value vs reference 에 관한 아티클을 읽어보시면 좋을 것 같습니다.
- [o.deep.equal](https://docs.cypress.io/guides/references/assertions.html#Chai) 해보니까, 배열에서는 순서까지 같아야 하네요.. 순서가 다른 경우의 비교에서는 못쓰지만, 정렬을 할 수 있다면 두 배열을 정렬하고 나서 쓰면 좋을거 같아요!
- 배열 비교 조건이 여러개일 수 있습니다. 순서 정렬 여부, 유니크 요소 여부 등 몇가지 생각해봐야할 부분이 있어요! [스택오버플로우](https://stackoverflow.com/questions/3115982/how-to-check-if-two-arrays-are-equal-with-javascript) 시간될때 한번 읽어보세요!
- 자바스크립트에 배열을 [flat](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)해주는 메서드가 있습니다.

<br />

### 이벤트루프

```
아이고...허허허
아까 테코톡 Q&A할 때 대답한 게 죄다 틀린 것 같습니다..허허
Web API 는 timer API, geolocation API 등등 여러 API를 통틀어서 부르는 호칭이고,
걔네들이 각각의 스레드를 가지고 동작한다고 합니다...
근데 걔네들도 결국에는 콜백 큐에 작업을 쌓아서 호출 스택에서 실행된다는 사실...
잊지 마시기 바랍니다...허허허,,,
```

- [Is Web Api Multi-Threaded?](https://stackoverflow.com/questions/58910448/is-web-api-multi-threaded)
- [JavaScript Event Loop Explained](https://medium.com/front-end-weekly/javascript-event-loop-explained-4cd26af121d4)

<br />

### 이벤트루프는 어떻게 동작하나요?

```
이벤트 루프 관련 아티클을 읽고 나름대로 엔진-브라우저 상에서 처리되는 과정을 정리해 보았습니다.
콜 스택에서는 최상위 실행 컨텍스트 안의 코드를 우선 처리한다.
실행 컨텍스트 안에 비동기 처리 관련 Web APIs 가 있다면, 해당 API 의 여러 조건을 토대로 task queue 에 콜백 함수 / 이벤트 핸들러를 담아 둔다.
이벤트 루프는 현재의 실행 컨텍스트가 종료 되었는지 반복적으로 확인 한다.
해당 컨텍스트가 종료되면, task queue 에 대기 중인 함수를 선입선출 순으로 콜 스택으로 보내고, 콜 스택은 들어온 함수들을 바로 바로 처리한다.
2번 과정에 대해 궁금한 점이 있는데,
```

```js
function() {
	setTimeout(callBack1, 1000);
	setTimeout(callBack2, 3000);
	setTimeout(callBack3, 2000);
}
```

```
이러한 경우에는 setTimeout 이 타이머를 설정하고, 타이머 종료 순으로 task queue 에 [callBack1, callBack3, callBack2] 순으로
임시 저장을 하고 있다고 이해하는 게 맞을까요?
```

- 브라우저에서는 web api영역, 노드 js에서는 libuv가 타이머관련 로직을 처리하고 콜백함수만 테스크큐에 enqueue하는걸로 알고있어요. 동작이 멀티스레딩이라서 말씀하신대로 큐에 담길 것 같아요.
- 저는 [자바스크립트와 이벤트루프](https://meetup.toast.com/posts/89) 이거 보고 많이 공부가 됐어요.

<br />

### 체이닝 메서드 어떻게 활용할 수 있을까요?

```
function chaining은 메서드에서 객체를 리턴함으로써 메서드 뒤에 .console()같은 방식으로 쓰게 하는 것이라고 보입니다.
그래서 가독성이 더 좋아지고 줄 수가 짧아진다는 장점이 있는 거 같아요.

car.start()
car.drive()
두 줄을 아래처럼 바꿀 수 있습니다.
car.start().drive()
또 어떻게 활용할 수 있을까요?
```

- filter().map()처럼 chaining을 통해서 자료 구조를 좀 더 깔끔하게 가져오게 활용할 수도 있습니다. 체이닝 패턴 이라고 검색해보시면 더 많은 자료를 찾으실 수 있을 것 같습니다. rxjs를 이용한 코드에서 엄청 많이 찾을 수 있습니다.

<br />

### 환경변수 불러오기

<p align="center"><img src="https://user-images.githubusercontent.com/60066472/108371948-a2850780-7241-11eb-9a8c-cde6a5f356ec.png" width="400"></p>

```
프로젝트에서 .env.local 파일을 만들어서 환경변수를 설정해주었습니다.
그리고 index.js에서 console.log(process.env)로 찍으려고 하니까 사진과 같은 에러가 발생합니다.
어떻게 해야 환경변수를 불러올 수 있을까요?
```

- Process env는 nodejs에서 쓰는 환경변수 입니다.
- process가 node에서만 사용되는 객체인 것으로 알고있습니다. 웹팩 에서 플러그인으로 process.env를 설정하고 사용하는 건 본 것 같습니다.

<br />

### HTMLElement 프로토타입에 mixin 추가 시 문제점

```
기존의 메서드도 그대로 사용하면서 커스텀 메서드는 체이닝을 할 수 있게 해보았습니다. built-in 객체의 프로토타입에 이렇게 직접 적용해도 되는 걸까요?
```

```js
import { CLASSNAME } from '../constants/index.js';
const customElementMethodMixin = {
  show() {
    this.classList.remove(CLASSNAME.COMMON.HIDDEN);
    return this;
  },
  hide() {
    this.classList.add(CLASSNAME.COMMON.HIDDEN);
    return this;
  },
  toggle(className) {
    this.classList.toggle(className);
    return this;
  },
};
Object.assign(HTMLElement.prototype, customElementMethodMixin);
export const $ = (selector) => document.querySelector(selector);
// 사용예시
$('#app').show().toggle('--shining').innerText = 'test';
```

- 객체 내의 동명의 프로퍼티를 갖게 될 경우 그 값이 override 되기 때문에 내장 객체의 모든 프로퍼티를 파악하지 않는다면 코드 작성 중에 예상 동작과 다르게 적용될 수도 있을 것 같아요
- 빌트인 객체에 직접 적용하는 것은 많은 문제가 발생한다고 하네요. $ 함수 안에서 필요한 메서드만 만들어서 객체로 반환하는 것이 가장 안전할 것 같다고 생각합니다.

<br />

### createElement를 통해 생성된 DOM 객체에 appendChild한 경우 reflow가 발생할까요?

```
createElement를 통해 생성만 해둔 DOM 객체에 appendChild를 실행하는 것도 실제 DOM에 변경이 가해지는지, 그러니까 Reflow가 발생하는지 궁금합니다.
```

- createElement 자체는 DOM에 반영되지 않기 때문에 appendㅊhild하더라도 reflow가 발생하지 않아요.
  추가적으로 Element가 많아질수록 DOMNode.appendChild( … )보다 Fragment.appendChild( ... )를 사용하는 것이 좋아요.

<br />

### 상수파일 json vs js

```
상수파일 json이랑 js 중 뭐로 만드는게 좋을까요?
json은 읽기만 되고 수정이 안되어서 더 적절한 것 같아요
```

- json파일을 import하려면 babel 또는 webapack이 필요합니다. js에서 상수를 관리하는 것이 더 좋을 것 같아요.
  [참고링크](https://stackoverflow.com/questions/34944099/how-to-import-a-json-file-in-ecmascript-6)

<br />

### 크롬 콘솔 창에 `#`이 생기는 이유가 뭔가요 ?

```
콘솔에 샵은 뭘까요! 티케 궁금해서 미쳐가는 중
```

- 정확히 말하자면 크롬 타입 에러 메세지에요.
  다른 타입들은 #안뜨고 다르게 뜹니당

<br />

### switch - case 문에서 왜 케이스를 통과할까요?

```
switch-case 문 안에서,
this.matchingNumbers 가 5이고 this.isMatchBonus 가 true일 때는 rank를 2로 하고,
this.matchingNumbers 가 5이고 this.isMatchBonus 가 false일 때는 rank를 3으로 하고 싶은데 아래와 같이 썼을 때만 정상 작동하고,
case 5 && this.isMatchBonus 라고 조건문의 순서를 바꾸면 rank가 2가 아닌 3이 됩니다.
저희가 어딘가 잘못 쓴 건지, 아니면 개념을 잘못 이해하고 있는 건지 궁금해서 고민하다가 질문 올립니다!
아시는 분 답변 부탁드리겠습니다.
```

```js
switch (this.matchingNumbers) {
  case 6:
    this._rank = 1;
    break;
  case this.isMatchBonus && 5: // 문제의 라인
    this._rank = 2;
    break;
  case 5:
    this._rank = 3;
    break;
  case 4:
    this._rank = 4;
    break;
  case 3:
    this._rank = 5;
    break;
  default:
    this._rank = Infinity;
}
```

- case 5 에 `this.isMatchBonus`를 if문으로 분기하시면 어떨까요...?
- expr1 && expr2에서 expr1 를 true로 변환할 수 있는 경우 expr2을 반환하고, 그렇지 않으면 expr1을 반환합니다. `5 && true`의 경우는 `5`를 `true`로 변환할 수 있었기 때문에 `true`가 반환된 것이고
  `true && 5`의 경우는 `true`를 `true`라고 변환할 수 있었기에 `5`가 반환될 수 있었군요. 무조건 true나 false가 나올 줄 알았는데 이런 규칙이 있었군요... [참고링크](<https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/%EB%85%BC%EB%A6%AC_%EC%97%B0%EC%82%B0%EC%9E%90(Logical_Operators)>)
- `this._rank = this.isMatchBonus ? 2 : 3` 과 같은 방식으로 하는 어떨까요?
