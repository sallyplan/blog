---
title: "스마트 버튼 시스템 만들기"
date: 2023-07-05
image: "https://utilitybend.com/imager/blog/77154/the-button-case_9d9edcf0c4ac6500f5ef73b033eea0d6.webp"
categories: ["tech"]
authors: ["한은정"]
tags: ["tech", "css"]
draft: false
---

CSS를 좋아한다면 이전에 사용자 정의 속성(일명 변수.CSS 대해 들어본 적이 있을 것입니다. 그럼에도 불구하고 많은 사람들이 CSS의 상수로 사용하는 것 같습니다. 이 기사에서는 이러한 사용자 정의 속성을 사용하여 스마트 시스템을 만들거나 CSS에서 부울로 사용하고 쉽게 점진적으로 향상시키는 방법에 대한 더 많은 통찰력을 제공하려고 합니다.


### 스마트 버튼 시스템 만들기

#### SCSS의 변수와 CSS

프론트엔드 개발자라면 SASS 또는 SCSS를 꽤 오랫동안 사용해 왔을 겁니다. SASS가 등장했을 때 유용했던 기술 중 하나는 변수의 사용이었습니다. CSS는 이미 "CSS3 변수"라고도하는 사용자 정의 속성의 형태로 꽤 오랫동안이 대안을 가지고 있습니다.

SASS 변수를 사용하여 body 태그의 배경 스타일을 'hotpink'로 지정하면 다음과 같습니다.

```CSS
$color-primary: hotpink;
body {
  background: $color-primary;
}
```

동일한 내용을 CSS를 사용하면 다음과 같습니다.
참고: 사용자 정의 속성에는 항상 접두사로 이중 대시가  붙습니다.

```CSS
:root {
  --color-primary: hotpink;
}
body {
  background: var(--color-primary);
}
```

여기에는 상당히 큰 차이가 있습니다. 사용자 정의 속성은 브라우저가 이해할 수 있다는 것입니다. 전처리기인 SASS와 달리 SASS 변수 시스템을 사용하는 경우 최종 코드가 다음과 같은 CSS 파일을 출력합니다.

```CSS
body {
  background: hotpink;
}
```

사용자 지정 속성에는 변수를 설정하고 상수로 사용하는 것보다 훨씬 더 많은 것이 있습니다. 사용자 지정 속성이 구축되는 방식에 따라 이를 사용하여 몇 가지 스마트 시스템을 만들 수 있습니다. 사용자 지정 속성을 사용할 경우의 몇 가지 이점은 다음과 같습니다. `:root`

- 범위를 지정할 수 있습니다
- 덮어쓸 수 있습니다
- 대체가 있을 수 있습니다
- 그들은 당신이 원하는 무엇이든 포함 할 수 있습니다 (!)
- JS로 제어 할 수 있습니다.

**중요한 점**은 CSS의 전반적인 성능에 영향을 미친다는 것입니다. 루트에 몇 가지 색상을 추가하는 것만으로는 큰 영향을 미치지 않지만 사용할 때 루트 수준에서 과도한 계산이나 끝없는 덮어쓰기로 과도하게 사용하지 않도록 주의하십시오.


##### 버튼 케이스 - SASS 변수 대 CSS 사용자 정의 속성

우리는 버튼을 스타일링 할 것입니다! 🥳 보다 구체적으로 다음 버튼은 다음과 같습니다.

![버튼 예시1](https://utilitybend.com/imager/blog/75766/Screenshot-2023-05-21-9.38.21-AM_cdd212fe916193b7417a09ec86e73888.webp)

여기에 불어오는 것도 없고, 멋진 디자인도 없고, 웹에서 꽤 많이 본 것처럼 4개의 버튼, 기본 및 보조 버튼, 각각 윤곽선 변형이 있습니다. 모두 호버링/포커스 상태도 있습니다.

![버튼 예시2](https://utilitybend.com/imager/blog/75820/Screenshot-2023-05-21-9.39.18-AM_cdd212fe916193b7417a09ec86e73888.webp)


이 글에서 요점을 밝히기 위해 버튼에는 패딩 및 테두리 반경에 대한 몇 가지 기본 스타일이 있으며 이 글의 나머지 부분에서는 반복하지 않을 것입니다.

```CSS
button {
  padding: 13px 20px;
  border-radius: 5px;
  font-size: 1.1rem;
  cursor: pointer;
}
```

#### SASS 변수를 사용하여 단추 스타일 지정

버튼을 색칠하기 위해 SASS 변수를 사용할 때 일종의 믹스 인을 사용할 것입니다. 그러나 이것은 "SASS 튜토리얼"이 아니기 때문에 그것이 생성하는 출력에 대해 이야기하고 싶습니다. SASS 변수를 사용하여 이러한 버튼을 만들면 색상을 지정하면 다음과 같은 출력이 생성됩니다 (큰 코드 덩어리가 나타납니다).

```css
button {
  background: black;
  border: 2px solid black;
  color: white;
}

button:is(:hover, :focus) {
  background: DarkCyan;
  border-color: DarkCyan;
}

button.secondary {
  background: deeppink;
  border-color: deeppink;
}

button.secondary:is(:hover, :focus) {
  background: purple;
  border-color: purple;
}
button.outline {
  background: transparent;
  color: black;
}

button.outline:is(:hover, :focus) {
  border-color: DarkCyan;
  color: DarkCyan;
}

button.outline.secondary {
  color: deeppink;
  border-color: deeppink
}

button.outline.secondary:is(:hover, :focus) {
  background: transparent;
  border-color: purple;
  color: purple;
}
```

따라서 SCSS 변수를 사용하여 믹스인과 같은 스마트한 것을 사용했을 수도 있지만 처리된 코드는 지속적으로 색상을 덮어쓰고 그 특이성을 올바르게 얻음으로써 매우 반복적으로 보입니다. 우리는 더 잘할 수 있습니다! 따라서 새로 시작하여 동일한 스타일을 적용하되 이번에는 사용자 지정 속성을 사용하겠습니다.

#### 사용자 지정 속성을 사용하여 단추 스타일 지정
전처리기 대신 CSS를 사용하여 다시 작성해 보겠습니다. 버튼을 보면 한 가지 공통점이 있다는 것을 알 수 있습니다. 이제 사용자 지정 속성을 사용하여 "채워진 버튼"을 위한 스마트 시스템을 만들어 보겠습니다.


```css
button {
  --color: black;
  background: var(--color);
  border: 2px solid var(--color);
  color: white;
}

button:is(:hover, :focus) {
  --color: DarkCyan;
}

button.secondary {
  --color: deeppink;
}

button.secondary:is(:hover, :focus) {
  --color: purple;
}
```

우리가 방금 무엇을 했습니까? 이름이 지정된 사용자 지정 속성을 만들고 --color이를 버튼 요소로 범위 지정했습니다. 그런 다음 이러한 사용자 지정 속성을 읽을 수 있도록 배경 및 테두리 색상을 업데이트했습니다. 사용자 지정 속성을 덮어쓸 수 있으므로 테두리와 배경을 다시 선언하는 대신 사용자 지정 속성만 업데이트합니다. 이렇게 하면 CSS 크기가 크게 줄어듭니다.

우리는 아직 폴백(대체제)을 도입하지 않았습니다. 이 경우에는 필요하지 않을 수 있지만 튜토리얼을 위해 이렇게 합시다. 변수 를 읽고 --color사용할 수 없을 때 기본 색상으로 폴백하도록 하여 기본 버튼을 업데이트해 보겠습니다. 의 각 사용에 폴백을 추가하는 대신 var()단일 사용자 정의 속성을 사용하여 이를 처리할 수 있습니다. 지금은 해당 사용자 지정 속성에 밑줄을 붙일 것입니다. 이전에는 JavaScript에서 개인 변수를 나타내는 데 사용되었고 물건(아, 좋은 옛날)이었기 const때문에 이것은 단지 규칙일 뿐입니다. let귀하의 스타일에 맞는 방식으로 이러한 사항을 자유롭게 표시하십시오. 코드의 업데이트된 부분:

```css
button {
  --_color: var(--color, black);
  background: var(--_color);
  border: 2px solid var(--_color);
  color: white;
}
```

엄청난! 이제 우리가 해야 할 일은 버튼의 개요 버전을 만드는 것입니다. 우리는 채워진 버튼에 대한 사용자 정의 속성을 사용하여 이미 모든 도구를 사용하고 있습니다. 개요 버튼의 유일한 차이점은 배경이 투명하고 배경색 대신 텍스트 색상을 변경한다는 것입니다. 이제 우리는 이것을 실현하기 위한 지름길을 취할 수 있습니다.

```css
button.outline {
  background: transparent;
  color: var(--_color);
}
```

#### 버튼 케이스 - 사용자 지정 속성의 향상된 사용
저 같으면 쉽게 포기하지 않습니다. 어떻게든 코드를 더 스마트하게 만들 수 있을지 궁금했습니다. 호버 및 초점 색상에 대한 두 번째 사용자 지정 속성을 도입하여 4개의 버튼을 만드는 더 스마트한 방법이 있습니다. 코드를 17줄로 줄이고 새로운 색상 변형을 덜 중복되게 만듭니다. 다음은 전체 코드입니다.

```css
button {
  --_color: var(--color, black);
  background: var(--_color);
  border: 2px solid var(--_color);
  color: white;
}

button.secondary {
  --color: deeppink;
  --hoverColor: purple;
}

button.outline {
  background: transparent;
  color: var(--_color);
}

button:is(:hover, :focus) {
  --color: var(--hoverColor, DarkCyan);
}
```

따라서 호버 상태를 다시 선언하는 대신 사용자 --hoverColor지정 속성을 읽고 기본 버튼 호버 상태로 폴백하는 버튼 요소에 대한 일반 호버를 추가했습니다.


여기에는 우리가 해결해야 할 몇 가지 장점과 단점이 있습니다.

#### 거꾸로...

이와 같이 버튼의 스타일을 지정하면 버튼의 채워진 버전과 윤곽선 버전이 모두 있는 새로운 색상 변형을 쉽게 만들 수 있습니다. 예를 들어 새 주황색 변형을 추가하려는 경우 보조 버튼 옆에 다음을 추가할 수 있습니다.

```css
button.orange {
  --color: orange;
  --hoverColor: darkorange;
}
```

#### 그리고 단점...

버튼의 호버 상태가 스타일시트에서 마지막에 와야 하므로 여기에서 약간의 특이성 위험 영역에 들어가고 있습니다. 캐스케이드 레이어 내부에 기본 버튼 스타일을 추가하여 이를 방지하는 방법이 있습니다 . 이것이 노력할 가치가 있는지 여부는 스타일을 지정할 이러한 버튼의 양에 따라 다르며 완전히 주관적입니다. 제가 이렇게 다양한 방법을 제시하는 이유는 여러분이 선택할 수 있고 자신에게 가장 적합한 접근법을 신중하게 계획하기 때문입니다.

```css
/* default buttons layer */
@layer buttons {
  button {
    --_color: var(--color, black);
    background: var(--_color);
    border: 2px solid var(--_color);
    color: white;
  }

  button.secondary {
    --color: deeppink;
    --hoverColor: purple;
  }
}

/* Non layered styles come last */
button.outline {
  background: transparent;
  color: var(--_color);
}

button:is(:hover, :focus) {
  --color: var(--hoverColor, DarkCyan);
}

/* then in another file or lower in the file, you can add them to the layer */
@layer buttons {
  button.orange {
    --color: orange;
    --hoverColor: darkorange;
  }
}
```

#### 그렇다면 여전히 사용자 지정 속성을 사용하지 않습니까?

맞춤 속성은 일부 스마트 디자인 시스템을 만드는 데 실제로 도움이 될 수 있다고 생각합니다. 그리고 당신이 그것들을 많이 사용하지 않았다면, 나는 완전히 이해합니다. 나도 파티에 늦었어...
하지만 일단 그것들을 사용하는 습관을 기르기 시작하면 완전히 새로운 CSS 작성의 세계가 열리는 것과 같다. 그래서 나는 당신이 그들과 놀기를 강력히 권장합니다. :has()내 프레젠테이션에서는 점진적인 개선과 컨테이너 스타일 쿼리를 추가하고 혼합에 추가하여 부울로 사용하는 등 사용 방법에 대해 훨씬 더 많은 방법을 살펴봅니다 . 적은 비용으로 더 많은 작업을 수행하는 스마트 코드를 작성하여 작업 흐름에 큰 이점을 줄 수 있습니다. 이 작은 버튼 케이스가 "사용자 지정 속성을 생각"하는 데 정말 도움이 되었고 앞으로의 프로젝트를 향상시킬 수 있기를 바랍니다.

---

출처 : [utilitybend.blog](https://utilitybend.com/blog/the-button-case-using-custom-properties-for-a-smart-button-system)
참고글 : [iodigital.tech](https://techhub.iodigital.com/articles/going-beyond-constants-with-custom-properties)
