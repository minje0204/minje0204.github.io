# Virtual Dom (가상돔)

react를 사용해오면서 가상돔을 알게 되고, 이게 왜 필요한 것인지 궁금해졌다. 먼저, 
한줄 요약을 해보자면, 실제 DOM 트리를 직접 조작하기에 시간이 오래 걸리기 때문에 가상돔을 활용하여 DOM트리 노드들의 배치를 최적화 시킬 수 있다고 한다. 이를 더 자세히 알아보기 위해서는 먼저 브라우저의 작동 방식을 알아야 한다.

### 브라우저 주요 기능
 사용자가 선택한 자원(주로, html문서)의 URI를 참조하여 서버에 요청한다. 이를 W3C가 정한 HTML CSS 명세에 따라 해석하여 브라우저에 표시한다.  
### 브라우저의 렌더링 방식 (WebKit엔진 기준)
<img width="691" alt="howwebkitworks" src="https://user-images.githubusercontent.com/32082727/130776446-13622635-82ee-4f77-a86b-d7c57ae0ec8f.png">

다음은 webkit이 작동하는 방식이다.  
1. 브라우저는 HTML문서를 파싱하여 **DOM Tree**를 생성한다.
2. css style에 관한 style sheet를 파싱하고 해당하는 Node의 **Attach Method**를 실행하여 해당 노드에 스타일을 덫붙힌다. 이 동작을 **Attachment**라고 하며, **Synchronous**하게 처리된다. 
3. 브라우저에서 각 Node들이 어떤 위치에 있어야하는지 스크린의 좌표를 계산하는 **Layout 과정**을 거친다.
4. Tree에 각 노드들을 거쳐가면서 색을 칠해준다.
5. **Rendering** 완료  
 
 ## 왜 DOM Tree를 직접 수정하는 것이 오래걸릴까?
DOM Tree에 변화가 생기면, 위 렌더링 과정이 처음부터 다시 시작되어야 한다. 특히, **attachement** 과정에서 style은 tag, class, id별로 style이 다르게 주어질 수 있고, 별다른 언급이 없다면 부모 노드의 style을 따르기 때문에 상당한 연산이 필요한데, 복잡한 **SPA** 와 같이 DOM 변경이 잦아 진다면, 렌더링 과정을 비효율적으로 만들것이다.   

### 가상돔을 쓴다면?
뷰의 변화가 있을 때, 실제 DOM에서 만들어 질 수 있는 가능한 모든 후보군을 가상돔에서 만들어보고(*실제 DOM에서 적용하는 것이 아니기 때문에 비용이 덜 들어간다.*) 실제 DOM에 적용 시킴으로서 렌더링 과정을 더 효율적으로 만들 수 있다.
렌더링의 연쇄과정을 가상 DOM에서 진행하고 이 결과물만 떼어 실제 DOM에 적용시킨다고 난 이해했다.

>DOM fragment를 직접 관리하지 않아도 되게(어디를 변화시켜야 하는지, 어디까지 변화를 반영했는지 등등) 자동화, 추상화 시켜 준다. 
>DOM Tree변화를 하나로 묶어 적용시킴으로서, 변경된 노드사이의 동기화 작업이 필요없어진다.

어쨌든 가상 돔을 사용해도, 연산이 아예 사라지는 것이 아니기 때문에 단순히 **가상 돔**을 쓴다고 해서 빠르다고 볼 수 없다. 그래도 보통 문제없이 사용할 정도는 된다고 한다. **가상 돔**에서의 연산과정 조차 줄이기 위해서 아예 빌드시 해당 연산을 해버리는 **servlet**도 있다. 하지만 html 변경시 재빌드가 필요하다는 단점이 있다.

### REFERENCE
https://hashnode.com/post/the-one-thing-that-no-one-properly-explains-about-react-why-virtual-dom-cisczhfj41bmssp53mvfwmgrq
https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/
