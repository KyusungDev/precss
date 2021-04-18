# PRECSS 설계 가이드

## 규칙

- 특성에 따라 CSS를 분류한다.
- HTML과 스타일링을 느슨하게 결합한다.
- 영향 범위를 지나치게 넓히지 않는다.
- 특정한 콘텍스트에 지나치게 의존하지 않는다.
- 상세도를 지나치게 높이지 않는다.
- 클래스 이름에서 영향 범위를 유추할 수 있다.
- 클래스 이름에서 형태, 기능, 역할을 유추할 수 있다.
- 확장하기 쉽다.

### PreCSS 규칙

#### 여섯 가지 그룹 분류

- 베이스
- 레이아웃
- 모듈
  - 블록 모듈
  - 엘리먼트 모듈
- 헬퍼
- 유니크
- 프로그램

#### 기본 지침

- 이름 규칙 (클래스 이름에서 영향 범위를 유추할 수 있다)
  - 각 그룹에서 두 글자의 접두사 뒤에는 언더스코어를 사용하고 그 뒤에는 클래스 이름을 붙인다.
  - 한 계층안에서 여러 단어를 포함하는 경우에는 앞 문자를 소문자로 기술하는 로워 캐멀 케이스 (lowerCamelCase)를 사용한다.
  - 상세도 관리가 복잡해지는 것을 방지하기 위해서 ID 셀렉터를 기본적으로 사용하지 않는다.
- 범용적으로 사용할 수 있는 단어
  - \_wrapper, \_inner, \_header, \_body, \_footer
- 베이스 그룹 (접두사 없음)

  > 특성에 따라 CSS를 분류한다.
  > 영향 범위를 지나치게 넓히지 않는다.

  ```css
  html {
    font-family: serif;
  }
  a {
    color: #1565c0;
    text-decoration: none;
  }
  ```

#### 레이아웃 그룹 (\_ly)

> 특성에 따라 CSS를 분류한다.

- 헤더, 보디, 메인, 사이드, 푸터 등 큰 레이아웃을 형성하는 요소에 사용한다.
- 원칙적으로 레이아웃과 관련된 스타일링 **(width, margin, padding, float)**만 사용할 수 있다.

#### 모듈 그룹 (\_bl, \_el)

> 클래스 이름에서 영향 범위를 유추할 수 있다.
> 클래스 이름에서 형태, 기능, 역할을 유추할 수 있다.

- 블록 모듈 (\_bl)

  - 여러 Element를 가진 Block
  - 블록 모듈에 레이아웃에 관련 스타일링은 하지 않고, 블록 모듈을 사용하는 콘텍스트의 Element로서 스타일을 적용한다.

  ```html
  <div class="bl_card">
    <figure class="bl_card_imgWrapper">
      <img src="/assets/img/elements/code.jpg" alt="웹사이트 제작" />
    </figure>
    <div class="bl_card_body">
      <p class="bl_card_ttl">웹사이트 제작</p>
      <p class="bl_card_txt">사용자에게 최고의 체험을 제공하는</p>
    </div>
  </div>
  ```

  ```css
  .bl_card {
    box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16);
    font-size: 16px;
    line-height: 1.5;
  }
  .bl_card_imgWrapper {
    position: relative;
    padding-top: 56.25%;
    overflow: hidden;
  }
  .bl_card_imgWrapper img {
    position: absolute;
    top: 50%;
    width: 100%;
    transform: translateY(-50%);
  }
  .bl_card_body {
    padding: 15px;
  }
  .bl_card_ttl {
    margin-bottom: 5px;
    font-size: 1.125rem;
    font-weight: bold;
  }
  .bl_card_txt {
    color: #777;
  }
  ```

### 저자의 기준을 나누는 방법

### 팁

- 모듈에 대한 레이아웃 지정모듈 자체에는 레이아웃과 관련된 지정은 하지 않는 것이 좋다.

  - position (static, relative)
  - z-index
  - top / right / bottom / left
  - float
  - width
  - margin

- 클래스의 이름에서 영향 범위를 유추할 수 있도록 하려면?

  - 자녀 요소의 클래스 이름 머리에 모듈 이름을 붙인다.

- 기본 모듈에서 파생 모듈을 만들고자 하는 경우 멀티 클래스 설계를 고려한다.

```html
<a class="el_btn hp_theme" href="#">기본 버튼</a> <a class="el_btn hp_warning" href="#">색이 다른 버튼</a>
```

- 모디파이어를 붙이는 위치는 변경을 추가하는 요소의 숫자와 일치시키는 것이 아니라, 제공할 기능(또는 역할)마다 하나씩 만든다.

```html
<div class="bl_media bl_media__rev">
  <figure class="bl_media_imageWrapper"></figure>
  <div class="bl_media_body"></div>
</div>

<style>
  .bl_media__rev {
    flex-direction; row-reverse;
    text-align: right;
  }
  .bl_media__rev .bl_media_imageWrapper {
    margin-right: 0;
  }
  .bl_media__rev .bl_media_body {
    margin-right: 3.33333%;
  }
</style>
```
