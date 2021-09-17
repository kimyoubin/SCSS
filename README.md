## CSS Preprocessor란?
CSS 전 처리기 SASS, LESS, STYLUS 같은 것들을 CSS 전 처리기라고 한다.
이것들을 CSS Preprocessor라고 한다.

## 어떻게 쓸까?
웹에서는 CSS만 동작한다. SASS, LESS, STYLUS 같은 전처리기는 직접 동작시킬수 없다.
전처리기로 먼저 작성한 뒤 웹에서 동작하는 CSS로 컴파일을 한다.

## SASS 와 SCSS의 차이점?
- {}(중괄호)와 ;(세미콜론)의 유무
- SASS는 들여쓰기로 유효범위를 구문하지만 SCSS는 {}로 유효범위를 구분한다.

## 컴파일하기
여러가지 있겠지만, VSCODE에서 컴파일 하는 방법을 사용하고 있다.
https://ossam5.tistory.com/90 참고

## SCSS 문법

### 중첩
상위 선택자의 중복을 피하고 좀더 편리하게 작성이 가능하다.

scss
```css
.section {
    width: 100%;
    ul {
        padding: 20px;
        li {
            width: 30%;
        }
    }
}
```
compiled to 
```css
.section { width: 100%; }
.section ul { padding: 20px; }
.section ul li { width: 30%; }
```
### 변수
반복적으로 사용되는 값을 변수로 지정할수 있다.
변수 앞에는 $를 붙여서 사용한다.
```
$변수이름: 속성값;
```
scss
```css
$mainColor: #e3ed2;
$width: 200px;

.section {
    width: $width;
    background-color: $mainColor;
}
```
compiled to
```
.section { width: 200px; background-color: #e3ed2; }
```
#### 변수의 유효범위
변수는 사용가능한 유효범위가 있다.
{}블록 내에서만 유효범위를 가진다.
.box1에서 선언된 $color 값은 .box2에서는 사용할 수 없다.
```css
.box1 {
    $color: #111;
    background-color: $color;
}
// error
.box2 {
    background-color: $color;
}
```

#### !global (전역설정)
!global을 사용하면 변수의 유효범위가 전역으로 설정된다.

scss
```css
.box1 {
    $color: #111 !global;
    background-color: $color;
}
// not error
.box2 {
    background-color: $color;
}
```
css
```
.box1 { background-color: #111; }
.box2 { background-color: #111; }
```
💥대신 이렇게 사용 할 시 이전에 같은 변수가 있을 경우 그 변수까지 덮어씌울 경우가 있으니 사용 시 주위하자.


### 가져오기 (Import)
```@import```는 여러 파일로 나눈뒤 그 파일을 가져와 사용하는 기능이다.
```css
@import "common.scss";
or
@import "common"
or
@import "common", "main";
```
