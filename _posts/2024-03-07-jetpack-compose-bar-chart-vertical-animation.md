---
layout: post
title: Jetpack Compose - Bar Chart 세로 애니메이션
description: Jetpack Compose - Bar Chart 세로 애니메이션
summary: Jetpack Compose - Bar Chart 세로 애니메이션
tags: 
minute: 1
---
```kotlin
@Composable
fun Ex1_1() {
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.BottomStart
    ) {
        val barDataList = listOf(0.2f, 0.4f, 0.6f, 0.8f, 1f)
        val fullHeight = 500.dp
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .height(600.dp)
                .padding(20.dp),
            horizontalArrangement = Arrangement.SpaceBetween,
            verticalAlignment = Alignment.Bottom
        ) {
            barDataList.forEachIndexed { index, it ->
                var resultHeight by remember { mutableStateOf(0.dp) }
                LaunchedEffect(true) {
                    delay(1000L * index)
                    resultHeight = fullHeight * it
                }
                val animatedHeight by animateDpAsState(
                    targetValue = resultHeight,
                    animationSpec = tween(durationMillis = 6000, easing = LinearOutSlowInEasing),
                    label = "Bar Chart"
                )
                Column(
                    horizontalAlignment = Alignment.CenterHorizontally
                ) {
                    Text(
                        text = "${(it*100).toInt()}%"
                    )
                    Box(
                        modifier = Modifier
//                            .fillMaxHeight(fraction = it)
                            .height(animatedHeight)
                            .width(30.dp)
                            .background(
                                Color.Black,
                                shape = RoundedCornerShape(topStart = 15.dp, topEnd = 15.dp)
                            )
                    )
                }
            }
        }
    }
}
```