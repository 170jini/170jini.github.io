---
layout: post
title: Jetpack Compose - 주사위 만들기
description: Jetpack Compose - 주사위 만들기
summary: Jetpack Compose - 주사위 만들기
tags: 
minute: 1
---
```kotlin
@Composable
fun MyDiceApp() {
    var diceNumber by remember {
        mutableStateOf(1)
    }
    Column(
        modifier = Modifier
            .fillMaxSize()
            .background(Color.LightGray),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Box(
            modifier = Modifier
                .size(300.dp)
                .border(3.dp, Color.Black)
                .background(Color.White)
                .padding(20.dp),
            contentAlignment = Alignment.Center
        ) {
            when(diceNumber) {
                1 -> DiceNumberCircle1()
                2 -> DiceNumberCircle2()
                3 -> DiceNumberCircle3()
                4 -> DiceNumberCircle4()
                5 -> DiceNumberCircle5()
                6 -> DiceNumberCircle6()
            }
        }
        Button(
            onClick = {
                diceNumber = Random.nextInt(1, 7)
            },
            modifier = Modifier
                .fillMaxWidth()
                .padding(50.dp)
                .height(50.dp),
            colors = ButtonDefaults.buttonColors(
                containerColor = Color.White
            )
        ) {
            Text(
                text = "rolling the dice",
                color = Color.Black,
                fontWeight = FontWeight.Bold,
                textAlign = TextAlign.Center,
                fontSize = 20.sp,
                modifier = Modifier.fillMaxWidth()
            )
        }
        Text(
            text = diceNumber.toString(),
            fontWeight = FontWeight.Bold,
            fontSize = 30.sp
        )
    }
}

@Composable
fun DiceNumberCircle1() {
    Box(
        modifier = Modifier.size(50.dp)
    ) {
        Canvas(
            modifier = Modifier.fillMaxSize()
        ) {
            drawCircle(Color.Black, radius = size.minDimension / 10)
        }
    }
}

@Composable
fun DiceNumberCircle2() {
    Row {
        DiceNumberCircle1()
        Spacer(modifier = Modifier.size(50.dp))
        DiceNumberCircle1()
    }
}

@Composable
fun DiceNumberCircle3() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceBetween
    ) {
        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceBetween
        ) {
            DiceNumberCircle1()
            Spacer(modifier = Modifier.size(50.dp))
            Spacer(modifier = Modifier.size(50.dp))
        }
        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceBetween
        ) {
            Spacer(modifier = Modifier.size(50.dp))
            DiceNumberCircle1()
            Spacer(modifier = Modifier.size(50.dp))
        }
        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceBetween
        ) {
            Spacer(modifier = Modifier.size(50.dp))
            Spacer(modifier = Modifier.size(50.dp))
            DiceNumberCircle1()
        }
    }
}

@Composable
fun DiceNumberCircle4() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceBetween,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        DiceNumberCircle2()
        DiceNumberCircle2()
    }
}

@Composable
fun DiceNumberCircle5() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceBetween,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        DiceNumberCircle2()
        DiceNumberCircle1()
        DiceNumberCircle2()
    }
}

@Composable
fun DiceNumberCircle6() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceBetween,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        DiceNumberCircle2()
        DiceNumberCircle2()
        DiceNumberCircle2()
    }
}
```