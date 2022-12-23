---
title:  "[React] React styled-components"
permalink: /categories/react/styled-component
author_profile: true
categories:
  - 리액트
tags:
  - 직무면접
  - 리액트
toc: true
toc_label: "목차"
toc_icon: "bookmark"
last_modified_at: 2022-12-23
toc_sticky: true 
comments: true
---

 싸피에서 React로 프로젝트를 진행하면서, 스타일링을 위해 가장 많이 사용한 방법이 바로 Styled Components였다. 
 그런데 최근에 누군가 나에게 Styled Components의 정의에 대해 물어봤고, 아무런 대답을 하지 못하는 나를 보면서 '뭔지도 모르면서 쓰는 방법만 알고 있구나'라는 생각이 들어, 오늘은 대표적인 CSS-in-JS 라이브러리인 Styled Components가 무엇인지, 어떻게 스타일링을 하는지 살펴보겠다.



### CSS in JS란?

> **CSS in JS는 스타일 정의를 css나 scss 파일이 아닌 JavaScript로 작성된 컴포넌트에 바로 삽입하는 스타일 기법**이다.
>
> 기존 웹사이트는 HTML, CSS, JavaScript를 각자 별도의 파일로 두었는데, React나 Vue, Angluar와 같은 모던 자바스크립트 라이브러리가 인기를 끌고 컴포넌트 기발 개발 방법의 주류가 됨에 따라 한 컴포넌트에 HTML, CSS, JavaScript를 모두 포함하는 패턴이 많이 사용되고 있다.



#### CSS-in-JS의 장점

- CSS의 컴포넌트화로 스타일시트의 파일을 유지보수 할 필요가 없다. CSS 모델을 문서 레벨이 아닌 컴포넌트 레벨로 추상화한다 (모듈성)
- CSS-in-JS는 JavaSript 환경을 최대한 활용 할 수 있다
- JavaScript와 CSS 사이의 상수와 함수를 쉽게 공유 할 수 있다
- 현재 사용중인 스타일만 DOM에 포함한다.
- CSS-in-JS는 짧은 길이의 유니크한 클래스를 자동으로 생성하기 때문에 코드 경량화의 장점이 있다



#### CSS-in-JS의 단점

- 러닝 커브
- 새로운 의존성
- 별도의 라이브러리를 설치해야 하므로 번들 크기가 커진다
- 인터랙션한 페이지일 경우 CSS 파일을 따로 관리하는 방법에 비해 느린 성능을 보여줄 수 있다.



### Styled Components란?

>이 CSS-in-JS 라이브러리 중에서 가장 널리 사용되고 있는  **React**를 주 대상으로 한 라이브러리
>
>컴포넌트 밖에 있는 css, scss 파일에서 태그나 id, class이름으로 가져와 쓰지 않고, 동일한 컴포넌트에서 컴포넌트 이름을 쓰듯 스타일을 지정하는 방식으로 사용



#### 설치

```javascript
$ npm install styled-components
```

#### 기본문법

```jsx
// styled-components 라이브러리에서 styled를 import 해온다.

import styled from 'styled-componets'


const Example = () => {
    return (
      <Wrapper>
    	<Title>Hello World!</Title>
  	  </Wrapper>
    )     
}
 
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;
```

기본적인 모양은 다음과 같다.

```jsx
const 컴포넌트이름 = styled.태그이름`
	css 스타일링
`
```



#### props를 활용해 조건부로 스타일링 해주기

```jsx
const Example = () => {
    return (
      <div>
    	<Button>Normal</Button>
    	<Button width="100">Primary</Button>
  	  </div>
    )     
}

const Button = styled.button`
  background: ${props => props.width < 200 ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};
  font-size: 1em;
  margin: 1em;
`
```



#### 기존에 만들어놓은 컴포넌트 스타일 확장하기

```jsx
const Example = () => {
    return (
      <div>
        <Button>Normal Button</Button>
        <TomatoButton>Tomato Button</TomatoButton>
      </div>
    )     
}

const Button = styled.button`
  color: palevioletred;
  font-size: 1em;
  margin: 1em;
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;

// 기존의 스타일링이 끝난 Button을 확장해서 사용하기
const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;
`;
```

