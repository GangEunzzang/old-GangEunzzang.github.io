---
title: '[기술 면접] 네트워크 정리'
layout: post
categories: 기술면접
tags: 기술면접
comments: true
---

<details>
<summary> <b> https://www.google.com 을 접속했을 때 일어나는 일  </b> </summary>
<div markdown="1">

1) 브라우저가 URL에 적힌 값을 파싱해서 HTTP Request Message를 생성하고, OS에 전송 요청을 한다. 이때, Domain으로 요청을 보낼 수 없기 때문에 DNS LookUp을 수행한다.
2) 

</div>
</details>

<details>
<summary> <b> GET과 POST 차이  </b> </summary>
<div markdown="1">

- GET
  - 요청 데이터가 `HTTP Request Message`의 Header 부분에 url 이 담겨서 전송된다.
  - 전송할 수 있는 데이터의 크기가 제한적이다.
  - 보안이 필요한 데이터에 대해서는 적절하지 않다.

- POST
  - 요청 데이터가 `HTTP Request Message`의 Body 부분에 데이터가 담겨서 전송된다.
  - 서버의 상태를 변경시키기 때문에 멱등성이 유지되지 않는다.  

부수적인 차이점을 좀 더 살펴보면 GET 방식의 요청은 브라우저에서 `Caching` 할 수 있다.  
때문에 POST 방식으로 요쳥해야 할 것을 보내는 데이터가 작고 보안적인 문제가 없다는 이유로 GET 방식으로 요청한다면,  
기존에 캐싱 되었던 데이터가 응답될 가능성이 존재한다.

</div>
</details>

<details>
<summary> <b> TCP와 UDP의 차이  </b> </summary>
<div markdown="1">

- TCP(Transmission Control Protocol)
  - 신뢰성 있는 데이터 전송을 위한 연결 지향성 프로토콜
  - UDP에 비해 속도가 느리다
  - 파일 전송, 이메일 전송과 같은 신뢰성이 중요한 서비스에 사용된다.

- UDP(User Datagram Protocol)
  - 연걸 설정 및 확인 단계 없이 데이터 전송하는 비연결 지향성 프로토콜
  - 데이터 손실이나 순서 변경 가능성이 존재하며, 수신 확인 또는 재전송을 처리하지 않는다.
  - 실시간 스트리밍, 온라인 게임, DNS 등과 같은 서비스에 사용.

</div>
</details>

## 참고
- [백엔드 개발자로 입사를 준비하며 받았던 질문, 예상했던 질문, 인터넷 참고한 질문(CC BY-NC)](https://github.dev/ksundong/backend-interview-question)
- [기술면접 정리](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/Network)