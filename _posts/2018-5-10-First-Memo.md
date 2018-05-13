---
layout: post
title: First memo
---
#### Intro
항상 쓰면서도 헷갈리던 것들이니 기회가 될 때 정리해두자. 사실 아래 Reference의 원문을 공부하는 겸해서 내가 이해한 바대로 다시 적는 것 뿐이다.

#### 스토리
이 명제에서 출발하면 될 듯 하다. 
`Apple의 하드웨어에서 특정 소프트웨어가 동작하게 허락하는건 Apple 뿐.`
그럼 개발자가 앱을 디바이스에 넣어서 실행시키거나 테스트하려면? Apple의 허락이 필요하다.
이 '허락'을 받는 과정이 Certificate(인증서)을 받는 것 + Provisioning Profile을 만드는 것이라고 보면 되는 듯.

* Certificate
Certificate Signing Request(=CSR)를 Keychain Access에서 만들어 애플에게 보여주면, 애플은 나를 개발자로 인정(?)해주는 의미로 Certificate을 발급해준다. 그럼 CSR은 분명히 '나는 Apple 하드웨어를 사용하면서 Apple ID를 가지고 Apple 소프트웨어를 개발하려고 하는 사람이 맞다'라는 정보를 담고 있어야겠네.
원문을 참고해보면 공개키/개인키를 가지고 내 정보를 담은 파일을 사인해서 CSR을 만든다고 한다. 그럼 결국 저 정보들을 담고 있는게 맞네.
결과적으로 발급받은 Certificate은 앱을 사인할 때 쓰인다. 쉽게 이해하자면 Certificate은 나를 'Apple이 인정해 준 개발자'로 만들어주고, 사인할 수 있게 해주는 역할이군

* Provisioning Profile
Certificate이 '내'가 애플로부터 개발자 라는걸 인증받는 용도라면, Provisioning Profile은 소프트웨어를 설치할 Device들한테 허락을 구하는 과정이라고 보면 된다. 
Provisioning Profile을 만든다 = Certificate과 테스트할 Device들을 연결한다
#### Reference
[원문 - http://la-stranger.blogspot.com/2014/04/ios.html](http://la-stranger.blogspot.com/2014/04/ios.html)
