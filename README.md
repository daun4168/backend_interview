# Backend Interview
백엔드 인터뷰의 질문 및 답변 내용에 대해 정리하였습니다. 
CS인터뷰를 준비하는데 도움이 되기를 바랍니다. 


## Table Of Contents
- [데이터베이스](#데이터베이스)
- [네트워크](#네트워크)
- [운영체제](#운영체제)
- [자료구조&알고리즘](#자료구조&알고리즘)
- [컴퓨터보안](#컴퓨터보안)
- [프로그래밍 언어](#프로그래밍-언어)
- [기술동향](#기술동향)
- [기타](#기타)
- [참고자료](#참고자료)


<details>
  <summary>질문질문?</summary>
  </br>
  답변답변
  
  </br>
</details>


## 데이터베이스


## 네트워크
<details>
  <summary>웹사이트에 접속할 때 무슨 일이 일어나나요?</summary>
  </br>
  주소창에 URL을 입력하면 브라우저는 DNS서버에 요청을 해서 IP주소를 얻습니다. 
  IP주소를 얻으면 HTTP를 이용해서 IP주소로 웹사이트에 대해 요청합니다. 
  서버는 요청을 받으면, 처리해서 다시 응답을 보냅니다. 
  브라우저는 응답을 받으면 HTML코드를 파싱해서 화면에 출력합니다. 
  </br>
</details>

<details>
  <summary>DNS서버에 요청하는 과정을 자세하게 설명해보세요.</summary>
  </br>
  브라우저는 DNS서버에 요청하기 전, 브라우저에 도메인이 캐싱되어 있는지 확인합니다.
  없을 경우, OS의 hosts파일에 도메인이 있는지 확인합니다. 없을 경우, local dns서버에 물어봅니다. 
  local dns서버는 root dns서버에게 물어보고, root dns서버는 국가코드에 따라 
  top-level name server에 물어봅니다. top-level name server는 그 아래 서버에 요청하는 과정으로
  IP주소를 찾습니다. 물론 각 서버는 한번 요청한 이후 캐시를 저장하고 있어 동일한 요청에 대해 계속
  다른 DNS서버로 요청을 보내지는 않습니다. 
  
  DNS서버에 요청을 보낼 때, 
  </br>
</details>

## 운영체제


## 자료구조&알고리즘


## 컴퓨터보안


## 프로그래밍 언어


## 기술동향


## 기타


## 참고자료
[네이버 기술 블로그](https://d2.naver.com/helloworld)

[라인 기술 블로그](https://engineering.linecorp.com/ko/blog/)

[카카오 기술 블로그](https://tech.kakao.com/blog/)

[쿠팡 기술 블로그](https://medium.com/coupang-tech/technote/home)

[우아한형제들 기술 블로그](https://woowabros.github.io/)

https://github.com/ksundong/backend-interview-question



