## 🌏 HTML

### 📎 `<iframe></iframe>`

#### srcdoc attribute

- scrdoc이란 ?
  - `<iframe>` 태그의 srcdoc 속성은 `<iframe>` 요소에 보일 웹 페이지의 HTML 코드를 명시합니다. 다시 말해, `<iframe>`이 하나의 웹 페이지의 브라우저 역할을 하는 것입니다.
    만약 `srcdoc` 속성이 명시되어 있고 해당 브라우저가 `srcdoc` 속성을 지원하면, `<iframe>` 요소의 `src` 속성값은 `srcdoc` 속성값으로 재정의 됩니다.
  - 어떻게 활용하면 좋을까? : youtube API로 영상을 불러올 때, 사용자에게 썸네일을 먼저 보여주고 이후에 특정한 행동을 (ex. click) 통해 영상을 보여줌으로써 불필요한 지연을 경험하지 않도록 할 수 있습니다.
  - 참고문서 : http://tcpschool.com/html-tag-attrs/iframe-srcdoc
  - 참고문서 : https://developer.mozilla.org/en-US/docs/Web/API/HTMLIFrameElement/srcdoc
  - 참고문서 : https://samwize.com/2020/06/23/embedding-youtube-on-website-lazily/
