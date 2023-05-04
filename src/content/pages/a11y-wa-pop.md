---
title: "PC 팝업 예시"
meta_title: "셉템 | Web Accessibility"
draft: false
---

### popup

---

##### html
```html
<strong class="modal_title">홈페이지 검색 길잡이</strong>
	<div class="modal_content">
		<a href="#" role="text">first</a>
		<a href="#" role="text">팝업내용2</a>
		<a href="#" role="text">팝업내용3</a>
		<a href="#" role="text">팝업내용4</a>
	</div>
	<a href="#" class="modal_close">last</a>
</div>
<div class="modal_bg" style="display: none; top: 0px; height: 100%;"></div>
```
##### 스타일
```css
  .modal_bg{position:fixed !important;top:0;left:0;width:100% !important;height:100%;background:rgba(0,0,0,0.8) !important;z-index:998 !important}
  .modal_close{overflow:hidden;position:absolute;right:5px;top:5px;width:36px;height:36px;;text-indent:-9999px;}
  .modal_close:before,.modal_close:after{content:'';display:block;position:absolute;top:calc(50% - 8px);left:50%;width:1px;height:16px;background:#666;}
  .modal_close:before{transform:rotate(45deg)}
  .modal_close:after{transform:rotate(-45deg)}
  .modal_pop,.modal_bg{display:none;position:fixed !important}
  .modal_pop{overflow:hidden;top:50%;left:50%;padding:10px 15px 15px;box-sizing:border-box;background-color:#fff;z-index:999}
  .modal_title,.modal_content{box-sizing:border-box}
  .modal_title{display:block;margin-bottom:10px;height:36px;padding:6px 34px 0 0;border-bottom:1px solid #dfdfdf;line-height:100%;font-size:18px;color:#333}
```

##### 바닥 스크롤 막는 스크립트
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

##### 팝업위치 & 키보드제어
```javascript
function showLayer(self,obj){
	var $self = $(self);
	var $target = $($self.attr('href'));
	var _pWidth = $target.width()/2;
	var _pHeight = $target.height()/2;
	$('.modal_bg').show();

	scrollNone();

	$target.attr('tabindex', '0').show().focus();
	$(obj).css({"margin-top":"-"+ _pHeight +"px","margin-left":"-"+ _pWidth +"px"})
	$(obj).find(".modal_close").click(function(){
		hideLayer();
	});

	//키보드 포커스 modal popup 영역운영
	var
		firstElement = $target.find("div[tabindex='0'],a,input:not([disabled='disabled']),select,button,textarea").filter(':first'),
		lastElement = $target.find("div[tabindex='0'],a,input:not([disabled='disabled']),select,button,textarea").filter(':last');
	firstElement.off("keydown").on("keydown",function(b){
		if(b.keyCode == 9 && b.shiftKey){ //("keyCode==9"==Tab) -> Sthift+Tab
			b.preventDefault(); //preventDefault 동작취소
			lastElement.focus();
		}
	});

	lastElement.off("keydown").on("keydown",function(b){
		if(b.keyCode == 9 && b.shiftKey){
		} else if (b.keyCode == 9){
			b.preventDefault();
			firstElement.focus();
		}
	});

	function hideLayer(){
		$(obj).hide();
		$(obj).removeAttr('tabindex');
		$('.modal_bg').hide().css({'top':'0','height':'100%'});
		scrollBlock();
		$self.focus();
		$(this).off('click');
	}
}
```
