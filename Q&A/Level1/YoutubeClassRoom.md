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