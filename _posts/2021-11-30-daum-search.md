---
layout: post
title: Daum 검색 (Rest API)
description: 이 문서는 다음(Daum) 검색 API를 안내합니다.
summary: Daum 검색 API는 포털 사이트 Daum에서 방대한 웹 문서, 동영상, 이미지, 블로그, 책, 카페를 검색하는 기능을 제공합니다. 검색 결과는 JSON 객체로 전달돼 서비스에서 자유롭게 출력하거나 활용할 수 있습니다.
tags: 
minute: 1
---
``` json
GET /v2/search/web HTTP/1.1
Host: dapi.kakao.com
Authorization: KakaoAK {REST_API_KEY}
```