## 📝 Cypress Q&A

### 모듈을 어떻게 import 해서 사용하나요?
```
model로 선언한 RacingCar() 모듈을 cypress spec 코드에서 import해서 쓸 수 있나요?
import하면 addEventListener() 하는 부분에서 DOM을 찾을 수 없다는 문제가 계속 발생합니다.
혹시 다른 라이브러리 등을 설치해서 쓰셨는지 이와 같은 에러는 없으셨는지 궁금합니다!
```
  - 비즈니스 로직 함수만 따로 가져와서 사용했어요. nodejs에는 DOM객체가 없어서 따로 만들어야 합니다.
  - spec코드에 import해오면 html에 붙어있는 형태가 아니라 DOM 조작을 하지 못합니다. 다른 방식으로 구현하셔야 합니다.
  - Car 객체에 DOM을 조작하는 요소가 없으면 require해서 사용할 수 있습니다. DOM 조작 메서드를 분리하는 것은 어떨까 싶습니다.
  - `dom && dom.style.display = 'none'`과 같이 dom 요소가 있는 경우에만 dom 관련 로직을 수행하게끔 하는 방법도 있습니다.

<br />

### alert 호출 여부는 어떻게 검증하나요?
```
window.alert 가 호출이 되어야 하는 상황임에도 아예 window.alert 가 호출되지 않은 경우면 아래의 코드는 문제없이 통과될 것 같습니다.
cy.on('window:alert', (txt) => {expect(txt).to.contains(CAR_NAME_EMPTY);});
해당 부분에 대해서는 어떻게 검증하셨을까요? 
```
- 저도 이렇게 해서 alert가 없으면 pass가 되어서 결국 stub를 이용해서 구현했습니다. valid 테스트하는 describe를 분리해서 아래와 같이 공통화 시켜주었습니다.
  ```javascript
  beforeEach(() => {
    cy.visit("http://localhost:5500/");
    cy.window()
      .then(win => cy.stub(win, "alert"))
      .as("alertStub");
  });
  ```

<br />

### 직접 테스트했을 때 통과하지만 cypress에서는 통과가 안돼요.
```
자동차 1단계 alert 한 후 화면 조작 관련된 질문입니다.
자동차 이름을 입력받은 후, 유효성 검사를 통과하지 못하면 alert를 띄워준 후 다시 게임을 초기화 하도록 설정하였습니다. 
그 과정에서 테스트 코드와 직접 입력했을 때 모순이 생깁니다.
테스트 돌려보면 alert를 확인 한 후 시도 횟수를 입력하는 칸이 보여지고, 직접해보면 잘못된 정보를 입력한 경우 보이지 않습니다.
어떠한 자동차 이름을 입력하게 한 경우에도 강제로 시도 횟수를 입력하는 부분을 숨기도록 설정했을 때, 테스트 코드가 통과합니다.
어떤 부분이 잘못되었는지 모르곘습니다ʕʘ‿ʘʔ ʕʘ‿ʘʔ 도와주세여ㅠㅠㅠ 
```
- 해결이 되었습니다. cypress의 should 와 expect의 동작 차이인 것 같습니다.
- 저희가 원했던대로 잘못된 케이스를 넣으면 무조건적으로 alert가 뜨고 그 이후에 안보이게 하려고 한다면 should를 쓰는게 맞는가 봅니다.
  <p align="center"><img src="https://user-images.githubusercontent.com/60066472/108363872-bf690d00-7238-11eb-8471-2deb42870498.png" width="400"></p>


<br />

### cypress 에서 DOM 요소를 찾을 수 없다는 에러가 발생합니다.
  <p align="center"><img src="https://user-images.githubusercontent.com/60066472/108364946-fbe93880-7239-11eb-8fcf-4146e801e41b.png" width="200"></p>
  
```
addArrow 함수는 피드백 받기 이전에 view/racingView.js 에 displayArrow 라는 이름으로 있었는데
이름을 addArrow 로 변경하고 위치를 controller/racingController.js 로 옮겼습니다.
문제는 racingTest.spec.js 에서 import 를 변경된 위치와 이름으로 변경하면, 첨부한 사진과 같은 에러가 발생합니다ㅠ
집단 지성으로 문제의 원인을 유추해봤을 때, ‘앱 전체가 처음에 컴파일 될 때 문제가 발생하는 듯 하다’라고 몇몇 분께서 말씀해주셨습니다.
근거로, 새로운 파일을 만들어서 addArrow 만 넣고 import 했을 때는 문제없이 실행되었습니다.
전체 코드는 https://github.com/jum0/addArrow 에서 따로 확인하실 수 있습니다.
```
- spec.js에서는 dom 요소에 접근할 때 cy 메소드를 사용해야 하는것 같습니다. [(Stack Overflow)](https://stackoverflow.com/questions/60439448/document-queryselectorall-doesnt-work-in-cypress-running-with-chrome-80)
- 문제를 찾았습니다. 찾고자 하는 값들이 cypress의 document에 없으니 null 값에 대해서 value 나, addEventListner 와 같은 동작을 할 수 없다고 하는 것이었습니다. racingController 에서 index.js 에서 import 를 불러오지 않게 하거나, addArrow가 다른 함수를 이용하지 않으니, 아예 다른 파일로 빼놓아야 할 것 같습니다.
  <p align="center"><img src="https://user-images.githubusercontent.com/60066472/108364533-841b0e00-7239-11eb-81da-2bf06e25f26a.png" width="400"></p>


<br />

### cypress 버전 오류가 나요.
```
cypress 6.5 버전 오류가 나네요. 어떻게 해결할 수 있을까요?
```
- `yarn remove cypress` 하신 다음에 `yarn add cypress@6.4.0` 하시면 문제 없이 열립니다.
