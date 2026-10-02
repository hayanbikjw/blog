---
title: "길드림 출시!"
published: 2026-10-01
description: '두 번째 게임을 출시했습니다. 와아아!'
image: 'https://shared.fastly.steamstatic.com/store_item_assets/steam/apps/3908240/99cbea5c06c0b360988921d05c07d26c39a92514/header.jpg'
tags: [게임, 개발]
category: '게임개발'
draft: false 
lang: ''
---

안녕하세요, 오랜만에 찾아뵙습니다. 

제가 프로그래머로 참여해 개발했던 게임 'Guildream'이 9월 29일 00:11분 경, steam과 stove 두 플랫폼에서 출시되었습니다.    
와앙아아아아아아아ㅏ아아아아아앙!!!!!

<img src="https://blogimage001.blob.core.windows.net/pictures/guildream/yeah.webp" alt="yeah~" width="60%" style="min-width: 250px;">

스팀에서도 잘 검색됩니다!

<img src="https://blogimage001.blob.core.windows.net/pictures/guildream/steam-page.webp" alt="스팀 상점 페이지 스크린샷" width="60%" style="min-width: 250px;">

## 개발 후일담

지난 9월 초 즈음부터 Team DiKi에 들어와서 약 1년 동안 개발하였습니다.   
개발을 진행하면서 깨달은 점을 적어볼까 합니다.

### ScriptableObject Architecture는 생각보다 별로다

들어와서 개발할 당시, 저는 Unity에서 제공한 [e-book](https://unity.com/kr/resources/create-modular-game-architecture-with-scriptable-objects-ebook)을 읽고 좋은 방법론이라고 생각해서 길드림 프로젝트에 적용했습니다. 

event라던가 runtime data라던가 data container라던가를 ScriptableObject(이하 'SO')로 만들었는데요, 처음으로 적용해본 거라 잘 몰랐기도 했고 그냥 SO로 구조를 짠다는 것 자체에 문제도 있다고 지금은 그렇게 생각합니다. 당시에는 SO로 구조를 짜면 좋게 만들어질 줄 알았죠.    

그렇다고 SO로 구조 짜는 게 나쁜 것만은 아닙니다. 처음에는 구조가 예쁘게 짜졌어요. 그러다 점점 더러워졌을 뿐이지만요. 결론은, SO가 좋은 방법론은 아닌 건 확실한 것 같습니다. 적당히만 쓸만 한 것 같아요.

마지막으로 SO로 구조 만들 예정이라면, 런타임 데이터는 절대 SO로 다루지 마십시오. 나중에 문제가 발생해도 어디서 문제가 생겼는지 추적하기 힘들어서 애먹었습니다. 나중에 다른 프로젝트 할 때에는 무조건 코드로 작성해서 추적하기 쉽게 할 겁니다. 

### 아트는 다다익선이다

복창합니다 

아트는 다다익선입니다    
아트는 다다익선입니다

### 대충 코드를 짜지 말자

후회하는 것 중 하나입니다. 미래의 나를 믿는 행위만큼 어리석은 짓은 없기 때문에, 코드는 항상 예쁘게 짭시다. 

지금 당장이 급하다고 나중을 생각 안 하고 일단 질렀더니 나중에는 저를 원망했습니다.  * 대충 인터스텔라에서 쿠퍼가 오열하며 책장 치는 사진 *

### Y/N 을 묻는 팝업 창은 값을 리턴받아서 처리했으면 좋았을텐데

길드림의 팝업창 코드는 대부분 아래와 같은 형태로 작성되어 있습니다.

```csharp title="OpenSomePopup.cs" showLineNumbers
SomePopup popup = PopupManagerController.Current.Enqueue("Some Popup") as SomePopup;

popup.Setup(slotIndex, () =>
{
    // ok 시 수행할 로직
});
```

```csharp title="SomePopup.cs" showLineNumbers
public void Setup(Action action)
{
    okButton.onClick.AddListener(() =>
    {
        DequeuePopup();
        action.Invoke();
    });
    cancelButton.onClick.AddListener(() =>
    {
        DequeuePopup();
    });
}
```

팝업을 누를 때 ok를 누르면 인수로 넘겨진 Action을 수행하는 방식입니다.    
이 코드를 아래와 같이 바꾸고 싶었습니다.

```csharp title="OpenSomePopup2.cs" showLineNumbers
SomePopup popup = PopupManagerController.Current.Enqueue("Some Popup") as SomePopup;
bool result = await popup.GetResultAsync();

if (result)
{
    // ok 시 수행할 로직
}
else 
{
    // cancel 시 수행할 로직
}
```

```csharp title="SomePopup2.cs" showLineNumbers
private TaskCompletionSource<bool> _popupTaskSource;

public async Task<bool> GetResultAsync() // task 대신 coroutine이나 unitask도 가능
{
    _popupTaskSource = new TaskCompletionSource<bool>();

    okButton.onClick.AddListener(() => OnButtonClick(true));
    cancelButton.onClick.AddListener(() => OnButtonClick(false));

    bool result = await _popupTaskSource.Task;

    return result;
}

private void OnButtonClick(bool result)
{
    _popupTaskSource.SetResult(result);
}
```

위와 같은 식으로 바꾸면 코드가 조금은 길어지겠지만 로직이 분기되어 멀리 떨어져나가지 않고 중앙에서 계속 진행된다는 점에서 관리하기 편할 것 같다고 생각했습니다.

길드림의 팝업창 코드를 아래 로직으로 바꾸고 싶었지만, 이미 많은 팝업창이 윗방식으로 작성되어서 통일성을 해치지 않기 위해 바꾸지는 않았습니다. 그러나 테스트해보고 싶어서 일부 팝업창에는 아랫방식이 적용되었는데, 되려 윗방식과 아랫방식이 혼용되어 로직을 알기 쉽지 않아졌다는 문제를 낳았습니다. 

### 확장성 있는 개발을 하는 것도 좋지만, 처음부터 넣으면 더 좋다 

우리는 클린 아키텍처, 소프트웨어 아키텍처, 설계 등등 여러 권장도서들을 읽다보면 나중에 변경될 것을 대비하여 '확정성 있게 개발하라'라는 조언과 문구를 많이 보곤 합니다. 

혹은 YANGI(You Ain't Gonna Need It) 설계원칙, 당장 필요없는 기능이나 코드를 미리 구현하지 말라는 말도 익히 들었을 것입니다. 

그러나 유니티는 말입니다. 다른 소프트웨어 개발 환경과 달리 꽤나 특수한 환경이라 생각합니다. 미리 구현해두어야 나중이 편한 경우가 왕왕 생깁니다. 예를 들어, Localization package 같은 경우, 도입 예정에 있다면 일찍일찍 넣어두어야 편합니다. 나중에 text 들어간 데를 찾아서 localization component를 어디에 넣어야할지 찾는 것은 게임의 크기가 커질수록 오래 걸리기 때문입니다.  

### 여러 플랫폼에 런칭하기

우리 팀은 Steam과 Stove 양 플랫폼에 동시 출시하기로 결정했습니다. 

클라우드 저장이나 업적 등등 플랫폼 별로 구분해서 동작시킬 필요가 있었고, 솔직히 스토브는 너무 어려웠습니다.   
자료가 없어요 자료가 

그리고 생각보다 steamworks 웹페이지가 구려요. 하지만 잘 굴러가니 장떙입니다.

## 개발자 인터뷰

출시 기념으로 개발자 분을 인터뷰해보기로 했습니다.    
팀장님이신 박늘보를 모시겠습니다. 안녕하세요.

### 출시 소감 한 말씀 가능할까요?

출시소감 얘기하기 전에, 어쩌다 이 게임을 만들게 되었는지 이야기하는 게 좋을 것 같습니다. 첫번쨰 게임이 스케일이 너무 컸기 때문에 두 번쨰 프로젝트를 할 때에는 할 수 있는 걸 해보자라는 마인드로 시작했습니다. 그래가지고 리소스도 진짜 최소한으로 쓸 수 있는 방향으로 하고 이제 시스템도 진짜 간단하게 할 수 있는 포인트 앤 클릭으로 되어 있죠. 덕분에 의도대로 만들 수 있는 걸 만들었다고 생각을 합니다. 의도대로 만들긴 했는데 당초 만들 수 있는 걸 만들자가 목표였다 보니 지금 와서는 아쉽거나 부족한 점이 정말 많다고 생각하기는 합니다. 

그래도 지금 이 프로젝트를 하면서 정말 배운 게 많은 것 같고 특히 이제 단순히 게임을 만들었다에서 그치는 게 아니라 QA까지 해보도 미팅 같은 것도 해보고 전시도 해보고 펀딩도 받아보고 결과적으로 스팀에 출시까지 해보는 이 경험들은 정말 값지지 않았나 이렇게 좀 생각을 합니다. 

### 길드림과 관련된 "재미있는" 에피소드가 있을까요?

일러스타 페스에서 전시를 했는데 당시에 스토브에서 지원을 받기도 했고 첫 전시이다 보니 조금 적극적으로 했어요. 막 길 가는 사람한테 눈 마주치면 전단지를 줬거든요. 이제 붙잡히면은 나한테 설명을 들어야 해. 이런 식으로 나름 열심히 했다고 생각해요. 직접 본 건 아니고 전해 들은 건데 나중에 인디 게임 마이너 갤러리인가 거기서 일러스타 플레이 누가 글을 올렸는데 길드림 저격당했더라고. 뭐였냐면 자기는 조용히 구경하고 싶은데 자꾸 와가지고 막 호객행위 해가지고 거슬렸다 이런 식의 내용이 있더라고요. 

그런 저격을 당했던 일화가 있는데 근데 그걸 들어도 '내가 실수했구나'라는 이런 생각보다는 그만큼 내가 열심히 한 걸 알아봐줬구나 이런 생각이 들어요.

### 1년 동안 하게 되면서 개발을 지속해게 된 원동력이 무엇일까요?

일단 책임감이 가장 큰 것 같다는 생각이 들고요, 게임 개발을 할 수 있는데도 안 하는 나 자신이 상상이 잘 안 된다고 생각합니다. 그러니까 게임 개발이 힘들고 노력해야 되는 무언가라고 느껴지지 않기는 해요. 그래서 출시를 지키고 거기까지 오는 데 그 책임감이라는 것 떄문에 억지로 끌려온 감도 없지 않긴 하지만 그냥 게임 개발하는 게 자연스러운 일이었던 것 같다는 생각이 듭니다. 힘든 일 이런 것보다는 재밌고 그러니까 그냥, 그냥 했다가 좀 큰 것 같아요. 저스트두잇이 70% 정도 되고 30%는 팀원과 후원자님들에 대한 책임감. 

### 향후 계획이나 포부가 있으실까요?

한동안은 게임 개발을 즐기는 감을 좀 되찾으려고 생각을 해요. 사실 이 출시까지 오면서 솔직히 좀 힘들었거든요. 힘들고 지칠 때도 있고 그랬는데 그러면서도 드는 생각이, 내가 게임 개발을 너무 좋아해서 진짜 즐기기 위해 시작을 했는데 즐기지 못하는 내 모습이 좀 회의감이 들었어요. 그해서 한동안은 게임 개발하는 스스로가 좀 즐거워보이는 그 감을 찾기 위해 노력을 할 것 같고 그러다가 뭔가 다른 사람한테 보여줘도 자랑스러울 만한 프로젝트나 그런 걸 준비해서 좀 활동도 많이 해보고 싶다는 생각이 있습니다. 

_이상으로 인터뷰를 마치겠습니다. 응해주셔서 감사합니다!_


## 버그를 잡으러 바다로 갈까요

아 잠깐만

<img src="https://blogimage001.blob.core.windows.net/pictures/guildream/daehwa.webp" alt="게임 개발자 커뮤니티의 버그 제보" width="60%" style="min-width: 250px;">

왜   
왜에ㅔㅇ에ㅔ

흙흐긓글그르으ㅡㄹ그ㅡ

---

그렇게 정식 출시를 하고도 다시 픽스하고 있습니다. 너무너무 슬퍼요

<img src="https://blogimage001.blob.core.windows.net/pictures/guildream/steam-discount.webp" alt="길드림 스팀 출시 할인" width="50%" style="min-width: 250px;">

어찌되었건, 10월 13일까지 출시 기념 20% 할인을 하고 있습니다. 잘 부탁드립니다!

[스팀 페이지(store.steampowered.com)](https://store.steampowered.com/app/3908240/Guildream/)   
[스토브 페이지(store.onstove.com)](https://store.onstove.com/ko/games/105470)