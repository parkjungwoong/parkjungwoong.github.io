---
title:  "레거시 소스 개선을 하며 느낀 점(1/4)"
date:   2019-03-10
description: 레거시 소스를 개선하며 느낀 점들을 공유합니다.
---
## 헬게이트의 시작
2017년 여름쯤 6~7년정도 운영된 시스템을 받았다.\\
Struts2 + Spring 구조의 시스템이였는데 그동안 운영하던 회사도 바뀌고 그냥봐도 여러사람의 손을 거쳐간 시스템이였다.\\
엄청난 양의 하드코딩 (이벤트가 있을때마다 if else if else 로 막 넣었나봄..)\\
어느것이 최신인지 모를 문서, 업무 정책은 말하는 사람마다 다르고..\\
그래도 문제 없이 잘 돌아가는 시스템고 최근 몇년간 사업쪽으로 특별한 이슈가 없어 개발건은 많이 없겠구나 했는데 "이제부터 큼직막한 기능들이 새로 개발되어야한다." 라는 말을 듣고나서 고민이 깊어졌다.\\
더이상 이 소스에 똥을 뿌리긴 싫고.. ( 커밋 로그에 내 이름이 남는데 똥을 남길 순 없다라는게 내 생각이다. )\\
주변 동료 : "운영 적용만 하면 장애가 난다.. 업무 자체가 정말 복잡하다.. 우리팀 3대장중 하나다.." 이런소리를 듣고 겁이 났다.

그래도 어찌겠는다 이왕 맡은거 차세대!! 하고 싶었지만 그렇게 하기엔 일정,등 여러가지 상황이 안되니 점진적으로 개선해보도록 계획을 잡았다.

## 시스템 개선을 위한 3 STEP
시스템 개선을 위해 우선적으로 해야될것을 생각해보니 3가지로 추려졌다.

***1.정확한 업무 파악***\\
API 명세 최신화, 정책, 시스템 구성, 외부 연동이 있는지.. 등등을 정리한다.\\
모든 코드에는 이유가 있다고 누군가 말했었다.. 경험상 대부분 업무에 관련한 이유가 많았다.\\
내가 보기엔 필요없는 부분이라도 업무를 알고보면 필요한 것일 수 도 있게 때문에 정확한 업무 파악이 먼저 선행되어야한다.\\
특히 중점적으로 봐야하것은 정책! 예를 들면 고객 등급 정책이라던지 이런것들을 확실히 알아야 잘못된 부분을 수정할 수 있다.\\
그리고 빼먹기 쉬운것중 하나로 외부 연동 시스템 유무인데 최소한 최근 1년내의 인입 로그를 확인하는게 좋다고 생각한다.

***2.TODO 리스트 작성***\\
업무 파악이 끝났으면 이제부터는 시스템 구성과 코드를 보면서 개선점이 있는지 살펴본다.\\
정책에 맞지 않은 코드가 있는지, 반복되는 코드는 없는지,장애 히스토리를 보며 개선이 되었는지,등 할일의 목록을 작성하고 우선순위를 정하도록한다.\\
이렇게 하면 좋은점이 보통 회사에서는 주단위 업무보고가 많은데 다음주 일정에 대해서 미리 정해두고 보고를 해야된다.\\
차주 일정에 대해서 TODO 리스트를 보고 결정할 수 있으니 담주에 뭐하지 라는 쓸대없는 고민을 할 시간을 세이브해준다.  

***3.테스트 코드***\\
API 명세가 바뀐 게 아니라면 코드 수정 전 응답과 수정 후 응답이 같아야한다.\\
이런 테스트는 상당히 귀찮고 반복적인 작업이 많기 때문에 JUnit과 같은 도구를 통해 미리 만들어 놓고 사용하는게 편하다.\\
간단하게 API요청, 응답 값 검사부터 DB에 들어가는 데이터까지 체크 할 수 있는 부분은 모두 해놓는 것이 좋다.

## 마치며..
간단하게 이전 경험을 정리하다 보니 글이 길어질거 같아 4개로 나눠 쓰기로 하였다.\\
다음에는 ***정확한 업무 파악***을 진행하며 겪었던 경험담을 정리할 예정이다.