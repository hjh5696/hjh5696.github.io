---
layout: post
title: navigation bar transition 정복해보자
---
### Intro
왜이렇게 어렵게 해놨는지 이해가 안되지만.. 일단 기억보관용 메모

### 스토리
navigationBar.isTranslucent => true면 viewController의 child view가 bar 아래로 들어가고, bar 색깔이 semi transparent로 됨
=> false면 bar opaque, view도 bar 아래서 부터 시작함. 
true가 기본값이고, 사실 pinLayout쓰니까 safeArea로 아래 view는 bar 밑에 안가도록 쉽게 조정할 수 있어서 true가 좋다. 근데 문제는 navigationBar 색깔이 내가 원하는 색으로 설정되지 않고 semi transparent 효과때문에 달라진다는 점..
어떤 SO에 보니까 isTranslucent를 viewController마다 바꿔주는게 (투명한 bar 위해서) 이상한 navigationBar transition의 원인이라고 해서 없이 실험을 계속 하다가 시간 많이 날림

일단 결론을 얘기하자면 투명한 navigationBar를 만들고 싶으면 
navigationController?.navigationBar.isTranslucent = true
navigationController?.navigationBar.setBackgroundImage(UIImage(), for: .default) 를 viewWillAppear에서 설정해줘서 백그라운드 없애버리고 Translucent 하게 만든다.
SO에 보면 대부분 backgroundColor와 barTintColor를 clear로 설정해주라고 하는데 안해줘도 잘 나오는듯? 이건 추가 실험 필요
viewWillDisappear에선 isTranslucent 다시 false로 바꿔줌 (물론 다음 네비게이션이 어디냐에 따라 다르겠지만 또..)

willMove가 이상하게 transition 되는거 없애주네. transparent로 갈때 부드럽게 바꿔줌. willDisappear 쓰지말고 
