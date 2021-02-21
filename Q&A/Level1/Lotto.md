## 🚀 로또 Q&A

### CSS 클래스 추가/삭제에 내포된 의미를 어떻게 드러낼 수 있을까요?
```
이번 과제에서는 최대한 innerHTML을 이용한 렌더링을 줄이고 CSS 처리 기반으로 로직을 짜고 있는데요,
class name을 추가, 삭제하는 코드를 어떻게 하면 더 명시적으로 표현할 수 있을까요?

$lottoContainer.classList.add('flex-col');
$lottoContainer.classList.remove('flex-col');

토글버튼의 이벤트를 조작하는 함수에서 'flex-col'이라는 class이름의 조작이 다른 사람이 보기에 한번에 이해하기는 쉽지않을 것 같아서요.
주석을 이용해 좀 더 부연 설명을 하는 쪽도 있을 것 같은데 각자의 생각을 공유해주시면 감사하겠습니다
```
- flex-col  클래스를 추가하여 하고 싶어하는 행동을 함수명으로 해주면 어떨까요? flex-col 클래스는 목적을 달성하기 위한 수단이니까, 그 목적을 함수명으로 하면 좋겠다는 뜻입니다. 
  ```javascript
  const 레이아웃을 가로로 전환한다 = () => {
    $lottoContainer.classList.remove('flex-col');
  }
  ```
- 저는 가독성을 위한 추상화는 좋다고 생각합니다. 다만, 이제 flex-col 의 의미를 알고 나서 다시 보게 되니, 현재로도 충분히 괜찮아보이네요.
- 저도 메서드로 추상화하는 쪽이 제일 합당해보입니다.
- InnerHTML은 왜 지양하나요?
  - 렌더링할 때 innerHTML을 반복적으로 사용하는 것은 노드를 계속 추가해주는 행위라서 브라우저의 속도에 영향을 미친다고 합니다. 굳이 동적으로 가공해서 뿌려줘야 하는 애들이 아니라면 한 번에 먼저 렌더링을 해놓고 display 로 다루어주는 게 좋다고 해서 그런 식으로 초점을 맞추고 진행했습니다.

<br />

### CSS 수직 정렬 어떻게 하나요?
```
로또 미션 진행 중 HTML 요소 수직정렬로 애를 먹고 있습니다.
flex, flex-flow, flex-wrap 등 여러 속성을 넣어보면서 시도하고 있는데 예시 사진처럼 깔끔하게 정렬되지 않네요ㅠㅠ
```
- 아래 구조처럼 로또와 번호 열을 따로 감싸주는 wrapper 노드를 생성해 각 flex 방향을 제시해주면 됩니다. container 의 flex-direction 은 column, wrapper 의 flex-direction은 row 이렇게요 !
  ```
  <container>
    <wrapper>
      <로또> <번호>
    </wrapper>
    <wrapper>
      <로또> <번호>
    </wrapper>
  </container>
  ```
- 위의 구조에서 container에 아래처럼 CSS 주면 로또티켓 이모지랑 글씨랑 세로로 중앙정렬 됩니다.
  ```
  display: flex;
  align-items: center;
  ```
- 저희도 준이 만들어주신 flex-col을 넣고, 티켓 이모지가 살짝 글씨보다 위에있는 느낌이 들어서 티켓 이모지에 mt-1 클래스 줬습니다.
- 해결한 코드입니다.
  ```
  <div
  id="purchase-result-section__col-align"
  class="d-flex flex-wrap flex-col">
    <div class="d-flex flex-wrap">
      <span class="purchase-result-section__lotto-icon mx-1 text-4xl"
        >🎟️
      </span>
      <span class="mx-1 mt-1 text-xl">19, 11, 17</span>
    </div>
    ...
  </div>
  ```
  
<br />  

### CSS Flex 꿀 자료 공유 합니다
```
저번에 로또 번호 수직 정렬 질문이 올라왔었죠.
저도 어제 페어 하면서 <label>태그 안에 <input>를 집어 넣겠다고 HTML을 변경했다가 스타일이 깨져 flex 복습하며 복구하다 보니
전에 본  네이버 D2 블로그 글이 생각나서 공유합니다. 저번 질문에 나왔던 수직 중앙 정렬 예시도 있어요
```
- [flexbox로 만들 수 있는 10가지 레이아웃](https://d2.naver.com/helloworld/8540176)
- 거의 모든 flex요소를 다 써볼 수 있는 [개구리 게임](https://flexboxfroggy.com/#ko)도 있어요! 
- 저는 [플렉스박스 가이드](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) 보고 바로 이해됐어요
- 영어가 부담스러우신 분은 [휴로파이 블로그](https://heropy.blog/2018/11/24/css-flexible-box/)도 추천합니다. 저는 flex 쓸 때 마다 여기서 찾아봐요
