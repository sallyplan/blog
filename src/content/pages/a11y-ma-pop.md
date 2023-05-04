---
title: "모바일 팝업 예시"
meta_title: "셉템 | Web Accessibility"
draft: false
---

### popup

---
##### html
```html
<div id="contents" class="contents" aria-hidden="true">//aria-hidden="true"를 줘 팝업 내에서만 포커스가 돌도록 한다.
<a href="#" onclick="popupOpen()" role="button" title="OO팝업열기" class="popupOpen popup1">
팝업을 여는 버튼</a>
</div>

<div class="popup" style="display:block;">
	<div class="dimmed"></div>
	<div class="popupWrap">
		<h1><a href="#" role="text">팝업제목</a></h1> <!-- 현재 포커스 여기 -->
		<!-- iOS에서는 tabindex로 focus 안가는 이슈 있었음 a필수 -->
		<div class="popupCon"></div>
		<a href="#" onclick="popupClose('popup1')" role="button" title="팝업닫기">X</a>
	</div>
</div>
			</pre>

			<strong>모바일 팝업 닫힌 후</strong>
			<pre name="code" class="brush:html  highlight:[2, 3]">
<div id="contents" class="contents" aria-hidden="false">
	<a href="#" onclick="popupOpen()" role="button" title="OO팝업열기" class="popupOpen popup1">팝업을 여는 버튼</a>  <!-- 현재 포커스 여기 -->
</div>

<div class="popup" style="display:none;">
	<div class="dimmed"></div>
	<div class="popupWrap">
		<h1><a href="#" role="text">팝업제목</a></h1>
		<!-- iOS에서는 tabindex로 focus 안가는 이슈 있었음 a필수 -->
		<div class="popupCon">
			<span>1번</span><span>2번</span><span>3번</span><span>4번</span>
		</div>
		<a href="#" onclick="popupClose('popup1')" role="button" title="팝업닫기">X</a>
	</div>
</div>
```
##### 스타일
```css
  .popup {z-index:1000;position:fixed;top:50%;left:50%}
  .popupWrap {position:fixed;z-index:2000;background:#fff;transform: translate(-50%, -50%);}
  .popupWrap h1 {padding:5px 20px;background:#efefef;border-bottom:#ddd}
  .dimmed{position:fixed !important;top:0;left:0;width:100% !important;height:100%;background:rgba(0,0,0,0.8) !important;z-index:998 !important}
```
##### 스크립트
```javascript
var $popup = $('.popup');
var $content = $('#contents');

function popupOpen(){
	$popup.show();
	$popup.find('.popupWrap h1 > a').focus();
	$content.attr('aria-hidden','true');
}

function popupClose(name){
	var $name = $('.'+name);
	$popup.hide();
	$content.attr('aria-hidden','false');
	$name.focus();
}
```
