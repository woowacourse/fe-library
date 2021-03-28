## 🚀 지하철 노선도 Q&A

- 의견을 들어보고 싶어서 질문 드립니다! 여러분은 JWT Access Token을 어떻게 관리하시나요?
  저는 보통 localStorage에 저장하고, API 요청을 보낼 때 Header에 매번 담아서 요청하는 방법을 이용하고 있습니다. Access Token을 저장할 때, 쿠키에 담아서 저장하는 방법도 있지만, 각각 보안적으로 취약점이나 문제점이 존재한다고 합니다. Access Token을 최대한 완벽하게 관리할 수 있는 방법은 없을까요?

- 대칭키로 암호화 하는 건 어떨까요 ㅋㅋ 키는 잘 숨겨놓고..
- 근데 이번 미션에서는 web storage에 저장했다가 사용만 잘 해도 충분히 목표달성 아닌가 싶긴합니다!



###  지하철 노선도 1단계 jbee 공통 피드백 

#### babel
모든 크루분들이 잘 사용해주고 계십니다!
꽤나 중요한 친구라서 몇 가지 추가로 살펴보면 좋을 것들을 알려드려요~
@babel/preset-env 의 역할은 뭘까?
@babel/polyfill은 뭘까? (+ 왜 deprecated 되었을까?)
babel은 뭐고 polyfill은 뭐지? (다른건가?)

#### Protected Routes
로그인 상태를 판단하기 위해 라우터 이동마다 API 호출하고 있는데요, 왠지 비효율적이지 않나요? :생각하는_얼굴:
어떤 페이지에서 인증이 필요한 API를 호출했을 때, 에러가 발생하면 그 때 로그인 페이지로 redirect 해주면 어떨까요?

#### 에러 처리에 대한 이야기
API 호출이 기능에 추가되면서 try-catch를 사용하여 각자 다양한 방식으로 에러를 핸들링해주고 계십니다. 바로 위에서 말씀드린 Protected Routes 에서 드렸던 이야기와도 일맥상통할 이야기인데요,
늘 그렇듯 개발엔 돌아가기면 하면 틀린 것은 없다고 생각합니다. 다만 더 나은 것은 항상 있고 더 낫다고 하더라도 항상 “트레이드 오프“가 존재하기 마련인데요, 제가 최근에 이 에러 처리에 대해 고민했고 그 과정을 글로 적은게 있습니다. 여러분도 한번 에러를 어떻게 처리하면 좋을까 충분히 고민해보시고, 시간 되실 때 글 한 번 읽어보세요!
(1편, 3편은 React 중심이라서 2편만 읽어보시길 권장드립니다)
[율적인 프런트엔드 에러 핸들링 2편. 클라이언트의 사용자 중심 예외 처리](https://jbee.io/react/error-declarative-handling-2/)


## github pages에 SPA 배포하기

[gh-pages: dist 디렉토리만 deploy 하기](https://velog.io/@bigsaigon333/gh-pages-dist-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A7%8C-deploy-%ED%95%98%EA%B8%B0)
[원문(영어)- Host single page apps with GitHub Pages](https://github.com/rafgraph/spa-github-pages)
[한국어 번역본 - 깃허브 페이지(GitHub Pages)에 SPA 배포/호스팅 하기](https://github.com/sujinleeme/spa-github-pages-ko)

