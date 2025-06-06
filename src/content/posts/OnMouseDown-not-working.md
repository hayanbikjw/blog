---
title: OnMouseDown가 동작을 안 해요
published: 2025-06-06
description: '구글 검색창: unity OnMouseDown() not working'
image: ''
tags: [C#, Unity]
category: 'Unity'
draft: false 
lang: 'ko'
---

### 왜 안됨?

무언가 동작을 하지 않는다면 원인은 컴퓨터가 아니라 내게 있으니 시도한 것들을 하나하나 해결해보고 정리했다.  
OnMouse 시리즈(?)에는 여러가지가 정의된 메서드가 있으나, 임의로 OnMouseDown으로 작성하겠다. 

:::note    
[OnMouseDown()](https://docs.unity3d.com/6000.1/Documentation/ScriptReference/MonoBehaviour.OnMouseDown.html)은 사용자가 콜라이더 위로 마우스 왼쪽 버튼을 누를 때 호출된다. (Unity Docs)  
:::

#### 콜라이더를 붙이지 않았다

설명에서 읽을 수 있듯이 OnMouseDown 메서드는 콜라이더가 붙어있어야만 동작한다. (2D라면 Collider2D를 붙이기)

#### 콜라이더 위에 무언가 가리고 있지는 않은가?

콜라이더 위에 다른 콜라이더가 붙어 있어 클릭되어야 할 콜라이더를 가리고 있을 수 있다.  
그치만 내 경우에는 간단히 스프라이트 하나만 덜렁 있었기에 이 경우는 해당되지 않았다. 

빈 씬에 스프라이트 하나 놓고 클릭 되는지 안 되는지 테스트하고 있는데 클릭에 반응하지 않으니 답답해 미치겠더라.  
이유가 어이가 없었는데

#### Input System과 호환되지 않는다

어.. 해결은 단순했다. 이유는 OnMouseDown()이 Input System과 호환되지 않기 때문이었다.  
단순히 내 유니티 프로젝트가 6000.1을 이용하고 있어서 기본적으로 구 인풋을 꺼놓았기 때문에 발생한 이슈였다. 

Project Settings > Player > Other Settings에서 Input Handling을 'Both'로 바꾸어주면 인식을 할 것이다. 
