---
title:  "target=_blank을 쓸 때 유의할 점"
excerpt: "(이었던것)"

categories:
  - Web
tags:
  - Browser

last_modified_at: 2021-11-08T17:00:00-18:00:00

---

개발자들은 새 탭이나 새 창으로 특정 페이지를 여는 링크를 구현할 때, 아래와 같이 **target="_blank"** 옵션을 이용하곤 한다.  
  하지만 이 방식에는 2가지 문제가 있었다. 오늘은 이 2가지 문제에 대해서 알아보려고 한다.
```html
  <a href="https://minje0204.github.io/" target="_blank">
	Made by minje0204 </a>
```
  
## target="_blank"의 문제점  

**target="_blank"** 에는 2가지 문제가 있는데 한가지는 **tab-napping**이고 다른 한가지는 

  
### 1.  보안상 취약점이 생긴다.
**target="_blank"** 가 사용된 a tag는 사용자가 클릭하면 **새 탭**에서 링크된 페이지가 열린다. 여기서, 해당 링크를 연 윈도우가 **window.opener**에 저장된다. 

>**Window.opener**  
>Window 인터페이스의 **opener 속성**은 open()을 사용해 현재 창을 열었던 창의 참조를 반환합니다.  
>  
>예제로 설명하자면, 창 A가 창 B를 열었을 때 B.opener는 A를 반환합니다.  
>**ref by. [Mozilia|MDN](https://developer.mozilla.org/ko/docs/Web/API/Window/opener)**

그리고 **window.opener**를 사용하면 새 페이지에서 이전 윈도우를 마음대로 조작할 수 있다. 예를 들면, `window.opener.location = new malicious URL` 와 같이 악성 url로 리다이렉트 시킬 수 도 있다.

### 2. 퍼포먼스가 떨어질 수 있다  

**target="_blank"** 가 사용된 링크에 의해 열린 링크된 페이지는 링크를 건 페이지와 같은 프로세스를 통해서 실행된다. 그래서 main-thread에서 진행중이던 모든 작업들이 순간적으로 disrupt 될 수 있다. 

>현재는 target="blank"로 이 문제를 재현 할 수 없지만, window.open으로는 가능하다. 심심하면 해보시길...

## 문제 해결방법(이었던 것)

**예시 코드**
  ```
  <a
	href="https://minje0204.github.io/"
	target="_blank"
	rel="_noreferrer noopener"
>
	Made by minje0204
</a>
  ```
위 두가지 문제 때문에 보통 **_blank 옵션**으로 새창에서 링크를 띄울 경우 위와 같이 **rel="_noreferrer noopener"** 를 보통 사용해왔다.

>**noreferrer**   
>브라우저가 링크를 건 페이지의 주소와 같은 정보를 Referer: HTTP 헤더에 리퍼러(referer 또는 referrer)로 송신하지 않습니다.    
>**noopener**  
>noopener(노오프너)를 지정하면, 링크된 페이지에서 window.opener을 사용해서 링크를 건 페이지를 참조(reference)할 수 없게 됩니다. 더불어 링크된 페이지와 링크를 건 페이지는 별개의 프로세스로 취급

## 이제는 상관없다?

그럼 첫번째 이슈(보안상 취약점이 생긴다.)를 재현해보자!
 window.opener로 부모 윈도우를 실제로 조작해보기 재밌겠다~!

```<a href="www.naver.com" target="_blank">naver<a/>```   
  
**target="_blank"** 만 주고 별다른 옵션은 주지 않았다.  그리고 브라우저에 opener를 쳐보았는데...(또잉..?)
 
<p align="center">
<img width="123" alt="null" src="https://user-images.githubusercontent.com/32082727/138868264-d9aa2214-f0b4-42a4-9921-159035686acf.png" align="center"></p>

noopener 옵션을 주지 않아도 opener를 받아 오지 못했고, 두번째 퍼포먼스 이슈도 재현되지 않아서 찾아보니 **이미** **크롬**은 작년에 해당 이슈관련 **업데이트를** 했다.  

>**The new update to Chrome will instead force  `target="_blank"`  to behave as  `rel="noopener"`** by default.
>ref. [GOOGLE CHROME WILL SOON BLOCK JAVASCRIPT REDIRECTS WHEN CLICKING WEB LINKS](https://chromeunboxed.com/chrome-javascript-block-malicious-redirects-update) 

결론은 chromium 88 업데이트 이후 크롬에서 **target="_blank"** 는 기본적으로 noopener옵션으로 동작한다. 따라서, 개발자가 따로 신경을 써주지 않아도 된다.  

인프런 강의를 보다가 강사분께서 말씀해주신 이슈를 찾아봤는데 과거에 이슈였던 것이었다....  
