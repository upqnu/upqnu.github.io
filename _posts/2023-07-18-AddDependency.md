---
layout: single
title: "스프링 프로젝트에 20초만에 의존성(dependency) 정확히 추가하기"
categories: Project
tag: [spring initializr, gradle, spring boot, 의존성 추가]
---

### Spring initializr 활용해서 스프링 프로젝트에 쉽게 의존성 추가
  
스프링 이니셜라이저(spring initializr)로 스프링 부트 프로젝트를 시작하면  
한 번쯤 화면 오른쪽 dependencies에서 뭔가 하나씩 빼먹은 기억이 있을 것이다. 내 얘기다...  
빼먹은 dependency는 없었지만 프로젝트 상황에 따라 추가되는 경우도 있다.  
  
![image](https://github.com/upqnu/upqnu.github.io/assets/101033614/199ee000-18f0-4f20-8c8a-4c2872eea30f)  

  
위와 같이 프로젝트를 시작해서 열심히 코드를 작성하다가 Spring Web을 추가해야 하는 상황이라면?  
사실 그동안 구글링해서 gradle.build에 의존성을 추가했었다.  
하지만 가끔씩 오타, 잘못된 안내 등등으로 dependency 설정이 잘못되는 경우도 있었다.  
  
![image](https://github.com/upqnu/upqnu.github.io/assets/101033614/9f39cb3d-d398-4b39-9280-e3b66c5b4ab7)  
  
spring initializr에서 정확하게 dependency를 추가해 보자.  
dependency를 추가하려고 하는 프로젝트의 환경과 동일하게 initializr 왼쪽 부분을 작성하고  
Dependency에는 추가하려는 Spring Web만 선택한다.  
  
자, 이제 가장 중요한 부분 : 바로 화면 하단에 **<u>"EXPLORE"</u>**를 클릭하자. 그러면...  
  
![image](https://github.com/upqnu/upqnu.github.io/assets/101033614/d7c6b63a-7e7f-4be1-b9b0-fc875a361eb0)  
  
build.gradle에 입력되어야 하는 내용을 깔끔하게 제시해준다.  
별도의 어려운 설정이 필요없다면 현재 프로젝트의 build.gradle에 없는 부분을  
추가해주면 되겠다.  
(Maven이라면 pom.xml에 추가해야 할 부분도 정확히 안내해준다.)  
  
이걸 이제서야 알다니...  