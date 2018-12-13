---
title:  "Authenticating to network가 반복적으로 뜰 경우"
permalink: "/:categories/mac-auth-to-network"
date: 2018-12-11 01:00:00 +0900
categories: [Mac]
tags: [Mac, auth, security, network]
typora-root-url: /Users/myeongwon/blog/
---

사실 나는 원래 그냥 아무 생각 없이 확인 버튼을 누르곤 하는 이른 바 '예스맨'인 관계로 매번 맥에서 무슨 다이얼로그가 뜨더라도 대부분 무시하곤 했다. 또한 문제점이 발생하더라도 macOS는 버전이 올라가며 해결되곤 하는 편이라 신경을 끄고 산 것도 있었는데, 이건 버전 세 개가 올라가도록 해결될 기미가 안 보여서 내가 직접 찾아보기로 했다.

# 문제

{% include figure image_path="/assets/images/mac_auth_to_network01.png" alt="mac_auth_to_network01" caption="와이파이 접속할 때마다 뜨는 대화상자. 덮개를 열었을 때도 예외는 아니다" %}

- 문제 발생 상황: WPA2 보안 방식을 사용하는 무선 랜 네트워크에 연결을 시도할 경우 인증서에 모종의 문제가 있는 경우
- OS 환경: macOS 10.12, macOS 10.13, macOS 10.14
- 증상: 와이파이를 사용하려고 할 때마다 확인 버튼을 눌러야 연결되므로 불편을 초래함

# 해결

1. 다이얼로그에서 'Show Certificate' 클릭 후 관련된 인증서들을 확인
2. 키체인 접근(Keychain access) 실행
3. 모든 탭에서 관련된 인증서를 찾아 전부 삭제
4. 네트워크에 다시 연결 후 추가된 인증서의 컨텍스트 메뉴에서 Get info 클릭
5. 'When using this certificate'에서 'Always Trust'를 선택

# 참고문헌

- [Apple discussions "Wi-Fi Connection to WPA2 Enterprise Keeps Asking to Verify Certificate"](https://discussions.apple.com/thread/7201481)
- [Superuser "Mac OS X “Verify Certificate” every time connecting to secure wireless"](https://superuser.com/questions/1036236/mac-os-x-verify-certificate-every-time-connecting-to-secure-wireless)