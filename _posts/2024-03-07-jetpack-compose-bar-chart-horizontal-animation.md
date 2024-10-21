---
layout: post
title: Jetpack Compose - Bar Chart 가로 애니메이션
description: Jetpack Compose - Bar Chart 가로 애니메이션
summary: Jetpack Compose - Bar Chart 가로 애니메이션
tags: 
minute: 1
---
```kotlin
@Composable
fun Ex1_1() {
    val barDataList = listOf(0.2f, 0.4f, 0.6f, 0.8f, 1f)
    val fullWidth = 320.dp
    Box(modifier = Modifier.fillMaxSize()) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(20.dp),
            verticalArrangement = Arrangement.SpaceBetween
        ) {
            barDataList.forEachIndexed { index, it ->
                var resultWidth by remember { mutableStateOf(0.dp) }
                val animatedWidth by animateDpAsState(
                    targetValue = resultWidth,
                    animationSpec = tween(durationMillis = 6000, easing = LinearOutSlowInEasing),
                    label = "Bar Chart Horizontal Animation"
                )
                LaunchedEffect(true) {
                    delay(1000L * index)
                    resultWidth = fullWidth * it
                }
                Row {
                    Box(
                        modifier = Modifier
//                            .fillMaxWidth(fraction = (it * 0.8).toFloat())
                            .width(animatedWidth)
                            .height(30.dp)
                            .background(
                                Color.Black,
                                shape = RoundedCornerShape(bottomEnd = 15.dp, topEnd = 15.dp)
                            )
                    )
                    Text(
                        text = "${(it*100).toInt()}%",
                        modifier = Modifier.padding(top = 3.dp, start = 10.dp),
                        fontWeight = FontWeight.Bold
                    )
                }
            }
        }
    }
}
```