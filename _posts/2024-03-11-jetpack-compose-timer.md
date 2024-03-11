---
layout: post
title: Jetpack Compose - 타이머
description: Jetpack Compose - 타이머
summary: Jetpack Compose - 타이머
tags: 
minute: 1
---
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                Box(modifier = Modifier.padding(40.dp)) {
                    Clock()
                }
            }
        }
    }
}

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun Clock() {
    val context = LocalContext.current
    var inputText by remember { mutableStateOf("") }
    var progress by remember { mutableStateOf(0) }
    LaunchedEffect(progress) {
        if (progress > 0) {
            delay(1000)
            progress -= 1
        }
    }
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(15.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        TextField(
            value = inputText,
            onValueChange = {
                inputText = it
            },
            label = {
                Text(text = "Input Time (1~60)")
            },
            colors = TextFieldDefaults.textFieldColors(
                focusedIndicatorColor = Color.Gray,
                unfocusedIndicatorColor = Color.White,
                cursorColor = Color.Gray
            )
        )
        Spacer(modifier = Modifier.padding(10.dp))
        Button(
            onClick = {
                try {
                    val number = inputText.toInt()
                    if (number in 1..60) {
                        progress = number
                    } else {
                        Log.d("TAG", "Please enter a value between 1-60")
                        Toast.makeText(context, "Please enter a value between 1-60", Toast.LENGTH_LONG).show()
                    }
                } catch (e: NumberFormatException) {
                    Log.d("TAG", "Please enter the numbers correctly")
                    Toast.makeText(context, "Please enter the numbers correctly", Toast.LENGTH_LONG).show()
                }
            },
            modifier = Modifier.fillMaxWidth(),
            colors = ButtonDefaults.buttonColors(Color.Black)
        ) {
            Text(
                text = "Time Settings",
                fontSize = 20.sp,
                fontWeight = FontWeight.Bold,
                color = Color.White
            )
        }
        Canvas(
            modifier = Modifier.fillMaxSize()
        ) {
            val center = Offset(size.width / 2, size.height / 2)
            val radius = size.minDimension / 2
            for (second in 0 until 60) {
                val angle = Math.toRadians(second * 6.0)
//                val startRadius = radius - 10.dp.toPx()
                val startRadius = if (second % 5 == 0) radius - 20.dp.toPx() else radius - 10.dp.toPx()
                val endRadius = radius
                val startX = center.x + cos(angle).toFloat() * startRadius
                val endX = center.x + cos(angle).toFloat() * endRadius
                val startY = center.y + sin(angle).toFloat() * startRadius
                val endY = center.y + sin(angle).toFloat() * endRadius
                drawLine(
                    Color.Black,
                    start = Offset(startX, startY),
                    end = Offset(endX, endY),
                    strokeWidth = if (second % 5 == 0) 3.dp.toPx() else 1.dp.toPx()
                )
            }
            val sweepAngle = (progress.toFloat() / 60f) * 360f
            drawArc(
                color = Color.Red,
                startAngle = -90f,
                sweepAngle = sweepAngle,
                useCenter = true,
                topLeft = Offset(center.x - radius + 75, center.y - radius + 75),
                size = Size(radius * 2 - 150, radius * 2 - 150),
                style = Fill
            )
        }
    }
}
```