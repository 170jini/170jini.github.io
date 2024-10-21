---
layout: post
title: Jetpack Compose - 이력서 앱 만들기
description: Jetpack Compose - 이력서 앱 만들기
summary: Jetpack Compose - 이력서 앱 만들기
tags: 
minute: 1
---
```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MyResume() {
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text(text = "Android Dev Resume") }
            )
        }
    ) {
        MyResumeContent(it)
    }
}

@Composable
fun MyResumeContent(paddingValues: PaddingValues) {
    val context = LocalContext.current
    Card(
        modifier = Modifier
            .fillMaxSize()
            .padding(paddingValues)
            .padding(20.dp),
        elevation = CardDefaults.cardElevation(
            defaultElevation = 10.dp
        ),
        shape = RoundedCornerShape(30.dp)
    ) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(20.dp)
        ) {
            Image(
                painter = painterResource(id = R.drawable.bok),
                contentDescription = "profile",
                modifier = Modifier
                    .size(150.dp)
                    .clip(CircleShape)
                    .align(Alignment.CenterHorizontally)
            )
            Spacer(modifier = Modifier.height(20.dp))
            Text(
                text = "자기 소개",
                fontSize = 20.sp,
                modifier = Modifier.align(Alignment.CenterHorizontally)
            )
            Spacer(modifier = Modifier.height(10.dp))
            Divider(color = Color.Gray, thickness = 1.dp)
            Spacer(modifier = Modifier.height(10.dp))
            Text(
                text = "안녕하세요. 저는 개발자입니다. 새로운 기술을 배우는 것을 좋아하고, 언제나 개발에 열정을 가지고 있습니다.",
                fontSize = 15.sp,
                modifier = Modifier.align(Alignment.CenterHorizontally)
            )
            Spacer(modifier = Modifier.height(10.dp))
            Text(
                text = "사실 위의 말은 뻥이고 월급을 받기 위해 개발자를 하고 있습니다.",
                color = Color.Red,
                fontSize = 15.sp,
                modifier = Modifier.align(Alignment.CenterHorizontally)
            )
            Spacer(modifier = Modifier.height(10.dp))
            Divider(color = Color.Gray, thickness = 1.dp)
            Spacer(modifier = Modifier.height(10.dp))
            Text(
                text = "핸드폰 번호 : 010-1234-5678",
                modifier = Modifier.padding(10.dp)
            )
            Text(
                text = "이메일 : abc@naver.com",
                modifier = Modifier.padding(10.dp)
            )
            Button(
                onClick = {
                    val intent = Intent(Intent.ACTION_DIAL, Uri.parse("tel:01012345678"))
                    context.startActivity(intent)
                }
            ) {
                Text(text = "전화 걸기")
            }
            Button(
                onClick = {
                    val intent = Intent(Intent.ACTION_SENDTO).apply {
                        data = Uri.parse("mailto:abc@naver.com")
                    }
                    context.startActivity(intent)
                }
            ) {
                Text(text = "이메일 보내기")
            }
        }
    }
}
```