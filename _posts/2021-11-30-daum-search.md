---
layout: post
title: Daum 검색 (Rest API)
description: 다음(Daum) 검색 API
summary: Daum 검색 API는 포털 사이트 Daum에서 방대한 웹 문서, 동영상, 이미지, 블로그, 책, 카페를 검색하는 기능을 제공
tags: 
minute: 1
---
1. [웹문서](https://developers.kakao.com/docs/latest/ko/daum-search/dev-guide#search-doc)    
Method - GET    
Property - Authorization: KakaoAK {REST_API_KEY}    
URL - https://dapi.kakao.com/v2/search/web?query=이효리&sort=accuracy&page=1&size=10    
2. [동영상](https://developers.kakao.com/docs/latest/ko/daum-search/dev-guide#search-video)    
Method - GET    
Property - Authorization: KakaoAK {REST_API_KEY}    
URL - https://dapi.kakao.com/v2/search/vclip?query=AOA&sort=accuracy&page=1&size=15    
2. [이미지]](https://developers.kakao.com/docs/latest/ko/daum-search/dev-guide#search-image)    
Method - GET    
Property - Authorization: KakaoAK {REST_API_KEY}    
URL - https://dapi.kakao.com/v2/search/image?query=설현&sort=accuracy&page=1&size=80    