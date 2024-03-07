---
layout: post
title: Jetpack Compose - Text 애니메이션
description: Jetpack Compose - Text 애니메이션
summary: Jetpack Compose - Text 애니메이션
tags: 
minute: 1
---
```kotlin
@Composable
fun Ex1_1() {
    var resultMoney by remember { mutableStateOf(0) }
    Box(
        modifier = Modifier
            .fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        LaunchedEffect(true) {
            resultMoney = 100000000
        }
        val animatedMoney by animateIntAsState(
            targetValue = resultMoney,
            animationSpec = tween(5000),
            label = "Text Animation"
        )
        val formattedResultMoney = NumberFormat.getNumberInstance().format(animatedMoney)
        Text(
            text = "$formattedResultMoney won",
            fontSize = 50.sp
        )
//        Button(
//            modifier = Modifier
//                .width(150.dp)
//                .padding(top = 150.dp),
//            onClick = {
//                resultMoney = 100000000
//            }
//        ) {
//            Text(text = "GO")
//        }
    }
}
```