---
title: "UX 중심의 webview를 위한 세팅"
date: 2023-09-01 
image: "/images/posts/img-webview-app.jpg"
categories: ["tech"]
authors: ["김범석"]
tags: ["tech", "WebView"]
draft: false
---



출처 : shylog,  2020년 02월 04일, [https://shylog.com/settings-for-a-more-complete-webview/](https://shylog.com/settings-for-a-more-complete-webview/)<br>

- [WebView란](#aria)
1. [pinch to zoom & zoom-in action](#zoom)
2. [버튼 Touch 시 나오는 음영 지우기](#touch)
3. [test select 안되게 하기](#select)
4. [link Long touch 막기](#long)
5. [over scroll시 흰 영역이나 background가 나오는 경우](#scroll)
6. [iphoneX와 같이 화면이 Web 영역을 침범할 경우](#iphoneX)

### WebView <a id="aria" href="#aria">#</a>


>웹뷰(WebView)란 프레임워크에 내장된 웹 브라우저 컴포넌트로 뷰(View)의 형태로 앱에 임베딩하는 것을 말한다.즉, 앱 안에 HTML iframe을 넣어놓은 것이다.웹 페이지를 보기 위해서 혹은 앱 안에서 HTML을 호출하여 앱을 구현하는 하이브리드 형태의 애을 개발하는데에도 많이 사용된다.

#### 1.pinch to zoom & zoom-in action <a id="zoom" href="#zoom">#</a>
![Alt text](/public/images/post-9/pinch-to-zoom-example.jpg "pinch to zoom example")
위 이미지의 오른쪽 처럼 webview에서 더블 클릭을 하거나 pinch to zoom을 이용해서 확대를 할 수 있다면  기본적으로 앱에서 zoom을 이용한 커뮤니케이션을 하는 경우가 많이 없기 때문에 당연히 webview에서도 막는 것이 좋다.
```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1.0, minimum-scale=1, user-scalable=0">
```

하지만 ios 버전이 올라가면서 반드시 확대해야 하는 유저들의 경험을 해칠 수 있다고 판단했기 때문에 더 이상 safari에서는 viewport를 통해 브라우저를 확대하지 못하게 하는 방법이 불가능하게 되었다.  이에 따라 삼성 브라우저 등 몇몇 브라우저들도 마찬가지로 제어가 불가능하게 되었다.
```javascript
// 자바스크립트로 기본 핀치 줌 제어
// 상황에 따라 wheel, touchstart 등 다른 이벤트도 막아야 할 수 있다.
export default function preventZoom() {
  function listener(event: TouchEvent) {
    // 핀치 줌의 경우 두 개 이상의 이벤트가 발생한다.
    if (event.touches.length > 1) {
      event.preventDefault();
    }
  }

  document.addEventListener('touchmove', listener, { passive: false });
}
preventZoom();
```
또는
```css
/* css로 핀치 줌 제어, body 혹은 자동으로 scale 되는 대상에 적용 */
.preventTouch {
  touch-action: none;
}
```
- 
---

#### 2.버튼 Touch 시 나오는 음영 지우기 <a id="touch" href="#touch">#</a>
![Alt text](/public/images/post-9/shadow-example.jpg "shadow example")
webview에서 버튼을 클릭 했을 때 오른쪽 이미지와 같이 음영이 생긴다. 머터리얼 디자인처럼 각진 모양의 버튼에서는 크게 눈에 띄지 않지만 모서리가 둥근 버튼이나 텍스트로 된 a link의 경우 깔끔하지 않은 화면을 만나볼 수 있다.
```css
* {
  -webkit-tap-highlight-color:rgba(255,255,255,0);
}
```

**안드로이드 일 경우**
```CSS
* {
  outline: none;
  -webkit-tap-highlight-color:rgba(0,0,0,0);
  -webkit-tap-highlight-color:rgba(255,255,255,0);
}
```
- 속성을 추가해둬야 함.

위의 속성 때문에 선택 음영이 나오는 것인데 해당 속성에 color 값을 넣으면 자신이 의도한 색상으로 음영을 만들 수도 있다. 위 속성의 rgba(255, 255, 255, 0) 에서 중요한 포인트는 투명도를 0으로 하는 것이다. (transparent를 넣으면 투명하게 처리할 수 있으나 구형의 안드로이드에서는 정상적으로 동작 안할 수 있다.)<br><br>
위 3개를 통해 zoom과 관련된 내용들을 막을 수 있다.<br><br>

**`*` 을 이용해서 현재 모든 Tag들에 일괄 적용 했지만 특정 부분에서만 해당 속성을 추가해서 특정 Tag에서만 동작하지 않게 할 수 있다.**

---
#### 3.test select 안되게 하기 <a id="select" href="#select">#</a>
![Alt text](/public/images/post-9/test-select-example.jpg "test select example")

```css
* {
	user-select: none;
}
```
위의 `user-select` 를 이용한다면 유저가 더블클릭 등을 이용하여 글자를 선택하는 것을 막을 수 있다
`user-select: auto | all | none | text` 총 4개의 값이 존재하며 아래와 같다.

- `auto` : default 값으로 브라우저 허용 시 텍스트 선택 가능
- `all` : 더블클릭이 아닌 클릭만으로도 선택이 가능
- `none` : 텍스트 선택이 안됨
- `text` : 텍스트 선택이 가능

---
#### 4. link Long touch 막기 <a id="long" href="#long">#</a>
![Alt text](/public/images/post-9/long-touch-example.jpg "long-touch-example")
`a` 태그 와 같은 링크태그는 `long touch(press)` 할 경우 위와 같이 나오게 된다. 유저에게 불필요한 정보를 노출하는 것은 유저 경험 뿐만 아니라 보안적인 측면에서도 좋지 않다
```css
* {
  -webkit-touch-callout: none;
}
```
위 속성을 통해 팝업이나 액션시트를 제어할 수 있다. 아래와 같은 값들을 지정해 줄 수 있다.
```css
/* Keyword values */
-webkit-touch-callout: default;
-webkit-touch-callout: none;

/* Global values */
-webkit-touch-callout: initial;
-webkit-touch-callout: inherit;
-webkit-touch-callout: unset;
```
**참고1. 해당 부분도 AND와 IOS 자체 설정으로 막을 수 있다.**

---
#### 5. over scroll시 흰 영역이나 background가 나오는 경우<a id="scroll" href="#scroll">#</a>
![Alt text](/public/images/post-9/scroll-example.jpg "scroll-example")
PC와 다르게 모바일의 경우 시작과 끝 시점에서 스크롤을 하더라도 스크롤이 되었다가 원상복구 되는 Spring(?) 과 같은 유저 경험을 제공하고 있다. 유저 경험 상 Spring과 같은 Action은 매우 좋으나 별도의 대응이 없다면 왼쪽 위와 같이 흰 화면을 맛보게 되고 이는 이질감을 줄 수 있다. 
```html
<body style='background: gray;'>
</body>
```
위와 같이 body에 background color를 지정해주면 오버 스크롤링 되는 상황에서 지정한 배경 색상이 나오게 된다.

만약 제일 상단과 제일 하단이 보여줘야할 background가 다르다면 아래와 같이 설정하면 좋다.
```html
<style>
  .backgroundTop {
		position: fixed;
  	width: 100%;
  	height: 50%;
  	background: gray;
  	z-index: -10;
  	top: 0;    
  }
  .backgroundBottom {
		position: fixed;
  	width: 100%;
  	height: 50%;
  	background: yellow;
  	z-index: -10;
  	bottom: 0;
  }
</style>
<body>
  <div class='backgroundTop'></div>
  <div class='backgroundBottom'></div>
</body>
```

position: fixed 를 통해 위 아래를 고정한 후에 background color를 각각 지정해주면 보다 자연스러운 화면을 접할 수 있다.

**참고1. 해당 부분도 AND와 IOS 자체 설정으로 막을 수 있다.**

---
#### 6. iphoneX와 같이 화면이 Web 영역을 침범할 경우<a id="iphoneX" href="#iphoneX">#</a>
![Alt text](/public/images/post-9/web-Invasion-example.jpg "web-Invasion-example")
![Alt text](/public/images/post-9/web-Invasion-example2.jpg "web-Invasion-example")



 노치(notch)가 존재 아이폰X 대응사례,[https://wit.nts-corp.com/2019/10/24/5731](https://wit.nts-corp.com/2019/10/24/5731)

아이폰 X의 경우 하단 저 검은 길다란 바와 겹치는 issue가 생길 수 있다. 또한 상하단에 생기는 브라우저 버튼들에 가려지는 상황도 생길 수 있는데 이를 대응하는 방법이 있다.

```html
<meta name="viewport" content="viewport-fit=cover">
<style>
  .floating-button {
    padding-top: env(safe-area-inset-bottom);
  }
</style>
```
먼저 뷰포트에 전체 화면을 사용한다는 속성을 추가하면 브라우저 상 하단의 영역도 사용하게 된다. 이런 상황에서 safe-area-inset 속성들을 추가하면 된다.

주의할 점은 ios 버전마다 각기 다른 속성을 사용해야 한다.

```css
env(safe-area-inset-bottom); // IOS 11.0 이상 (신)
constant(safe-area-inset-bottom); // IOS 11.0 버전 (구)
```
safe-area-inset의 기본값이 있어 값을 수정을 해야한다면 calc를 이용하여 조절해주면 된다.

```css
padding-bottom: calc(env(safe-area-inset-bottom) - 5px);
padding-bottom: calc(constant(safe-area-inset-button) - 5px);
```


![Alt text](/public/images/post-9/env-support.jpg "env-support")
env() 지원 범위,[https://caniuse.com/?search=env1](https://caniuse.com/?search=env)


**Constant & env 둘다 추가해야 ios 구, 신버전 대응이 가능하다.**


---
[목록으로](/)
