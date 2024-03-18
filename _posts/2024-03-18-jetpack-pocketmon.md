---
layout: post
title: Jetpack Compose - 포켓몬 카드 만들기
description: Jetpack Compose - 포켓몬 카드 만들기
summary: Jetpack Compose - 포켓몬 카드 만들기
tags: 
minute: 1
---
```kotlin
@Composable
fun PocketCard() {
    var cardFront by remember {
        mutableStateOf(true)
    }
    val animationDegree by animateFloatAsState(
        targetValue = if (cardFront) 0f else 180f,
        animationSpec = tween(500),
        label = "animationDegree"
    )
    Log.d("cardFront", cardFront.toString())
    Log.d("animationDegree", animationDegree.toString())
    Box(
        modifier = Modifier
            .fillMaxSize()
            .padding(top = 50.dp, bottom = 50.dp, start = 20.dp, end = 20.dp)
            .clickable {
                cardFront = !cardFront
            }
            .graphicsLayer {
                rotationY = animationDegree
            }
            //.background(Color.Gray)
    ) {
        if (animationDegree <= 90) {
            PocketFront()
        } else {
            PocketBack()
        }
    }
}

@Composable
fun PocketFront() {
    Box(
        modifier = Modifier
            .fillMaxSize()
            .background(Color(0xffffd700), shape = RoundedCornerShape(30.dp))
    ) {
        Box(
            modifier = Modifier
                .fillMaxSize()
                .padding(10.dp)
                .background(Color.Black, shape = RoundedCornerShape(30.dp)),
            contentAlignment = Alignment.Center
        ) {
            Image(
                painter = painterResource(id = R.drawable.card),
                contentDescription = null
            )
        }
    }
}

@Composable
fun PocketBack() {
    Box(
        modifier = Modifier
            .fillMaxSize()
            .background(Color(0xffffd700), shape = RoundedCornerShape(30.dp))
    ) {
        Box(
            modifier = Modifier
                .fillMaxSize()
                .padding(10.dp)
                .background(Color.Red, shape = RoundedCornerShape(30.dp))
                .graphicsLayer {
                    rotationY = 180f
                },
            contentAlignment = Alignment.Center
        ) {
            Column(
                modifier = Modifier.fillMaxSize(),
                verticalArrangement = Arrangement.Center,
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                Image(
                    painter = painterResource(id = R.drawable.img),
                    contentDescription = null
                )
                Spacer(modifier = Modifier.padding(20.dp))
                Text(
                    text = "파이리",
                    fontSize = 30.sp,
                    color = Color.White,
                    fontWeight = FontWeight.ExtraBold
                )
            }
        }
    }
}
```