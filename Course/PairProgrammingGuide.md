## 📝 페어프로그래밍 가이드

### 원본저장소에 제 브랜치가 없는데 어떻게 하나요?
- 사진에는 '진행 미션'자리에 보이는 '미션 시작' 버튼 누르면 본인 깃헙 닉네임으로 브랜치 생성 됩니다.
  <p align="center"><img src="https://user-images.githubusercontent.com/60066472/108366995-52577680-723c-11eb-999c-9d9053cb72db.png" width="300"></p>

<br />

### PR을 올리고 리뷰요청 버튼을 눌러도 리뷰요청이 안돼요.
- woowacourse:${본인 깃헙 아이디} 로 PR 보내셔야 합니다.
  <p  align="center"><img src="https://user-images.githubusercontent.com/60066472/108366277-87af9480-723b-11eb-9800-18e6a7a9431e.png" width="600"></p>
  
<br />

### PR 올리고 나서 메일도 보내야 하나요?
- 메일은 안보내줘도 됩니다.
  
<br />

### PR 커밋 로그에 페어와 함께 커밋을 쌓을 수 있는 방법이 있나요?
- 방법1
  - 페어1의 레포에는 git remote로 페어2의 레포를 add하고, 페어2의 레포에는 git remote로 페어1의 레포를 add해서 push, pull하면 됩니다. 참고하면 좋은 링크입니다. [git pull pair](https://dalya-tech.tistory.com/1), [Git Workflow](https://paigekim29.medium.com/til-2020-11-30-3f78f73d1173)
- 방법2
  - 페어1과 페어2 모두 페어1의 브랜치를 각자의 로컬에 클론해서 push, pull해도 됩니다. (최초에 권한 부여 필요, 그림:그루밍)
  <p align="center"><img src="https://user-images.githubusercontent.com/60066472/108356369-65177e80-722f-11eb-821a-2330261aeb1d.png" width="500"></p>

<br />

### 제가 직접 merge 할 수 있나요?
- 머지는 리뷰어만 할 수 있는 권한이 있습니다. 리뷰어에게 dm 보내서 머지해달라고 요청하세요.
  
<br />

### 커밋메세지의 feat이나 feature는 무슨 의미인가요?
- 특정 기능을 구현했을 때 feat을 주로 사용합니다. [여기](https://medium.com/hashbox/git-commit-%EB%A9%94%EC%84%B8%EC%A7%80-%EA%B7%9C%EC%B9%99-conventional-commits-71710f7f53c)서 컨벤션을 확인해볼 수 있어요.
- feature 는 주로 새로운 기능 추가를 할 때 이용합니다. feature 이라는 단어가 기능이라는 의미를 가지기도해서 그렇게 사용하는 것 같아요. 
- 영영 사전에서는 `something that makes a product, machine, or system different, and usually better, than others of a similar type` 라는 뜻과 통할 것 같은데 , 상품, 기기나 시스템을 다른 유사한 것들보다 더 좋거나, 다르게 만드는 것을 의미한다네요. 문맥상 이렇게 쓰여서, 특징 특성보다는 기능이라는 의미로 이해할 수 있을 것 같아요.
- 앵귤러 팀 커밋 컨벤션에 대해 검색해보셔도 좋습니다.

## 총 3단계 미션은 어떻게 진행하나요?
- 페어와 함께 1단계 기능을 구현하고 리팩토링 합니다. 페어와 동일한 코드로 각자 PR을 올리셔서 리뷰어에게 리뷰 요청을 하세요. 두 리뷰어의 리뷰 종합해 페어와 함께 토론 후 피드백 모두 반영해주세요.
- 미션 1단계  완료 후 동일한 코드를 가지고 페어와 함께 2단계 미션을 시작합니다. 2단계 구현을 마치면 각자 리팩토링을 하고 PR을 올립니다. 
- 이후로는 (총 2단계 미션인 경우와 동일하게) 각자 리뷰를 반영하고 3단계까지 진행하시면 됩니다.
