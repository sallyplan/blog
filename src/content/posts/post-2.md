---
title: "한국형 웹 콘텐츠 접근성 지침 2.2(개정)"
date: 2023-05-04 
image: "/images/posts/img-policy.jpg"
categories: ["tech", "policy" , "a11y"]
authors: ["윤지현"]
tags: ["tech", "a11y"]
draft: false
---


2022년 12월 28일 한국형 웹 콘텐츠 접근성 지침 2.2(KS X OT0003:2022)이 새롭게 개정되어 안내드립니다.
기존 24개의 검사 항목에 9개의 검사 항목이 추가되어, 총 33개의 검사 항목으로 변경되었습니다.

<추가되는 신규 검사항목 목록>
  |  |  |  |
  | :--: | :--: | :--: |
  | 6.1.4 문자 단축키 | 6.5.1 단일 포인터 입력 지원 | 6.5.2 포인터 입력 취소 |
  | 6.5.3 레이블과 네임  | 6.5.4 동작기반 작동 | 6.4.4 고정된 참조 위치 정보 |
  | 7.2.2 찾기 쉬운 도움 정보 | 7.3.3 접근 가능한 인증  | 7.3.4 반복 입력 정보 |

출처 : WebWatch,  2023년 4월 11일, [http://www.webwatch.or.kr/Board/BoardViewDetail.asp?boardname=%uC790%uB8CC%uC2E4&bid=3350&page=1&bsh=&skey=&sval=&seq=2&MenuCD=650](http://www.webwatch.or.kr/Board/BoardViewDetail.asp?boardname=%uC790%uB8CC%uC2E4&bid=3350&page=1&bsh=&skey=&sval=&seq=2&MenuCD=650)

---
### 추가되는 신규 검사항목

##### 6.1.4 (문자 단축키) 문자 단축키는 오동작으로 인한 오류를 방지하여야 한다.
단일 문자 단축키(예: 대/소문자, 구두점, 기호 등 글자키나 숫자키 또는 특수문자키)를 제공하는 경우, 오류를 방지하기 위하여 다음 중 하나 이상을 충족해야 한다. 
1. 비활성화: 단축키를 끌 수 있는 방법을 제공해야 한다. 
2. 재설정: 한 개 이상의 기능키(예: Ctrl, Alt, Shift, Option, Command 등)를 조합하여 단축키를재설정할 수 있어야 한다.
3. 초점을 받은 경우에만 활성화: 사용자 인터페이스 구성요소(예: 폼 콘트롤, 링크, 콘텐츠 에디터 등)가 초점을 받은 경우에만 단축키가 활성화되어야 한다.

검사항목 6.1.4을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 음성명령 사용자가 입력을 위해 음성을 사용하는 것만으로도 의도하지 않게 단일 문자 단축키를실행시키는 오작동을 방지할 수 있다.
2. 손 사용이 원활하지 않은 사용자의 단일 문자 단축키 사용 오류를 방지할 수 있다.
3. 단일 문자 단축키 재설정 기능을 활용하여 익숙한 단축키로 변경할 수 있다.

##### 6.4.4 (고정된 참조 위치 정보) 전자출판문서 형식의 웹 페이지는 각 페이지로 이동할 수 있는 기능이 있어야 하고, 서식이나 플랫폼에 상관없이 참조 위치 정보를 일관되게 제공ㆍ유지해야 한다.
페이지 구분이 있는 전자출판문서 형식의 웹 페이지는 참조 위치 정보(예: 페이지 번호와 같은 페이지 구분자(pagebreak locators))를 제공해야 하고, 각 페이지로 이동할 수 있는 기능도 제공해야 한다. 
또한 콘텐츠의 확대/축소 등으로 서식이 변경되거나 플랫폼이 변경되어 참조 위치 정보가 사라지거나 일관된 위치에 제공ㆍ유지되지 않을 경우, 참조 위치 정보를 사용하여 콘텐츠의 특정 부분을 지칭해야 하는 상황(강의 등)에서 어려움이 있을 수 있기 때문에, 해당 참조 위치 정보는 서식이나 플랫폼이 변경되더라도 일관된 위치에 제공ㆍ유지해야 한다. 

검사항목 6.4.4을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 콘텐츠를 확대해서 사용하는 사용자(저시력, 전맹, 인지장애 등)와 확대하지 않고 사용하는
사용자가 페이지 구분자(페이지 번호 등)를 사용하여 동일한 페이지를 참조할 수 있게 된다.

#### 6.5 입력 방식

##### 6.5.1 (단일 포인터 입력 지원) 다중 포인터 또는 경로기반 동작을 통한 입력은 단일 포인터 입력으로도 조작할 수 있어야 한다.
두 개 이상의 손가락을 동시에 사용해야 하는 다중 포인터(예: 핀치 줌, 두 손가락 탭 등) 또는 쓸어 넘기기 등의 경로기반 동작(예: 스와이프, 끌기와 놓기, 그리기 등)을 통한 입력으로 작동하는 모든 기능은 단일 포인터 입력으로도 조작할 수 있어야 한다. 다만, 다음과 같은 경우에는 예외로 간주한다.
1. 필수적인 경우: 피아노 앱의 건반 동시누르기와 같은 다중 포인터나 서명과 같은 경로기반 동작을
통한 입력이 반드시 실행되어야 하는 경우
2. 운영체제나 사용자 에이전트(예: 브라우저), 보조기기 등이 지원하는 동작(예: 운영체제가 제공하는
손가락 두 개 끌어서 스크롤하기)을 통한 입력

검사항목 6.5.1을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 한 손가락 또는 스틱 포인팅 장치를 사용하거나 다중 포인터 동작을 통한 입력이 불가능하거나
어려운 사용자도 해당 장치나 동작을 통한 입력을 할 수 있다.
2. 손떨림, 시각장애 등으로 끌기 동작이나 복잡하거나 정교한 동작, 또는 그리기 동작을 통한
입력이 어려운 사용자도 해당 동작을 통한 입력을 적절하게 수행할 수 있다.
3. 복잡한 조작 과정이나 수단을 통한 입력을 이해하기 어려운 인지 또는 학습장애 사용자도 해당
조작 과정이나 수단을 통한 입력을 보다 쉽게 수행할 수 있다.

##### 6.5.2 (포인터 입력 취소) 단일 포인터 입력으로 실행되는 기능은 취소할 수 있어야 한다.
단일 포인터 입력으로 실행되는 기능은 해당 입력이 실수로 실행되는 것을 방지하기 위하여, 다음
중 하나 이상을 준수해야 한다. 
1. 다운 이벤트만으로 실행 금지: 기능은 다운 이벤트만으로 실행되지 않아야 한다. 
2. 중지 또는 실행취소: 기능은 업 이벤트에 완료되어야 하며, 실행 전에 중지시키거나 실행 후에
취소시킬 수 있어야 한다.
3. 되돌리기: 다운 이벤트로 실행된 모든 기능은 업 이벤트로 되돌릴 수 있어야 한다.
4. 필수적인 경우: 기능을 완료하는 데 다운 이벤트가 반드시 필요하다.
기능을 완료하는 데 다운 이벤트가 필수적인 경우로는 화면 피아노 건반, 슈팅게임 등이 있다.

검사항목 6.5.2을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 사용자가 잘못된 입력임을 인식했을 때 동작을 취소하거나 실행결과를 되돌릴 수 있다.
2. 우발적으로 오동작을 일으킬 확률을 줄여준다.

##### 6.5.3 (레이블과 네임) 텍스트 또는 텍스트 이미지가 포함된 레이블이 있는 사용자 인터페이스 구성요소는 시각적으로 표시되는 해당 텍스트를 네임에 포함해야 한다.
사용자 인터페이스 구성요소(예: 메뉴, 링크, 버튼 등)에서 시각적으로 표시되는 텍스트를 네임에 제
공하지 않은 경우 보조기술이 해당 사용자 인터페이스 구성요소를 인식할 수 없기 때문에, 네임에는
시각적으로 표시되는 텍스트를 제공해야 한다. 또한 네임과 텍스트를 다르게 제공한 경우 해당 정보
사용자(예: 음성명령 사용자)가 혼란을 겪을 수 있기 때문에, 네임과 텍스트는 동일하게 제공하는 것
이 좋으며, 동일하지 않게 제공할 경우 텍스트는 네임의 앞부분에 제시하는 것이 좋다. 단, 텍스트나
텍스트 이미지가 포함된 레이블이 없는 사용자 인터페이스 구성요소는 본 지침이 적용되지 않는다.
검사항목 6.5.3을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.
1. 음성 입력(speech-input) 사용자는 시각적으로 표시되는 텍스트를 사용하여 사용자 인터페이스
구성요소를 제어할 수 있다.
2. 텍스트 음성 변환(TTS: Text-to-Speech) 사용자는 보조기술을 통해 음성으로 전달되는 텍스트와
시각적으로 표시되는 텍스트가 일치하기 때문에 해당 사용자 인터페이스 구성요소를 혼란 없이
보다 쉽게 인지ㆍ활용할 수 있다.

##### 6.5.4 (동작기반 작동) 동작기반으로 작동하는 기능은 사용자 인터페이스 구성요소로 조작할 수 있고, 동작기반 기능을 비활성화할 수 있어야 한다.
사용자가 장치를 움직이거나 사용자의 움직임을 통하여 작동하는 기능(예: 흔들어서 실행 취소, 손동
작을 이용한 사진 촬영 등)은 사용자 인터페이스 구성요소로 조작할 수 있어야 하며, 의도하지 않는
동작으로 기능이 작동하는 것을 예방하기 위해 해당 기능을 비활성화할 수 있어야 한다. 다만, 다음
과 같은 경우에는 예외로 간주한다.
1. 접근성 지원 인터페이스: 동작이 접근성 지원 인터페이스를 통해 기능을 조작하는 데 사용되는
경우(예: 안구마우스)
2. 필수적인 경우: 동작이 기능의 실행에 반드시 필요하고, 동작의 실행에 대한 비활성화가 기능
자체를 무효화할 수 있는 경우(예: 만보기)
검사항목 6.5.4을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.
1. 장치가 고정되어 있거나 특정 동작을 행할 수 없는 사용자도 기능을 사용할 수 있다.
2. 정확한 동작을 할 수 없거나, 의도하지 않은 동작으로 기능이 실행되는 것을 방지할 수 있다.

##### 7.2.2 (찾기 쉬운 도움 정보) 도움 정보가 제공되는 경우, 각 페이지에서 동일한 상대적인 순서로 접근할 수 있어야 한다.
단일 페이지 웹 애플리케이션 또는 웹 페이지 세트에서 다음 도움 정보 중 하나 이상의 도움 정보가
제공되면, 최소한 하나의 도움 정보는 해당 페이지에서 동일한 상대적인 순서대로 제공되어야 한다.
1. 담당자 상세 연락처: 전화번호, 이메일, 운영시간 등
2. 담당자 연락 방법: 메신저, 채팅창, 게시판, SNS 등
3. 도움말 옵션: FAQ, 사용법 등
4. 자동화된 연결방법: 챗봇 등
도움 정보가 특정 페이지에서만 접근할 수 있는 등 각 페이지에서 상대적으로 동일한 위치에 제공되
지 않으면, 도움 정보의 위치를 찾기 어려운 사용자는 해당 도움 정보에 접근하기 어렵다. 

검사항목 7.2.2을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 도움 정보가 상대적으로 동일한 위치에 제공되지 않으면, 사용자는 원하는 도움 정보를 찾는 데
어려움을 겪을 수 있다. 그러나 도움 정보가 동일한 상대적인 순서대로 제공되면, 사용자는 해당
도움 정보에 보다 쉽게 접근할 수 있다.

##### 7.3.3 (접근 가능한 인증) 인증 과정은 인지 기능 테스트에만 의존해서는 안 된다.
사용자 로그인 등과 같은 인증 과정이 인지 기능 테스트(예: 로그인을 위한 비밀번호 입력, 터치스크
린 화면의 패턴 인식, 임의의 문자열 기억, 계산 수행, 특정 객체를 포함하고 있는 이미지 찾기 등)에
의존하는 경우, 인지 기능 테스트에 의존하지 않는 인증 방법을 적어도 하나 이상 제공해야 한다. 
인지 기능 테스트에 의존하지 않고 인증을 하기 위해서는 브라우저가 아이디/비밀번호를 저장할 수
있도록 마크업된 서식, 공개인증(OAuth: Open Authorization)를 통한 서드 파티, 신체(얼굴, 지문 등)나
물건(휴대폰, USB 등)을 이용한 인증 등을 이용할 수 있다. 다만, 이미 사용자 자신에게 익숙하여 별
도의 인지적인 노력을 필요로 하지 않는 사용자의 이름이나 이메일 주소, 전화번호는 인지 기능 테
스트로 간주하지 않는다.

검사항목 7.3.3을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.

1. 기억, 읽기, 숫자계산 등에 어려움이 있는 사용자도 인지 능력에 상관없이 인증 과정을 수행할 수
있다.

##### 7.3.4 (반복 입력 정보) 반복되는 입력 정보는 자동 입력 또는 선택 입력할 수 있어야 한다.
하나의 과정(process) 중 특정 단계(step)에서, 이전 단계에서 사용자가 이미 입력했거나 사용자에게
제공되었던 동일한 정보를 반복 입력해야 하는 경우, 반복되는 입력 정보는 자동으로 채워지거나 사
용자가 해당 정보를 선택 입력할 수 있어야 한다. 예를 들어, 온라인 구매에서 주문자와 수령자 주소
가 동일한 경우, 이전 단계에서 입력한 주문자 주소를 수령자 주소에 재입력 없이 선택하여 채울 수
있다. 다만, 패스워드와 같이 보안 목적 등으로 재입력이 필수적인 경우는 예외로 간주한다.
검사항목 7.3.4을 준수함으로써 얻을 수 있는 기대효과는 다음과 같다.
1. 기억 또는 인지 기능에 어려움을 겪는 사용자의 특정 정보에 대한 반복적인 입력으로 인한
스트레스와 실수 발생 가능성을 줄일 수 있다.
2. 움직임에 제약이 있는 사용자(예: 스위치 콘트롤 또는 음성 입력 사용자)의 텍스트 입력 부담을
줄여줄 수 있다.
---
[목록으로](/)
