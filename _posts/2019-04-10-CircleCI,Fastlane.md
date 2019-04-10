---
layout: post
title: Circle CI + Fastlane
---
### Intro
CircleCI에 Fastlane 얹어서 배포와 테스트, 빌드를 자동화

### 스토리
#### Match
Match에 대한 이해. CodeSigning 각 용어 이해 필수.
까다로웠던건 config를 다양화해서 debug, release, beta로 나눴는데, 각각에 certificate과 provisioning profile이 필요하다는 것. 
nuke한 후에 private certificate repo에 match로 certificate/provisioning profile 생성했다. 
그런데 이 때 master/beta/dev 브랜치 별로 cert/profile들 저장하려 하니, beta와 release 각각이 둘다 type: appstore라 그런지 distribution certificate이 두개가 생겨버림.
그래서 그냥 app_identifier: ["~.dev", "~", "~.beta"]로 development, appstore 전부 생성. 그럼 profile은 6개 생기고, certificate은 dev하나, distribution하나 딱 잘 생성됨.
나중에 브랜치별로 하는거 다시 도전해보자.

#### Pod install cache
이게 시간이 엄청 길지는 않은데 캐시하는 방법 찾아보자.

#### 전반적인 세팅
https://medium.com/sixt-labs-techblog/continuous-integration-and-delivery-at-sixt-91ca215670a0
여기 많이 참고함. CircleCI에서 match codesigning 원활하게 하기 위해 CI에선 temporary keychain(?) 생성하게끔 돼있음.
새로운 팀원이나 새 머신에선 `bundle exec fastlane certificates refresh_certificates:true` 돌려서 certificate과 provisioning profile 다 share된거 쓰게끔.
새 로컬에서 세팅할 때 refresh_certificates가 `true`인지 `false` 여야하는지는 더 알아보자. 그리고 github certificate repo passphrase를 치면 로컬에 바로 깔린다.

#### Environment Variable
Testflight 업데이트할 땐 app Specific password 필요하다.
passphrase는 MatchPassword에..
