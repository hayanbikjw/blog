---
title: 대구 X 엔젤 인디게임 페스티벌의 기록
published: 2024-03-21
description: '학점을 상장과 맞바꾸기'
image: ''
tags: [회고, 게임]
category: '게임개발'
draft: false 
lang: ''
---

필자는 시험기간만 되면 공부를 안 하고 딴짓을 하는 버릇이 있다.  
그리고 시험기간에 가장 코딩이 잘 되는 것 같기도 하다.  

## 참가하기까지

<img src="https://www.wevity.com/upload/contest/20231012164507_f486f5e5.jpg" width="45%">

[대구 X 엔젤 인디게임 페스티벌 모집 공고 페이지 (대구디지털혁신진흥원)](https://www.dip.or.kr/home/notice/businessbbs/boardRead.ubs?sfpsize=10&fboardcd=business&sfkind=&sfcategory=&sfstdt=&sfendt=&sfsearch=ftitle&sfkeyword=&fboardnum=7659&sfpage=1)

우연히 위의 공고를 보게 되었고 제출일까지 1주일 가량 남았다. 그렇게 그 길로 시험공부를 접게 되었다.  
예선 제출일은 17일 화요일. 학교 중간고사 기간은 16일부터 20일까지로, 17일에도 논리회로 시험이 있었지만 아랑곳않고 예선을 준비하기로 한다. 

---  
발표일에도 합불 연락이 오지 않아 주최 측에 메일을 넣었고, 25일에 해당 메일의 답신을 받았다.

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-기한연장-메일.png" width="60%">

제출한 기획서가 개차반이었기 때문에 30일까지, 5일간 퀄리티를 올려 다시 제출하기로 했다.  
혼자서 기획서를 만들 때 어려움이 많았다. 그래서 이번에는 혼자 하지 않고 학교 선배를 꼬셔서 같이 하기로 했다.  
제출할 때가 되서는 선배가 힘써준 덕에 게임 기획서 같은 기획서가 만들어졌다. 

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-참여-카톡.webp" width="55%">

## 예선 통과

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-예선-통과-메일.webp" width="60%">  

_앗싸_

11월 10일. 예선 통과 메일을 받았다. 이제 12월 3일(일)까지 중간 결과 제출을, 12월 17일(일)까지 최종 결과를 제출해야 한다. 

<div style="display: flex; justify-content: space-evenly">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-기획서1.webp" width="47%">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-기획서2.webp" width="47%">
</div>

우리는 온라인 게임을 만든다. 네트워크는 [뒤끝](https://backnd.com/ko/) 게임 서버를 이용하기로 했다. 당시 나는 뒤끝은 써본 적이 없었고, 대신 [포톤](https://www.photonengine.com/ko-kr/pun) 엔진을 사용해봤다.  
이때 뒤끝을 고른 이유는 유저 데이터를 저장하기 위해..였고.. 뒤끝 자체로 로그인 기능을 제공했기 때문이다. 이때까지만 해도 자만이 하늘을 찔러 메인기능보다 로그인을 먼저 구현하려 했다. 게다가 점수, 재화 등의 유저 데이터를 저장까지 하려 했다. 왜 그랬을까.. 

뒤끝을 아예 사용해본 적이 없었기 때문에 사용법부터 익혀야 했다. 문서만으로는 도저히 모르겠어서 샘플 게임을 통해 동작 방식을 분석했다. 특히 개발에 있어서 [고박사의 '뒤끝을 이용한 온라인 게임 제작' (youtube)](https://www.youtube.com/playlist?list=PLC2Tit6NyVic7IwurqCebK8JscQfbH4ey) 영상이 큰 도움이 되었다. 만들어주셔서 감사합니다.. 덕분에 살았어요..

그냥 포톤으로 만들 걸ㅠㅠㅠ 만들면서 벅벅 후회했다. 그냥 컴포넌트 붙여서 뚝딱뚝딱하면 멀티 구현이 되는데 한 번도 안 써본 거 붙잡고 만들려니까 시간이 너무 오래 걸렸다. 심지어 버그가 발생해도 왜 그런지 내가 이해를 못하는 경우가 많았다. 흑흑 -> 결정적으로, 쓸모가 없었다. 

게다가 깃으로 버전 관리도 안 했다. 코드 수정하고 아니다 싶어서 되돌리려 해도 가끔 못 되돌렸다. 이때라도 버전 관리를 해야겠다고 깨달았으면 이후로도 불상사가 적었을 텐데 끝까지 버전 관리를 안 했다. 진짜 왜 안 했지? 

## 중간 결과 제출

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-중간-진행-상황.webp" width="80%">

어찌저찌 12월이 찾아왔다. 중간제출 때까지 매치메이킹해서 전투를 치를 수는 있게 만들었다. 

중간 결과를 제출하고 차후 일정 공지가 하나 날라왔는데, 심사위원들이 플레이를 해보는데 플레이에 문제가 생길 수 있으므로 로그인 기능은 제거해야 한다는 내용도 함께 작성되어 있었다. ㅋㅋ... 시간 들여 로그인 기능 만들었는데 도로 없애야 했다. 다만 뒤끝에서는 매치메이킹 시 플레이어가 뒤끝 서버에 등록되어야 했기에, 게임에 들어갈 때마다 id를 부여해서 유저로 등록시키는 방식으로 고쳤다. 테스트 할 때마다 서버에 등록된 유저가 증식했다.

## 최종 결과 제출

중간 제출 직후에는 기말고사(12.04 ~ 12.10)가 나를 반겼다. 나는 별로 반갑지 않았지만 일단 치르려고 했는데 어라라라ㅏ 아주 독한 감기에 걸려버렸다. 시험보는 일주일 내내 열에 시달렸다. 독감도 음성이고 코로나는 11월에 이미 앓았으므로 아닐 것이었다. 시험을 치를 만한 건강 상태가 아니었다보니 시험을 대차게 말아먹었다. 개발한답시고 시험공부를 거의 못했는데 다행히(?) 낮은 시험 점수의 핑계가 생겼다. (학점 낮게 나옴)  
근데 아팠던 건 진짜에요.. 시험 치르는데 머리 어지러워서 시험지가 눈에 안 들어올 정도였어요. 

아파서 개발을 하던 못하던 제출일은 다가온다. 17일까지 제출이지만 18일 오전까지 제출해도 ok라고 해주셔서 18일 8시 경에 제출했다.  
제출까지도 잡지 못한 오류가 있었다. 내가 배치한 캐릭터가 아무리 적 캐릭터를 때려도 내 디바이스에서만 체력이 준다. 상대 디바이스에서는 체력이 안 줄어든다.. 동기화가 제대로 안 되는 모양이다. 그래서 게임 종료가 이상하게 되버렸다. 내 디바이스에서는 아직 안 죽었어도 상대 디바이스에서 내가 죽었다면 게임 종료가 되어버린다. 그리고 한 판이 끝나면 로비에서 다시 플레이를 할 수 없다. 에러가 나서 멈춰버린다. 다시 하려면 게임을 껐다 켜야한다.. 

제출까지 이 심각한 결함을 잡지 못했다. 이거 아니어도 문제가 많았기 때문에;; (아..)

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-제출-전날.webp">  

_마지막 날 카톡으로 빌드 파일 보내고 테스트하고 버그 나면 수정해서 다시 보내고를 반복..._

## 발표하러 가기

제출하고 바로 다음 날 19일(화)에 발표를 하러 대구로 내려갔다. 

<div style="display: flex; justify-content: space-evenly">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/동대구역.webp" width="47%">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구콘텐츠비즈니스센터1.webp" width="47%">
</div>

다른 팀 발표도 보고 싶었지만, 별도 공간에서 대기하다가 우리 순서가 될 때만 발표장에 들어갈 수 있었기 때문에 다른 팀이 무슨 내용 발표했는지는 볼 수가 없었다. 아쉬운 부분.  
우리 팀 발표는 선배가 다 하셔서 난 옆에 서서 멀뚱멀뚱 있었다. 개발 관련 질문이 들어오면 내가 답변하는 거였는데 기술적 질문이 한두 개만 들어와서 발표에 있어 딱히 내가 한 건 없었다. 정상적인 동작이랄 게 별로 없어서 안 물어보셨던 게 아닐까. ㅠ  

기왕 대구까지 내려온 김에 저녁까지 있었다. 동대구역 근처에서 뭉티기를 먹었다. 

<img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-뭉티기.webp" width="45%">

완전 술상이었는데 정작 내가 술을 안 마셔서 그냥 쩝쩝 먹기만.  
발표 잘 했는지 안 했는지가 계속 신경쓰여서 먹는 데 집중을 못 하겠다.. 

&nbsp;

그런데, 그런데.>!!

## 시상식도 가기

대구에 다시 한 번 내려가게 되었다. 이번에는 마음 졸일 필요 없이 다녀와도 괜찮다.  
수상했으니까!! q(≧▽≦q) 

<div style="display: flex; justify-content: space-evenly">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-시상식.webp" width="31%" style="object-fit: cover">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-상장2.webp" width="31%" style="object-fit: cover">
    <img src="https://blogimage001.blob.core.windows.net/pictures/daegu-angel/대구엔젤-상장1.webp" width="31%" style="object-fit: cover">
</div>

**대구 X 엔젤 인디게임 페스티벌 끝!**