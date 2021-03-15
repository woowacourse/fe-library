## 🎬 나만의 유튜브 강의실 Q&A
### API KEY를 은닉화에 대한 고민
keyword : env , api key , github secrets, Github Actions, firebase, netilfy, Serverless Function, Redirect Server, API

#### Q. env 파일 모듈 에러가 났는데, 어떻게 해결하나요?

```markdown
dotenv 모듈을 설치해서 사용하고 싶은데 아래와 같은 에러가 발생합니다..ㅠㅠ
오류 내용을 보면 import를 할 때 

import dotenv from './dotenv' 

와 같은 형태로 사용하라는 것 같은데, 저희는 

import dotenv from 'dotenv'

로 사용해서 그런 것 같다고 생각이 됩니다. 그래서 node_modules에 직접 접근을 해서 불러오기를 시도했지만 실패했습니다...
혹시 웹팩을 사용해야 하는 것인가요? 같은 오류를 해결한 크루가 있다면 알려주세요!
```
![image](https://user-images.githubusercontent.com/59258239/110398682-ac1ec400-80b7-11eb-9c2f-ef587a33f3b6.png)


- [https://stackoverflow.com/questions/42182577/is-it-possible-to-use-dotenv-in-a-react-project](https://stackoverflow.com/questions/42182577/is-it-possible-to-use-dotenv-in-a-react-project) 여기서는 웹팩 쓰라네요
- Dotenv는 NodeJS 로 서버 돌릴때 서버 실행환경변수를 설정해주는 모듈로 알고 있어서 웹팩을 쓰지 않는한 프론트엔드에는 적용이 안되는걸로 알고 있어요.

<br />

#### API Key를 숨기는 방법 두번째, Github Secrets 사용

- 검색해보니까 `github secrets`를 이용하는 방법도 있네요! 저희가 현재 서버 없이 작업하고 데모 페이지를 위해 키가 필요한 경우니까 `github secrets`만 이용해도 충분할거 같아요!
- Github Secrets를 사용하려면 Github Actions을 써야 한다.(배포를 Github Actions로 해야한다) cicd
    - [https://git-secret.io/](https://git-secret.io/) 이런 배쉬 툴을 이용하는 방법도 고려해볼 수 있겠네요

<br />

#### API Key를 숨기는 방법 세번째, Firebase & Netilfy 사용

- 구글 firebase로 호스팅해서 pr에 데모 페이지 올려도 될것같아요! (호스팅 설정까지 3분컷! 근데, 브라우저에서 source 뜯어보면 `key`값 보이긴합니다 ㅎㅎㅜ) [참고 블로그](https://zereight.tistory.com/827)
- 저희는 netlify 이용해서 서버 호스팅해줬고, `build`해주는 순간에 `echo` 명령어를 이용해 `env.js` 파일을 만들어주는 방식으로 구현했습니다! 이 방법도 도비와 마찬가지로 source 보면 보입니다! [참고 유튜브](https://youtu.be/2J3xbMkH2K4)

<br />

#### API Key를 숨기는 방법 네번째, 원하는 URL에서만 요청을 보냈을 때마다 응답이 오도록 제한걸기
- 프론트엔드 서버에서는 API 키는 완전히 숨길 수는 없습니다. 결국 요청을 보낼 때는 API 키를 `query string`에 포함해서 보내기 때문입니다. 크롬 개발자 도구의 Network 탭에서 요청이 보내질 때마다 API 키가 포함된 요청 URL을 바로 확인할 수 있었습니다.
- 그래서 보통 이렇게 API 키를 제공하는 곳에서는 원하는 URL에서만 요청을 보냈을 때마다 응답이 오도록 제한을 걸 수 있습니다.
- 구글 API의 경우에는 첨부한 이미지에서와 같이 [사용자 인증 정보] 화면에서 해당 API 키의 정보에서 수정 버튼을 누른 뒤, [HTTP 리퍼러(웹사이트)]를 누르면 나오는 [웹 사이트 제한 사항]에서 항목 추가로 URL을 지정해주시면 됩니다.
- 구글 API 키의 경우는 유튜브 뿐만 아니라 구글 지도와 같은 다른 서비스를 이용할 때도 동일한 키를 사용하기 때문에, 특정 API만 호출할 수 있도록 제한을 걸어줄 수 있습니다.
- 물론 배포를 할 때는 Netlify나 Firebase, Heroku와 같이 환경 변수를 관리할 수 있는 서비스를 통해서 배포하거나, Node.js를 이용한 서버에서 배포를 한다면 `process.env` 객체에 둔다던지 하는 방법으로 API 키를 최대한 숨겨두는 것이 좋겠다고 생각합니다.
<p align="center"><img src="https://user-images.githubusercontent.com/59258239/110399439-361b5c80-80b9-11eb-94d3-0e20b42a972b.png"  width="30%" ></p>
<br />

#### API Key를 숨기는 방법 다섯번째, Serverless Function을 도입하여 Redirect Server를 만들어 사용하기
- Client-Side에서는 API Key를 숨길 수 없다
- Netlify Functions를 이용해 Redirect Server를 만들어 사용하여 API key를 숨길 수 있다.
- [바로 이용가능한 repo](https://github.com/bigsaigon333/hide-api-key-with-serverless-functions) : 이 레포지토리는 Client-Side 에서 API Key를 노출하지 않고 Youtube API와 통신하기 위한 redirect server 입니다.
- [레포 주인의 정리 블로그](https://velog.io/@bigsaigon333/Client-Side%EC%97%90%EC%84%9C-Youtube-API-Key-%EC%88%A8%EA%B8%B0%EA%B8%B0)
- [365kim - 쉽게 쓰인 유튜브 API 튜토리얼](https://365kim.tistory.com/93)
<br />

---

### Q. YOUTUBE API Quota가 너무 많이 들어요
keyword : youtube API Key, Quota 
```
https://developers.google.com/youtube/v3/determine_quota_cost
유튜브 API 코스트를 보면 search api 요청을 한번 보내는데 비용이 100입니다. 
하루 할당량이 10,000이라서 벌써 할당량을 다 사용해버렸네요… 
혹시 다른 분들은 search말고 다른 api요청을 보내고 계신가요? 아니면 검색을 최대한 자제하면서 미션을 진행하고 계씬가요?
```
- 구글 계정을 계속 만드는 중입니다..
- 저희두 구글 계정을 추가로 만들고 있습니다... 알아낸 바에 따르면 태평양 표준시(PT)에 할당량이 초기화되어서 곧 있을 17:00 면 초기화되기를 바라고 있습니다
- 일단 검색은 구현해두고 비활성화해두고 videos 를 이용해 영상 불러오는거 테스트 입니다. search는 비용이 100인데 video는 1이에요. 대신 키워드검색은 안되더라고요.[참고](https://developers.google.com/youtube/v3/docs/videos/list?hl=ko)
- https://www.googleapis.com/youtube/v3/search로 100씩 소진해야하지만, 검색은 어쨌든 잘될테니 https://www.googleapis.com/youtube/v3/videos 로 1씩 소진하며 렌더를 해본다!
- 저희는 따로 개발용으로 더미 데이터만 반환하는 가짜 API를 하나 만들어서 작업 중입니다. API 요청해서 받아온 데이터 JSON을 텍스트로 따로 만든 다음에, 그 JSON을 받아오도록 구현해서 만들었습니다. 제출할 때는 실제 API로 호출되게 코드를 바꿔서 제출하려구요

---

### **Youtube 미션 공통 리뷰** by JBee

**1. Local Storage**
- key 값을 상수화 한다면?
- 좀 더 나아가 key 값과 함께 추상화를 한 단계 더 하면 어떨까?
- getter에서 default value를 지정해주곤 하는데, 이 부분도 함께 **추상화** 할 수는 없을까?
- JSON.parse 하다가 올바르지 못한 JSON이 저장될 수는 없을까?
- parse하다가 에러가 발생하면? 고려해줘야 하지 않을까?

**2. Modal** 
- 모달이 open인 상태에서 document **body 의 scroll을 lock 해주는 UX**는 어떨까?
- dimmer click을 특정 값(data-*, id, class)에 의존하지 않고 **target, current target을 비교**해서 컨트롤 할 수 있지 않을까? -> 자세한 내용은 [Dom object model Event Delegation 글](https://jbee.io/web/about-event-in-the-web/) 참고!

**3. Scroll Event**
- 스크롤 이벤트는 엄청 많이 발생하는데 좀 더 **최적화** 해볼 수 있지 않을까? -> 자세한 내용은 [스크롤 이벤트 최적화 글](https://jbee.io/web/optimize-scroll-event/) 참고! **(주의: 어려움)**
- 스크롤 이벤트 너무 비용이 많이 드는데 **다른 방법**은 없을까? -> [IntersectionObserver](https://developer.mozilla.org/ko/docs/Web/API/Intersection_Observer_API)로 할 수 있을까

**4. Security**
- a tag에 `target="_blank"` property를 줘서 새 창으로 띄울 때 고려해야하는 이슈가…! (**hint: noopener**)

**5. Bonus**
- SPA Application (written by React)의 CSR(Client Side Rendering) vs Server Side Rendering (with VanillaJS) 무엇이 다를까?
