---
layout: post
title: Jetpack Compose - Slider + Circle
description: Jetpack Compose - Slider + Circle
summary: Jetpack Compose - Slider + Circle
tags: 
minute: 1
---
```kotlin
@Composable
fun Ex1_1() {
    Column(
        modifier = Modifier.padding(20.dp)
    ) {
        var sliderProgress by remember { mutableStateOf(0.5f) }
        Slider(
            value = sliderProgress,
            onValueChange = { sliderProgress = it },
            colors = SliderDefaults.colors(
                thumbColor = Color.Red,
                activeTickColor = Color.Black,
                inactiveTickColor = Color.Gray
            )
        )
        SliderCircle(sliderProgress)
    }
}

@Composable
fun SliderCircle(sliderProgress: Float) {
    Box(
        modifier = Modifier
            .fillMaxWidth()
            .height(300.dp),
        contentAlignment = Alignment.Center
    ) {
        Canvas(
            modifier = Modifier
                .width(250.dp)
                .height(250.dp)
        ) {
            drawArc(
                brush = SolidColor(Color.Gray),
                startAngle = 0f,
                sweepAngle = 360f,
                useCenter = false,
                style = Stroke(35f)
            )
            val sliderChangedProgress = sliderProgress * 360
            drawArc(
                brush = SolidColor(Color.Black),
                startAngle = 0f,
                sweepAngle = sliderChangedProgress,
                useCenter = false,
                style = Stroke(35f, cap = StrokeCap.Round)
            )
        }
        Text(
            text = "${(sliderProgress * 100)} %",
            fontSize = 30.sp,
            fontWeight = FontWeight.ExtraBold
        )
    }
}
```