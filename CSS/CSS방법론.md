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

> 참고    
> http://smacss.com/

## BEM

## OOCSS