---
layout: post
title: Google App Engine - Java
description: Google App Engine - Java
summary: Google App Engine - Java
tags: 
minute: 1
---
1. 구글 SDK에 추가 컴퍼넌트 설치    
gcloud components update app-engine-java    
gcloud components update    

2. Hello World 앱 다운로드    
git clone https://github.com/GoogleCloudPlatform/java-docs-samples    
cd java-docs-samples/flexible/helloworld    

3. 로컬 머신에서 Hello World 실행    
mvn jetty:run-exploded    
http://localhost:8080    

4. App Engine에서 Hello World 배포 및 실행    
mvn clean package appengine:deploy    
gcloud app browse    