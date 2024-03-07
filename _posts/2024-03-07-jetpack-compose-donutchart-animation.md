---
layout: post
title: Jetpack Compose - 도넛차트 애니메이션
description: Jetpack Compose - 도넛차트 애니메이션
summary: Jetpack Compose - 도넛차트 애니메이션
tags: 
minute: 1
---
```kotlin
data class ChartModel(val fraction : Float, val color: Color)

@Composable
fun Ex1_1() {
    val items = listOf(
        ChartModel(fraction = 0.2f, color = Color.Red),
        ChartModel(fraction = 0.3f, color = Color.Green),
        ChartModel(fraction = 0.5f, color = Color.Black)
    )
    var animationProgress by remember { mutableStateOf(0f) }
    val animationState by animateFloatAsState(
        targetValue = animationProgress,
        animationSpec = tween(durationMillis = 1500, easing = LinearOutSlowInEasing),
        label = "Donut Chart Animation"
    )
    LaunchedEffect(Unit) {
        animationProgress = 1f
    }
    var startAngle = 0f
    Box(
        modifier = Modifier.fillMaxSize(),
        contentAlignment = Alignment.Center
    ) {
        Box(
            modifier = Modifier
                .size(300.dp)
        ) {
            items.forEach {
                Canvas(modifier = Modifier.fillMaxSize()) {
                    drawArc(
                        color = it.color,
                        startAngle = startAngle,
                        sweepAngle = it.fraction * animationState * 360f,
                        useCenter = false,
                        size = Size(size.width, size.height),
                        style = Stroke(width = 200f)
                    )
                    startAngle += it.fraction * 360f
                }
            }
        }
    }
}
```