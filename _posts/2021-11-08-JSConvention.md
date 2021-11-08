
---
title:  "JS 컨벤션 정리(추가 중~~)"
excerpt: "구글(Google), 에어비엔비(Airbnb), NHN style guide"

categories:
  - JavaScript
tags:
  - Convention

last_modified_at: 2021-11-08T18:00:00-19:00:00

---

웹개발자를 지망하고 있는데 **JS style guide**를 한번도 제대로 보지 못했다.  
그래서 **구글, 에어비엔비, NHN의 js style guide**를 정리해보려고 한다.  

## Source File  Basics

### 2.3.1 White spaces (공백 문자)

>1.  All other whitespace characters in string literals are escaped, and
    'string literals' 안에 있는 모든 공백문제는 escape => **\\** 처리 되어야 한다.
>2.  Tab characters are  **not**  used for indentation.
	indentation(들여쓰기)를 위해서 Tab을 사용하면 **안 된다??**

Tab을 쓰면 안되는 이유는 다음과 같다.
Tab 문자 자체가 태생적으로 모호하고 (*can be blank 2칸 or 4칸*)  Tab이 코드라인 처음에 위치하기 때문에 **Tool에 따라서 같은 코드가 다르게 렌더될 수 있다.** [코드예시](http://www.javapractices.com/topic/TopicAction.do?Id=244)

## Objects

-   [3.1](https://github.com/airbnb/javascript#objects--no-new)  Use the literal syntax for object creation. eslint:  [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)
```javascript    
    // bad
    const item = new Object();
    
    // good
    const item = {}; 
```
-   [3.2](https://github.com/airbnb/javascript#es6-computed-properties)  Use computed property names when creating objects with dynamic property names.
    
    > Why? They allow you to define all the properties of an object in one place.

```javascript
    function getKey(k) {
      return `a key named ${k}`;
    }
    
    // bad
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;
    
    // good
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
```
-   [3.3](https://github.com/airbnb/javascript#es6-object-shorthand)  Use object method shorthand. eslint:  [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

```javascript
    // bad
    const atom = {
      value: 1,
    
      addValue: function (value) {
        return atom.value + value;
      },
    };
    
    // good
    const atom = {
      value: 1,
    
      addValue(value) {
        return atom.value + value;
      },
    };
```
