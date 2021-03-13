---
title:  "github.io 블로그 시작하기"
excerpt: "개인 기록, 공부한 것 기록을 위해서 블로그 시작하기로 했다."

categories:
  - Blog

tags:
  - Blog

last_modified_at: 2021-03-13T00:00:00-02:36:00

---

GitHub Blog 서비스인 github.io 블로그 시작하기로 했다.

GitHub Blog 서비스의 이름은 Pages이다.




Pages가 다른 블로그 플랫폼 보다 편한 것 같아서 마음에 든다.

다른 사람들도 같이 많이 사용했으면 좋겠다는 생각이 든다.




YFM에서 정의한 제목을 이중 괄호 구문으로 본문에 추가할 수 있다.

이 글의 제목은 {{ page.title }} (`{`{page.title`}`}로 표현) 이고 

마지막으로 수정된 시간은 {{ page.last_modified_at }} (`{`{ page.last_modified_at `}`}로 표현)이다.  
  
  
다음은 GitHubBlog를 작성하기 위해 필요한 간단한 markdown을 알아보자.  
1. 텍스트 줄바꿈
- - -  
```markdown
텍스트 줄바꿈을 하려면 스페이스 2번을 표기하면 된다.  
*기울이기*는 '*'를 이용하고,  
**볼딕체**는 '**'를 이용한다.  
~~취소선~~은 '~~'를 이용한다.  
```  
2. 글자 크기 지정  
- - -
```markdown
'#'개수가 적을 수록 글자가 커지며 # 개수는 6개 까지 가능하다.
#h1  ###h3  ######h6  
```  
3. 인용    
- - -  
```markdown
> 인용문 
```  
4. 코드인용
```markdown
int main(){
}
```  
  
markdown 코드를 그대로 표현하고 싶은데 C언어 처럼 '`' 백틱은 작동하지 않는 것 같다. 한번 알아봐야겠다.  
  
왜 인지는 아직 모르겠지만 지킬 서비스를 background에서 수행중에 post 내용을 수정하면 반영이 되지 않는데, 다른 터미널에서 지킬 서비스를
동작시키고 또다른 터미널에서 post내용을 수정하면 그때는 바로 반영이 된다.
  
- - -
GitHubBlog 개설 처음부터 마크 다운까지 [devinlife님](https://devinlife.com/howto/)의 블로그를 참조했다. 
  
  

