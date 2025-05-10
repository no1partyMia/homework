# 3주차 회고

2025년 5월 11일

_멋쟁이사자처럼 프론트엔드 부트캠프 14기_

## 배운 것

- `<img>` 태그 하나만 사용하기 보다는 대체 이미지를 위해 `<source>`를 사용하자
  picture를 안쓴다면 img 태그에 srcset이라도 추가하기! picture는 미디어, 뷰포트 같이 세세한 속성을 위해 쓰는 것. WebP를 지원하지 않는 브라우저 환경에서도 자동으로 PNG로 폴백되어 로딩 오류를 방지할 수 있다. WebP를 지원하지 않는 브라우저나 환경이 있을 수 있기 때문에 무작정 img 요소만 사용하지 말고 source를 적극 사용하자.

  ```
  <figure class="top-brand-item">
    <div>
      <picture>
        <source srcset="/src/assets/kream/top-brand/webp/top-brand-product-01.webp" type="image/webp" />
        <img src="/src/assets/kream/top-brand/png/top-brand-product-01.png" alt="" />
      </picture>
    </div>
    <figcaption><a href="/">나이키</a></figcaption>
  </figure>
  ```

- css float
  float을 처음 들어봤고 써본 적도 없었다. flex는 row가 기본값이니까 css로 row한 방법이 당연한 줄 알았다. flex가 등장하기 전에는 레이아웃 배치의 주축이었던 기능으로, 요소를 좌우로 띄워 텍스트나 다른 블록이 감싸도록 만들 수 있다.

- auto margin  
  `margin-inline: auto;`  
  수평 중앙 정렬이 필요한 블록 요소에 가장 간단하게 적용할 수 있는 방법으로, 요소의 좌우 마진을 자동으로 동일하게 설정해 가운데 띄운다. 반응형 레이아웃에서는 max-width와 함께 쓰면 화면 크기에 따라 적절히 크기를 유지하면서도 중앙에 고정된 레이아웃을 보장한다.  
  이번 과제에서 유용하게 사용했다.

- CSS 박스 모델

  ```
  +----------------------------+  ← margin (공간)
  |   (border)                |
  |  +----------------------+ |
  |  |     padding          | |
  |  |  +---------------+   | |
  |  |  |   content     |   | |
  |  |  +---------------+   | |
  |  +----------------------+ |
  +----------------------------+

  ```

  모든 요소는 content → padding → border → margin 순으로 외곽 공간이 쌓이며, 이 구조를 이해해야 정확한 크기 계산과 배치를 할 수 있다.
  특히 box-sizing: border-box;를 사용하면 padding과 border를 포함한 전체 너비를 계산해 예측 가능한 레이아웃 구성이 가능해진다.

- block 부모와 inline 자식일 때, 자식의 가운데 정렬  
  부모에 text-align: center;를 주면 인라인 혹은 인라인-블록 자식들이 수평 중앙에 배치되며, 특정 상황에선 line-height 조정으로 수직 중앙도 맞출 수 있다.

- custom properties와 tailwind.config.js 정의의 차이

  | 구분      | `tailwind.config.js`                              | CSS Custom Properties (`--`)   |
  | --------- | ------------------------------------------------- | ------------------------------ |
  | 정의 위치 | Javascript 설정 파일                              | CSS 파일 (`:root` 등)          |
  | 용도      | Tailwind 유틸리티 클래스에 사용될 값 (theme 기반) | 일반 CSS 내에서 변수처럼 사용  |
  | 적용 대상 | Tailwind 클래스 생성 시 참고                      | CSS 속성값에 직접 적용         |
  | JS 제어   | Tailwind 빌드 시만 가능                           | 런타임에서 JS로 동적 제어 가능 |

  Tailwind v4.0에서는 이제 tailwind.config.js 없이 CSS 내에서 custom properties와 @theme을 활용하라고 추천한다.
