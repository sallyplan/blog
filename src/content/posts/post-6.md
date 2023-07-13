---
title: "Chrome 개발자 도구로 디버깅하기 - 디버깅, breakpoint 개념 및 사용"
date: 2023-07-13
image: "https://t1.daumcdn.net/cfile/tistory/275121415865DB5920"
categories: ["tech"]
authors: ["이성범"]
tags: ["tech"]
draft: false
---

### Chrome 개발자 도구로 디버깅하기 - 디버깅, breakpoint 개념 및 사용

좀 더 복잡한 코드를 작성하기 전에, 디버깅이란 것에 대해 이야기해봅시다.

디버깅(debugging)은 스크립트 내 에러를 검출해 제거하는 일련의 과정을 의미합니다. 모던 브라우저와 호스트 환경 대부분은 개발자 도구 안에 UI 형태로 디버깅 툴을 구비해 놓습니다. 디버깅 툴을 사용하면 디버깅이 훨씬 쉬워지고, 실행 단계마다 어떤 일이 일어나는지를 코드 단위로 추적할 수 있습니다.

이 글에선 Chrome 브라우저에서 제공하는 디버깅 툴을 사용하도록 하겠습니다. 기능이 다양하고, Chrome에 익숙해지면 다른 브라우저에서 지원하는 디버깅 툴은 쉽게 익힐 수 있기 때문입니다.

#### ‘Sources’ 패널

Chrome 버전에 따라 보이는 화면은 약간씩 다를 수 있습니다. 하지만 버전이 바뀌어도 구성은 크게 바뀌지 않기 때문에 화면 캡쳐본과 함께 설명을 이어나가겠습니다.

- Chrome을 사용해 예시 페이지를 엽니다.
- `F12 (MacOS: Cmd+Opt+I)`를 눌러 개발자 도구를 엽니다.
- `Sources` 탭을 클릭해 `Sources` 패널(panel)을 엽니다.

Sources 패널을 처음 열었다면 아래와 같은 화면이 보일 겁니다.


![이미지1](https://blog.kakaocdn.net/dn/E6YSH/btrpW7HH2CP/QKOMJFpJ5j1r5EQuSizkFK/img.png)

`Sources`에서 `navigator`를 클릭합니다.
`Sources` 패널은 크게 세 개의 영역으로 구성됩니다.


- 파일 탐색 영역 
- 코드 에디터 영역
- 자바스크립트 디버깅 영역

![이미지2](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbTKir6%2FbtrpU3FKWdU%2FP3p4bVnBL5ZSHBpGQZMgA1%2Fimg.png)
![이미지3](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbeMS3g%2FbtrpU2GROAt%2FXDoipw6mN6bnflYzfKJc7k%2Fimg.png)
![이미지4](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTvjnV%2Fbtrp2BOymRs%2FAxrcfDnZWY2Qy6rLwmvjL0%2Fimg.png)

---

#### 중단점 사용

- 중단점 설정을 하고자 하는 파일의 코드 라인의 줄 번호를 클릭합니다.
- 중단점: 자바스크립트 실행이 중단되는 코드 내 지점을 의미합니다.
- 중단점 이용시 실행이 중지된 시점에 변수가 어떤 값을 담고 있는지 알 수 있고 중지된 시점을 기준으로 명령어 실행이 가능합니다. 즉, 디버깅이 가능해집니다.

![이미지5](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcUg8s8%2Fbtrp5zJvxU2%2F7XANeQ04acPFAxKgCZ2KPk%2Fimg.png)
![이미지6](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FANFCp%2FbtrpWyy4NvD%2FTKMTpU9AZkO6x3AejxvRe1%2Fimg.png)


---

#### debugger 명령어

 - debugger 명령어를 사용하면 소스코드에서 중단점을 설정하는 수고를 덜 수 있습니다.
 - 중단점을 기준으로 코드를 실행하면 중단점마다 코드가 중단이 됩니다.<br>
![이미지7](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsNf2k%2Fbtrp0adDdF5%2Fzv7EFnqJOkpXRwQD5hSSv1%2Fimg.png)
>디버깅 영역에서 역할
>>Watch: 표현식을 평가하고 결과를 보여줍니다.<br>
>>Call Stack: 코드를 해당 중단점으로 안내한 실행 경로를 역순으로 표시합니다.<br>
>>Scope: 현재 정의된 모든 변수를 출력합니다.<br>

---

#### 실행 추적

- Resume: 실행을 재개합니다. 추가 중단점이 없는 경우, 실행이 죽 이어지고 디버거는 동작하지 않습니다.<br>
![이미지8](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkPp3A%2Fbtrp00awC88%2Fj5W2kSY29M4pTK4O9eMS20%2Fimg.png)

- Step: 다음 명령어를 실행합니다. Step 버튼을 계속 누르면 스크립트 전체를 문 단위로 하나하나 실행할 수 있습니다.<br>
![이미지9](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrNA5k%2Fbtrp1Inc1ZW%2Fwu5SdLFt4KAytlC2Ob7Rl0%2Fimg.png)

- Step over: 다음 명령어를 실행하되, 함수 안으로 들어가지는 않습니다.<br>
![이미지10](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FWZSQR%2FbtrpZ9eJ5U3%2FzLGhlJL4flZwe5RTdVnATk%2Fimg.png)

- Step into: 'Step'과 유사하지만 비동기 함수 호출에서 'Step'과 다르게 동작합니다. 비동기 동작을 담당하는 코드로 진입하고, 필요시 비동기 동작이 완료될 때까지 대기합니다. <br>
![이미지11](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTBjym%2Fbtrp09E1ehs%2FldNxxusmkcNAs70hou0ZLk%2Fimg.png)

- Step out: 실행 중인 함수의 실행이 끝날때 까지 실행을 계속합니다. 현재 실행 중인 함수의 실행을 계속 이어가다가 함수 본문 마지막 줄에서 실행을 멈춥니다.<br>
![이미지12](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F5krW6%2Fbtrp5ABZvfa%2FxnvwvzzFRIAKFTPib346XK%2Fimg.png)



---

출처 : [amind.blog](https://amind2020.tistory.com/149)
참고글 : [javascript.info](https://ko.javascript.info/debugging-chrome)
