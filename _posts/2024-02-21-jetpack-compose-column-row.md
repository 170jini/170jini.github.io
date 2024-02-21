---
layout: post
title: Jetpack Compose - Column + Row
description: Jetpack Compose - Column + Row
summary: Jetpack Compose - Column + Row
tags: 
minute: 1
---
Arrangement
```kotlin
Column(
    modifier = Modifier
        .fillMaxSize()
        .padding(20.dp)
        .background(Color.Gray)
) {
    Text(
        text = "Hello",
        color = Color.Blue,
        fontSize = 20.sp
    )
    Row(
        modifier = Modifier.fillMaxWidth(),
        horizontalArrangement = Arrangement.SpaceBetween
//            horizontalArrangement = Arrangement.SpaceEvenly
//            horizontalArrangement = Arrangement.SpaceAround
    ) {
        Text(text = "Left")
        Text(text = "Center")
        Text(text = "Right")
    }
    Text(
        text = "Glad to you",
        color = Color.Red,
        fontSize = 20.sp
    )
}
```
Column + Row
```kotlin
Column(
    modifier = Modifier
        .fillMaxSize()
        .padding(20.dp)
        .background(Color.Cyan)
        .border(
            border = BorderStroke(5.dp, color = Color.Blue)
        )
) {
    Box(
        modifier = Modifier.padding(top = 20.dp, start = 10.dp)
    ) {
        Image(
            painter = painterResource(id = R.drawable.icons8),
            contentDescription = "fish",
            modifier = Modifier
                .size(100.dp)
                .clip(RoundedCornerShape(50.dp))
        )
    }
    Text(
        text = "SW Developer",
        fontSize = 20.sp,
        fontWeight = FontWeight.Bold,
        modifier = Modifier.padding(top = 50.dp, start = 10.dp)
    )
    Text(
        text = "Ryan Sim",
        fontSize = 15.sp,
        modifier = Modifier.padding(top = 10.dp, start = 10.dp)
    )
    Row(
        modifier = Modifier.fillMaxWidth()
    ) {
        Text(
            text = "Email",
            fontSize = 15.sp,
            fontWeight = FontWeight.Bold,
            modifier = Modifier.padding(top = 10.dp, start = 10.dp)
        )
        Text(
            text = "ryion76@naver.com",
            fontSize = 15.sp,
            modifier = Modifier.padding(start = 10.dp, top = 10.dp),
            color = Color.Blue
        )
    }
    Row(
        modifier = Modifier.fillMaxWidth()
    ) {
        Text(
            text = "Phone",
            fontSize = 15.sp,
            fontWeight = FontWeight.Bold,
            modifier = Modifier.padding(top = 10.dp, start = 10.dp)
        )
        Text(
            text = "010-1234-5678",
            fontSize = 15.sp,
            modifier = Modifier.padding(start = 10.dp, top = 10.dp)
        )
    }
}
```