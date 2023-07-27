---
title: "스와이프 : 중앙 큰 카드 뒤로 숨겨진 카드가 있는 스와이프 스타일"
date: 2023-07-27
image: "https://s.uiinitiative.com/items/carousel-slider/screenshots/2.jpg"
categories: ["tech"]
authors: ["한은정"]
tags: ["tech", "swiper"]
draft: false
---

### 스와이프 : 중앙 큰 카드 뒤로 숨겨진 카드가 있는 스와이프 스타일

#### 참고로 한 샘플 스와이프

[Carousel Slider](https://uiinitiative.com/catalog/carousel-slider)

[키오스크](http://192.168.0.5:8888/NH/nh_kiosk/contents/html/KBNW1P.html)

---

#### 결과 스와이프
![](assets/2023-07-27-14-36-42.png)

[결과 콕뱅크 메인 스와이프](http://192.168.0.5:8888/NH/cok/project/pub/MN/UI-MN-0006.html)

---

#### 소스코드
```css
<style>
		.box{padding:0 20px;overflow:hidden} /* 페이지 기본 여백. overflow:hidden 넣지 않으면 cancelable=false 스크립트 에러 */ 
		.swiper-slide{width:72%;height:200px;border-radius:30px;box-shadow:0px 2px 5px 0px rgba(41, 58, 88, 0.5)} /* 중앙 사이즈 기준(1)으로 width 지정. 이밎 늘어날 경우 height:auto */
		.swiper{background-color:antiquewhite;padding-bottom:5px;}
		.swiper-pagination{z-index:30}
		/* .swiper-wrapper{} */
</style>
```

```html
<div class="box">
	<div class="swiper-container swiper">
		<div class="swiper-wrapper">
			<div class="swiper-slide" style="background-color:red"></div>
			<div class="swiper-slide" style="background-color:green"></div>
			<div class="swiper-slide" style="background-color:pink"></div>
			<div class="swiper-slide" style="background-color:blue"></div>
			<div class="swiper-slide" style="background-color:black"></div>
		</div>
		<div class="swiperNavigation">
			<div class="swiper-button-prev"></div>
			<div class="swiper-button-next"></div>
		</div>
		<div class="swiper-pagination"></div>
	</div>
</div>
```



```js
<script>
	var swiperName = '.swiper';
	var sideScale = .7 //양쪽 카드 비율, 중앙 카드는 1
	var sideOpa = .6 //양쪽 카드 투명도

	var sildeWidth = $(swiperName+' .swiper-slide').width();
	var sidePositon = ($(swiperName).width() - sildeWidth) / 2 - sildeWidth; //사이트 스케일 1일 경우 위치px
	var sideMargin = (sildeWidth - sildeWidth * sideScale)/2; //사이드 스케일에 따른 추가 여백 계산
	var sideX = -1 * (sideMargin + sidePositon);
	
	window.swiper = new Swiper(swiperName, {
		loop: true,
		slidesPerView: "auto",
		centeredSlides: true,
		watchSlidesProgress: true, //progress 값 받아오기
		loopPreventsSlide: false, //활성화되면 전환이 이미 진행 중일 때 Swiper 슬라이드 이전/다음 전환을 방지합니다( loop활성화되면 효과가 있음).
		loopFillGroupWithBlank: true,
		loopedSlides: 10,
		on: {
			progress: function () {
				var r = this.slides.length;
				for (var s = 0; s < r; s += 1) {
						const t = this.slides[s]
							, o = t.progress
							, i = Math.abs(o);
						let a = 1;
						i > 1 && (a = .3 * (i - 1) + 1);
						const l = o * a * sideX + "px"
							, c = 1 - (1 - sideScale) * i
							, u = r - Math.abs(Math.round(o));
						t.style.transform = `translateX(${l}) scale(${c})`,
						t.style.zIndex = u;
						const opa = Math.min(Math.max( 1-( (1 - sideOpa) * i), 0), 1);
						t.style.opacity = opa;
				}
			},
			setTransition: function (s) { //스와이프시 튕기는 현상 제거
				for (let t = 0; t < this.slides.length; t += 1) {
							const r = this.slides[t];
							r.style.transitionDuration = `${s}ms`;
					}
			},
		},	
		navigation: {
				nextEl: swiperName+" .swiper-button-next",
				prevEl: swiperName+" .swiper-button-prev"
		},
		pagination: {
				el: swiperName+" .swiper-pagination",
				clickable: true
		}
	});
</script>
```

해결되지 않은 문제점
1. 크롬에서 prev버튼을 여러번 누를 경우 이전 슬라이드가 불러와 지지 않음
2. box-shadow가 있을 경우 여백에 별도 처리가 필요함
