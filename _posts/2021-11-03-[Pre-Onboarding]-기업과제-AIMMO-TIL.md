---
title: "[Pre Onboarding] 기업과제 AIMMO TIL"
excerpt: AIMMO TIL
author_profile: true
toc: true
toc_sticky: true
categories: 
  - preonboarding
tags:
  - coding
  - 위코드
  - 원티드  
  - #위코드
  - #원티드  
  - #AIMMO
  - #에이모  
  - AIMMO
  - 에이모
last_modified_at: 2021-11-03T17:46:30-05:00
---



## [Pre Onboarding]  기업과제 에이모 TIL

***

</br>

11월 1일부터 진행한 Wecode X Wanted 프리온보딩 코스에 참여하게 되었습니다. 총 인원은 약 80명으로 팀별로 5~7명씩 모여서 진행했는데 내가 속한 팀은 13팀으로 6명이서 진행하게 되었습니다.

첫 번째 기업 과제는 AIMMO 기업에서 진행한 과제였고 과제가 비교적 간단하다는 이유로 팀 내에서 3명씩 나뉘어 과제를 제출했습니다. 

 2개의 팀으로 나뉘어서 1팀과 2팀 중 저는 express framework를 사용할 2팀에서 과제를 진행하였습니다.

</br>

**AIMMO 기업 과제 내용**은 아래와 같았습니다.

- RESTful API 설계
- User 기능
- 게시글 CRUD
- 게시글 페이징
- 댓글 및 대댓글 페이징
- 테스트 코드
- 배포

</br>

팀을 나눠서 개발하기 전에 다 같이 구조와 코드에 대해서 통일화를 하는게 좋을 거 같아서 팀에서 사용할 노션 페이지를 새로 생성한 뒤 화상 회의를 통해 코드 컨벤션과 깃 컨벤션에 대해 정리를 했습니다. 

지금까지 깃을 커밋하면서 깃 메세지에 대해 크게 중요하게 생각하지 못했었습니다. 

간략하게 축소해 타이틀만 작성해서 올렸는데 해당 방식으로는 어떤 commit에서 무슨 작업을 진행했는지 제대로 알기 어려웠습니다. 이번에 팀원들끼리 깃 컨벤션 규칙을 정하면서 각각 어떤 기능을 구현했고 어떤 내용을 수정했는지 한 눈에 알 수 있어 좋았습니다.

</br>

기본 구조를 정한 뒤  ERD와 API 명세서를 작성했고 2팀에서 Express Framework를 이용해 개발을 진행했습니다. 

 팀원 한 분이 기본 세팅을 해주시고 바로 API 개발을 진행했습니다. 서로 화면 공유를 통해 API 기능을 구현 하면서 막히는 부분이 있으면 질문하고 문제를 해결하는 방식으로 진행했습니다. 

 </br>

저는 게시판 CRUD API 를 구현했고 이 외에 다른 팀원분들과 화면 공유를 통해 서로 의사소통하며 어려운 점에 대해 문제를 논의하고 방법을 함께 찾아봤습니다.

게시판 API에서 검색 기능을 구현할 때 title, author, category 중 셋 중 하나만 적어도 되는 조건을 걸기 위해 `$or` 을 사용했었습니다. 검색 api와 목록 api 가 query의 종류 여부에 따라 분류되고 같은 controller를 사용하고 있었고 `$or`을 적용하면 빈 값이 들어가 오류가 계속 발생했었습니다. `if(postQuery)` 라고 하면 값이 있는 경우에를 본다고 생각했는데 length가 0이라고 처리를 해야 값의 존재 여부를 판단할 수 있어 개념에 대해 잘못 알고 있어서 이를 고치고 문제를 해결했습니다.

</br>

또, Board API 에서 전체 목록을 Response로 보낼 때 조회수를 보여주기 위해 readUser를 object 로 넘겨줬는데 1000만건 이상의 테스트를 해보거나 인원 수가 많아질 때 데이터가 너무 커질 것을 염려해 delete로 지워주려고 했습니다. 

그런데 monogodb에서는 board의 전체 값이 POJO가 아니라 다소 특수한  object 형식인 것 같았고  그 결과 object에서 사용할 수 있는 delete 를 사용하니 지워지지 않는 것이었습니다. 

<img src="https://user-images.githubusercontent.com/60311404/140606424-39d28524-e301-4d1c-bcc4-b0e1616de321.png" alt="image" style="zoom:67%;" /> 

 [참고 블로그](https://velog.io/@modolee/mongodb-document-to-javascript-object#toobject-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%9D%B4%EC%9A%A9) 

팀원들과 함께 이에 대한 내용을 구글링 해보고 찾아보며 이러한 사실을 알게 되었고 toObject() 함수를 이용해 POJO 형식으로 변환시키고 delete를 적용하니 response에만 지워지는 모습을 확인할 수 있었습니다. ~~(다음에 기회되면 toObject() 메서드가 아니라 lean() 메서드를 사용해봐야지,,,)~~ 

</br>

기술적 측면에서 이러한 오류로 헤매는 것을 보고 아직 더 배워야하는 점을 깨달았고 팀프로젝트를 하면서 과제를 진행하니까 서로서로 모르는 것을 물어보고 아는 것은 서로 대답해주며 개념들이 좀 더 정확하게 머리에 정리 되는 것 같아서 앞으로 남은 주차 동안에는 **지금보다 더 많이 공부하고 다양한 지식을 주고받을 수 있을 거 같아 많은 것을 배울 것 같다는 생각이 들었습니다.**

</br>

다음 과제에서는 좀 더 다양한 구조를 사용해보고 코드 리팩토링도 진행해보면 좋겠다 라는 생각을 했습니다. 아직 오류 처리도 부족하다는 생각도 많이 들었고 코드 표준화가 아직은 부족하다는 생각이 들어서 이 부분을 좀 더 보완해서 앞으로 차츰차츰 과제의 완성도를 높여나가고 싶습니다!!

</br>

#### 결과물

[1. 2조 (framework : express)](https://github.com/preOnboarding-Team13/Assignment_1_AIMMO_express)

[2. 1조 (framework : nest.js)](https://github.com/preOnboarding-Team13/Assignment_1_AIMMO_nest)

