---
layout: post
title: Jetpack Compose - PieChart / DonutChart
description: Jetpack Compose - PieChart / DonutChart
summary: Jetpack Compose - PieChart / DonutChart
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
                        sweepAngle = it.fraction * 360f,
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