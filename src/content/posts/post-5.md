---
title: "[javascript & jQuery] jQuery 버전 차이점"
date: 2023-07-12
# image: "https://utilitybend.com/imager/blog/77154/the-button-case_9d9edcf0c4ac6500f5ef73b033eea0d6.webp"
categories: ["tech"]
authors: ["오병직"]
tags: ["tech", "jQuery"]
draft: false
---

현재 1.xx 에서 3.xx 까지 jQuery 버전이 나와있다. 

#### 1.xx 는 구형 브라우저 버전을 대부분 지원하며 가장 안정적인 release 이다. 

주로 공공기관 사이트나 국가 관련 사이트 등 구형 브라우저를 사용하는 사용자가 많을 것으로 예측되는 사이트에 사용된다.

※ 이슈) 1.9 이전의 버전과 그 후의 버전 간의 호환성 문제가 발생하여 최신버전의 jQuery를 필요로 하는 플러그인 이나 스크립트를 삽입할 때 제대로 작동하지 않을 수 있다. 따라서 jQuery Migrate를 삽입하여 문제를 해결한다.


```html
 <script src="http://code.jquery.com/jquery-1.9.0.js"></script>
 <script src="http://code.jquery.com/jquery-migrate-1.2.1.js"></script>
```
출처: http://webdir.tistory.com/468 [WEBDIR]


동일한 내용을 CSS를 사용하면 다음과 같습니다.
참고: 사용자 정의 속성에는 항상 접두사로 이중 대시가  붙습니다.

#### 2.xx 부터는 익스의 6~8 버전을 지원하지 않는 등 간소화? 하여 1.xx 보다 용량이 적다. 익스 6~8 버전 보다 높은 버전을 사용할것으로 예상되는 사용자만 접속한다는 가정하에 이 버전들을 쓰는 것이 좋다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99B3E54B5C188AD907)

출처: https://en.wikipedia.org/wiki/JQuery#jQuery_methods

#### 3.xx은 최신 플러그인, 아작스 등 을 지원하는 버전이다. 

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99C427505C188B312D)


출처 : https://jintrue.tistory.com/entry/javascript-jQuery-jQuery-%EB%B2%84%EC%A0%84-%EC%B0%A8%EC%9D%B4%EC%A0%90

### JavaScript와 JQuery 코드 패턴


#### 모듈 패턴

##### 네임스페이스 정하기

```javascript
 // 1. 네임스페이스와 모듈 정의
var MyApp = {} // 전역 객체
MyApp.modules = {}


// 2. 공개범위와 비공개 범위 결정
MyApp.modules.libs = (function() {

	// 비공개 프로퍼티
	
	// 비공개 메서드

	return {
		// 공개 멤버
	}

})();
```
#### 네임스페이스의 존재여부 확인

##### 프로그램의 복잡도가 증가하면 네임스페이스도 중복될 수 있습니다. 따라서 다음과 같이 존재 여부를 확인합니다.


```javascript
// 문제: 기존의 MyApp을 덮어 쓸 위험성이 있다
var MyApp = {};

// 개선: 존재 여부 확인 후 생성
if (typeof MyApp === 'undefined') {
	MyApp = {};
}

// 더 잛게 작성하기
var MyApp = MyApp || {};
```

### 싱글톤과 같은 메서드 사용

```javascript
var module = (function () {

  // 은닉할 멤버
  var privateKey = 0;
  function privateMethod() {
    return ++privateKey;  // 클로저 방식의 접근
  }

  // 공개할 멤버
  return {
    publicKey: privateKey,
    publicMethod: function() {
      return privateMethod();
    }
  }
})();


console.log(module.publicMethod()); // 1 
console.log(module.publicMethod()); // 2
```

module에는 익명함수가 반환하는 객체가 할당되며 은닉된 멤버는 외부에서 접근할 수 없으나 publicMethod에의해 값을 변경할 수 있습니다. module.publicMethod()를 여러번 사용하는 경우 하나의 인스턴스로 privateKey를 사용하는 것과 같아 값이 매번 변경됩니다. 이것은 싱글톤의 동작과 같습니다. 단, module.publicKey와 같이 직접 찍어볼때는 문맥이 다르므로 0을 나타냅니다.

스크립트가 실행되면 '즉시실행함수' (IIFE)가 한번 실행되지만 ++privateKey처럼 사용될 때마다 매번 초기화 되는 것이 아닌 자신만의 어휘적 환경(렉시컬 환경)을 가집니다. 이것은 해당 시점의 관계되는 코드들이 유지되는것이죠.

### JQuery의 플러그인 추가 패턴

```javascript
(function($){ 
  $.fn.myPluginName = function() {
    // 추가 플러그인 구현
  }; 
})(jQuery);
```

`$.fn`은 `$.prototype`입니다. 플러그인 패턴을 작성하는 또 다른 방법으로 `$.extend()`를 사용하는 것입니다.

```javascript
((function($) {
	$.extend($.fn, {
		pluginType1: function() {
			// pluginType1 구현
		},
		pluginType2: function() {
			// pluginType2 구현
		}
	});
})(JQuery);
```


JQuery의 extend(첫번째_객체, {두번째_객체}, {...}...)는 두개 혹은 그 이상의 객체들을 첫번째 객체에 저장하여 병합, 확장할 수 있습니다.

#### 간단한 유틸리티 플러그인 패턴

```javascript
// (1) 다른 스크립트나 플러그인에서 제대로 닫히지
// 않을 경우를 대비해 세미콜론(;)을 함수앞에 넣음
;(function($, window, document, undefined) {

	var pluginName = 'defaultPluginName',
		defaults = {  // (2) 
			propertyName: "value"
		};

	// (3) 플러그인 생성자
	function Plugin(element, options) {
		this.element = element;

		// (4) 첫번째 빈 객체 {}는 플러그인 인스턴스에 대한 
		// 기본 옵션을 변겅시키지 않도록 하기 위함
		this.options = $.extend({}, defaults, options);
		this._defaults = defaults;
		this._name = pluginName;

		this.init();
	}

	// (5) 초기화
	Plugin.prototype.init = function() {
		// 인스턴스를 통해 DOM, options을 사용
		// this.element, this.options ...
	};

	// (6) new Plugin() 주변에 여러개의 인스턴스 생성을
	// 방지하기 위한 래퍼와 data 메소드를 이용해 cache 구성해
	// 한번 생성된 인스턴스는 더 이상 같은 인스턴스를 생성하지 않는다
	$.fn[pluginName] = function(options) {
		return this.each(function() {
			if (!$.data(this, 'plugin_' + pluginName)) {
				$.data(this, 'plugin_' + pluginName,
					new Plugin(this, options));
			}
		});
	}
})(JQuery, window, document);
```

### JQuery의 안티 패턴

#### 다중 호출 회피

```javascript
$('button.confirm').on('click', function() {
    // Do it once
    $('.modal').modal();
 
    // And once more
    $('.modal').addClass('active');
 
    // And again for good measure
    $('modal').css(...);
});
```

다중으로 제이쿼리 객체를 만들어내면 문제가 발생할 수 있습니다. 다음과 같이 체이닝을 사용하거나 캐싱을 사용합니다.

```javascript
$('button.confirm').on('click', function() {
    $('.modal')
        .modal()
        .addClass('active')
        .css(...);
});
```
캐싱을 사용하면 다음과 같이 사용해 DOM요소에 3번을 만들어내지 않고도 단 한번 접근할 수 있습니다.

```javascript
$('button.confirm').on('click', function() {
    // modal 변수를 통해 캐싱
    var modal = $('.modal');
 
    modal.modal();
    modal.addClass('active');
    modal.css(...);
});
```

#### 콜백 헬을 적절히 나누어서

한번에 모든 것을 하려기 보다는 데스크를 적절히 분배하는 것이 필요합니다.

```javascript
$('a.data').on('click', function() {
    var anchor = $(this);
    $(this).fadeOut(400, function() {
        $.ajax({
            // ...
            success: function(data) {
                anchor.fadeIn(400, function() {
                    // callback hell에 진입했습니다
                });
            }
        });
    });
});
```


각각의 역할을 분담해서 다음과 같이 개선할 수 있습니다.

```javascript
var updatePage = function(el, data) {
    // append fetched data to DOM
};
 
var fetch = function(ajaxOptions) {
    ajaxOptions = ajaxOptions || {
        // url: ...
        // dataType: ...
        success: updatePage
    };
 
    return $.ajax(ajaxOptions);
};
 
$('a.data').on('click', function() {
    $(this).fadeOut(400, fetch);
});
```

출처 : https://acaroom.net/ko/blog/youngdeok/javascript%EC%99%80-jquery-%EC%BD%94%EB%93%9C-%ED%8C%A8%ED%84%B4
