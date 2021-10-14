# CSS 방법론

## SMACSS (Scalable and Modular Architecture for CSS)
- CSS를 위한 확장 가능한 모듈식 구조
- CSS 규칙을 다섯 가지로 분류한 스타일 가이드
- 각 범주에는 그에 해당하는 특정한 지침이 존재

### 1. Base
- 기본 스타일 정의
- 요소,하위,자식 선택자를 사용하여 적용하며 클래스, ID 선택자는 사용하지 않음
- **!important** 사용할 필요가 없음   

```css
body, form {
    margin: 0;
    padding: 0;
}

a {
    color: #039;
}

a:hover {
    color: #03F;    
}
```

### 2. Layout
- 레이아웃 스타일 정의
- 클래스 기반 선택자에는 **l-** 접두사를 붙여 사용 

```css
#article {
    width: 80%;
    float: left;
}

#sidebar {
    width: 20%;
    float: right;
}

.l-fixed #article {
    width: 600px;
}

.l-fixed #sidebar {
    width: 200px;
}
```

### 3. Module
- 모듈 스타일 정의
- ID,요소 선택자를 사용하지 않고 클래스 선택자만 사용
- 다만, 예측할 수 있는 경우 요소 선택자와 함께 자식 또는 하위 선택자를 사용

```css
.module > h2 {
    padding: 5px;
}

.module span {
    padding: 5px;
}
```

### 4. State
- 상태 스타일 정의
- 상태는 다른 스타일을 덧붙이거나 재정의 하는 것 (active, hidden 등)
- 상태 스타일은 레이아웃 또는 모듈 스타일에 적용할 수 있음
- 일반적으로 **is-** 접두사를 붙여 사용 

```html
<div class="msg is-error">
  There is an error!
</div>
```

```css
.msg {
    color: black;
}

.msg .is-error {
    color: red;
}
```
### 5. Theme
- 테마 스타일 정의
- 테마를 고유한 스타일 set으로 분리하면 해당 스타일을 쉽게 재정의할 수 있음.

```css
// in module-name.css
.mod {
    border: 1px solid;
}

// in theme.css
.mod {
    border-color: blue;
}
```
<br>

> 참고    
> - http://smacss.com/  
> - https://wit.nts-corp.com/2015/04/16/3538

<br><hr><br>

## BEM (Block, Element, Modifier) 
- Block, Element, Modifier 구조로 분리한 스타일 가이드
- 태그 또는 ID 선택자 사용할 수 없음
- 

### 1. Block
- 그 자체로 의미있는 독립적인 것
- 상태가 아니라 목적을 설명하는 것
- 예시) header, container, menu, checkbox, input
  
```html
<!-- `header` block -->
<header class="header">
    <!-- Nested `logo` block -->
    <div class="logo"></div>

    <!-- Nested `search-form` block -->
    <form class="search-form"></form>
</header>
```

### 2. Element
- 독립적인 의미가 없으며 블록과 블록을 연결하는 일부
- 별도로 사용할 수 없음
- 예시) menu item, list item, checkbox caption, header title
- **'이중 밑줄(__)'** 을 사용하여 Block과 구분
- block 또는 element 명을 **'하이픈(-)'** 을 사용하여 구분 가능.
- 예시 구조 : **block-name__element-name**

```html
<!-- `search-form` block -->
<form class="search-form">
    <!-- `input` element in the `search-form` block -->
    <input class="search-form__input">

    <!-- `button` element in the `search-form` block -->
    <button class="search-form__button">Search</button>
</form>
```

- 요소는 서로 중첩될 수 있으며, 여러 중첩을 가질 수 있음.

```html
<!--
    Correct. The structure of the full element name follows the pattern:
    `block-name__element-name`
-->
<form class="search-form">
    <div class="search-form__content">
        <input class="search-form__input">

        <button class="search-form__button">Search</button>
    </div>
</form>

<!--
    Incorrect. The structure of the full element name doesn't follow the pattern:
    `block-name__element-name`
-->
<form class="search-form">
    <div class="search-form__content">
        <!-- Recommended: `search-form__input` or `search-form__content-input` -->
        <input class="search-form__content__input">

        <!-- Recommended: `search-form__button` or `search-form__content-button` -->
        <button class="search-form__content__button">Search</button>
    </div>
</form>
```

### 3. Modifier
- 블록이나 요소의 모양, 상태 또는 동작을 정의
- 예시) disabled, highlighted, checked, fixed, size big, color yellow
- **'단일 밑줄(_)'** 을 사용하여 Block 또는 Element와 구분
- 예시 구조 
  + **block-name_modifier-name**
  + **block-name__element-name_modifier-name**


```html
<!-- `search-form` block -->
<!-- The `search-form` block has the `focused` Boolean modifier -->
<form class="search-form search-form_focused">
    <input class="search-form__input">

    <!-- The `button` element has the `disabled` Boolean modifier -->
    <button class="search-form__button search-form__button_disabled">Search</button>
</form>
```
<br>

> 참고    
> - https://en.bem.info/methodology/quick-start/#introduction
> - http://getbem.com/introduction/
> - https://wit.nts-corp.com/2015/04/16/3538

## OOCSS