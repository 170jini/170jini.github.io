---
layout: post
title: Local (Rest API)
description: 로컬(Local) API
summary: 로컬(local) API는 키워드로 특정 장소 정보를 조회하거나, 좌표를 주소 또는 행정구역으로 변환하는 등 장소에 대한 정보를 제공
tags: 
minute: 1
---
1. [주소](https://developers.kakao.com/docs/latest/ko/local/dev-guide#address-coord)    
https://dapi.kakao.com/v2/local/search/address.json?query=전북 삼성동 100&analyze_type=similar&page=1&size=10    
2. [좌표로 행정구역정보](https://developers.kakao.com/docs/latest/ko/local/dev-guide#coord-to-district)    
https://dapi.kakao.com/v2/local/geo/coord2regioncode.json?x=127.1086228&y=37.4012191&input_coord=WGS84&output_coord=WGS84    
3. [좌표로 주소](https://developers.kakao.com/docs/latest/ko/local/dev-guide#coord-to-address)    
https://dapi.kakao.com/v2/local/geo/coord2address.json?x=127.1086228&y=37.4012191&input_coord=WGS84    
4. [좌표계 변환](https://developers.kakao.com/docs/latest/ko/local/dev-guide#trans-coord)    
https://dapi.kakao.com/v2/local/geo/transcoord.json?x=160710.37729270622&y=-4388.879299157299&input_coord=WTM&output_coord=WGS84    
5. [키워드로 장소](https://developers.kakao.com/docs/latest/ko/local/dev-guide#search-by-keyword)    
https://dapi.kakao.com/v2/local/search/keyword.json?query=카카오프렌즈&y=37.514322572335935&x=127.06283102249932&radius=20000    
6. [카테고리로 장소](https://developers.kakao.com/docs/latest/ko/local/dev-guide#search-by-category)    
https://dapi.kakao.com/v2/local/search/category.json?category_group_code=PM9&y=37.514322572335935&x=127.06283102249932&radius=20000    
