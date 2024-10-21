---
layout: post
title: Jetpack Compose - 그래프의 텍스트 쓰기
description: Jetpack Compose - 그래프의 텍스트 쓰기
summary: Jetpack Compose - 그래프의 텍스트 쓰기
tags: 
minute: 1
---
```kotlin
data class ChartModel(val fraction : Float, val color: Color)

@Composable
fun Ex1_1() {
    val items = listOf(
        ChartModel(fraction = 0.2f, color = Color.Red),
        ChartModel(fraction = 0.3f, color = Color.Blue),
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
                val fraction = (it.fraction * 100).toInt().toString() + "%"
                Canvas(modifier = Modifier.fillMaxSize()) {
                    drawArc(
                        color = it.color,
                        startAngle = startAngle,
                        sweepAngle = it.fraction * animationState * 360f,
                        useCenter = true,
                        size = Size(size.width, size.height),
                        style = Fill
                    )
                    val paint = Paint().asFrameworkPaint().apply {
                        color = android.graphics.Color.WHITE
                        textSize = 60f
                    }
                    val midPosition = startAngle + it.fraction * 180f
                    val radiusPosition = size.width * 0.5f * 0.5f
                    val xPosition = (radiusPosition * kotlin.math.cos(midPosition * (Math.PI / 180))).toFloat() + size.width * 0.5f
                    val yPosition = (radiusPosition * kotlin.math.sin(midPosition * (Math.PI / 180))).toFloat() + size.height * 0.5f
                    val textWidth = paint.measureText(it.fraction.toString())
                    val textHeight = paint.descent() - paint.ascent()
                    val xPositionChanged = xPosition - textWidth * 0.5f
                    val yPositionChanged = yPosition + textHeight * 0.5f
                    drawIntoCanvas {
                        it.nativeCanvas.drawText(fraction, xPositionChanged, yPositionChanged, paint)
                    }
                    startAngle += it.fraction * 360f
                }
            }
        }
    }
}
```