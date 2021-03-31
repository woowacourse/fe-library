## 📝 Webpack

### 대소문자 파일명 인식 관련 webpack 버그

문제를 간략히 말씀드리면

1. import from 구문에서 upper case 파일명을 불러옴
2. 실제 파일 이름은 lower case임
3. vscode 상에서는 문제가 없었지만 webpack --watch로 빌드할때 해당 파일의 변화를 감지하지 못하는 현상이 발생함

자세한 내용은 [미키 벨로그](https://velog.io/@0307kwon/%ED%8C%8C%EC%9D%BC%EB%AA%85-%EB%8C%80%EC%86%8C%EB%AC%B8%EC%9E%90-%EC%9D%B8%EC%8B%9D%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EB%AF%BC) 로 가시면 확인하실 수 있습니다!
이 문제의 해결 방법은

1. 아예 처음부터 스네이크 케이스나 케밥 케이스의 파일명을 짓기
2. 대소문자 실수를 잡아주는 webpack 플러그인 쓰기

```
저는 저번에 어떤 크루분이 질문하셨던 깃 관련 문제도 있고, 이번 webpack 문제도 있어서,
개인적으로 파일명을 케밥 케이스나 스네이크 케이스를 쓰는게 좀 더 근본적인 문제 해결책이라고 생각합니다.
그런데 저번에 파일명을 스네이크 케이스로 쓰지말라는 공통 피드백을 받기도 했고,
좋은 라이브러리들을 봐도 최근에는 카멜 케이스로 변하는 추세인 것 같은데 이유가 있을까요? 궁금합니다!
```

- [Google Style Guide - File name](https://google.github.io/styleguide/jsguide.html#file-name), [Google Style Guide - Rules common to all identifiers](https://google.github.io/styleguide/jsguide.html#naming-rules-common-to-all-identifiers) 구글 자바스크립트 스타일 가이드 때문이려나요?
- 그러네요. 구글은 파일명 `_`나 `-`써서 lowercase로 가이드하고, 에어비엔비는 파일명을 camelCase로 가이드하는군요. [Airbnb - Base filename](https://github.com/airbnb/javascript#naming--filename-matches-export)

### 새로고침 시 발생하는 오류를 Webpack으로 해결하기

```
webpack에
devServer: {
  historyApiFallback: true
}
옵션을 주면 404 에러가 뜰 때 index.html으로 자동으로 보내줍니다.
자동으로 보내줄 때 index.js를 다시 실행하는 것 같아요!
이것을 이용해서
//index.js
const path = window.location.pathname;
const app = new App();
app.init();
app.router.route(path);
app.runPathMatchedAction(path);
이런 식으로 새로 고침을 눌렀을 때의 path를 받아 놓고, 받아 놓은 path를 가지고 라우팅을 시도하면 404에러가 발생하지 않고 원래 작업하던 페이지로 쓱 넘어갑니다!
더 이상 주소 창을 더블클릭해서 지우고 첫 화면으로 가서 작업하지 않아도 됩니다!!
저만 몰랐을 수도 있지만 모르는 크루들을 위해 공유합니다.:눈이_하트_모양인_고양이::눈이_하트_모양인_고양이:
도움 : 도비, 카일
```
