## 📝 DOM

### Custom DOM Library 만들기

```
개인적으로 DOM library 를 만들어보고 고민했던 지점과 차용 패턴을 정리한 링크를 여기에 다시 올려두겠습니다! 
제가 봐도 아직 부족한 부분이 많지만 FE 아카이브에 해당 개념에 대해 이런 식으로도 고민을 해보았다는 의미로 정리되면 좋을 것 같아 재공유합니다. 😀 - 카일
```

- [[DOM] custom DOM library 만들기](https://velog.io/@mkitigy/DOM-custom-DOM-library-%EB%A7%8C%EB%93%A4%EA%B8%B0) (DOM 을 좀 더 편하게 쓰고 싶다면)

### visibility의 변경이 reflow를 발생시킬까?

```
visibility를 변경해주는게 reflow를 정말 발생시키지 않나요...? 
저는 visibility 속성을 조작하는 것도 reflow 를 발생시키는 것으로 아는데, 
제가 잘못 알고 있다면 지적해주시면 감사하겠습니다.
```

- reflow가 발생 : DOM의 레이아웃이 변경(element 크기 변경, element 위치 변경, 창 사이즈 조절 등)
- `visiblity: hidden`은 레이아웃은 유지(영역 차지)한 채로 해당 영역만 보이지 않게 하는 것이기 때문에 reflow가 발생하지 않고 repaint만 발생
- 반면 `display: none` 은 영역 자체가 사라져 외부 Element의 위치 이동이 존재하므로 reflow와 repaint 모두 발생