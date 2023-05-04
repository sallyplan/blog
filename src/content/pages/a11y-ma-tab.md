---
title: "모바일 탭 예시"
meta_title: "셉템 | Web Accessibility"
draft: false
---

### Tab
---

##### html
```html
<div id="contents" class="contents">
  <ul class="tablist" role="tablist">
    <li><a href="#tab1" class="active" role="tab" aria-selected="true"><span>탭 제목1</span></a></li>
    <li><a href="#tab2" role="tab" aria-selected="false"><span>탭 제목2</span></a></li>
    <li><a href="#tab3" role="tab" aria-selected="false"><span>탭 제목3</span></a></li>
    <li><a href="#tab4" role="tab" aria-selected="false"><span>탭 제목4</span></a></li>
  </ul>
  <ul class="tabcon">
    <li id="tab1" tabindex="0" aria-labelledby="탭 제목1" role="tabpanel" style="display:block;">탭 제목1 콘텐츠</li>
    <li id="tab2" tabindex="0" aria-labelledby="탭 제목2" role="tabpanel" style="display:none">탭 제목22 콘텐츠</li>
    <li id="tab3" tabindex="0" aria-labelledby="탭 제목3" role="tabpanel" style="display:none">탭 제목333 콘텐츠</li>
    <li id="tab4" tabindex="0" aria-labelledby="탭 제목4" role="tabpanel" style="display:none">탭 제목4444 콘텐츠</li>
  </ul>
</div>
```
##### 스타일
```css
  .tablist{position:relative;height:50px}
  .tablist li {float:left;width:25%;text-align:center;}
  .tablist li a {border:1px solid #ddd;border-left:0;display:inline-block;width:100%;height:100%;background:#efefef;line-height:50px;}
  .tablist li:first-child a{border-left:1px solid #ddd;}
  .tablist li a.active {background:#fff;color:blue;border-bottom:1px solid #fff;}
  .tabcon {padding:20px;border:1px solid #ddd;border-top:0}
```
##### 스크립트
```javascript
  $(function(){		

    var tabM = $(".tablist a");
    var tabCont = $(".tabcon > li");

    tabM.click(function(){
      var tabIdx = $(this).parent("li").index();
      tabM.removeClass('active');
      tabM.attr('aria-selected','false');
      $(this).addClass('active');
      $(this).attr('aria-selected','true');
      tabCont.hide();
      tabCont.each(function () {		
        tabCont.eq(tabIdx).show();
      });
    });
  });
```

