---
layout: post
title: Jetpack Compose - Navigation
description: Jetpack Compose - Navigation
summary: Jetpack Compose - Navigation
tags: 
minute: 1
---
build.gradle
```xml
implementation("androidx.navigation:navigation-compose:2.7.7")
```
navigation1
```kotlin
@Composable
fun MyScreen1(navController : NavHostController) {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "화면1",
            fontSize = 50.sp
        )
        Button(onClick = {
            navController.navigate("myScreen2")
        }
        ) {
            Text(
                text = "2번 화면으로 가기",
                fontSize = 30.sp
            )
        }
    }
}

@Composable
fun MyScreen2(navController : NavHostController) {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "화면2",
            fontSize = 50.sp
        )
        Button(onClick = {
            navController.navigate("myScreen3")
        }
        ) {
            Text(
                text = "3번 화면으로 가기",
                fontSize = 30.sp
            )
        }
    }
}

@Composable
fun MyScreen3(navController : NavHostController) {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "화면3",
            fontSize = 50.sp
        )
        Button(onClick = {
            navController.navigate("myScreen1")
        }
        ) {
            Text(
                text = "1번 화면으로 가기",
                fontSize = 30.sp
            )
        }
    }
}

@Composable
fun MyNav() {
    val navController = rememberNavController()

    NavHost(
        navController = navController,
        startDestination = "myScreen1"
    ) {
        composable("myScreen1") {
            MyScreen1(navController = navController)
        }
        composable("myScreen2") {
            MyScreen2(navController = navController)
        }
        composable("myScreen3") {
            MyScreen3(navController = navController)
        }
    }
}
```
navigation2
```kotlin
@Composable
fun MyNav(navHostController: NavHostController) {
    NavHost(navController = navHostController, startDestination = "myGridScreen") {
        composable("myGridScreen") {
            MyGridScreen(navHostController)
        }
        composable("myNumberScreen/{number}") { navBackStakEntry ->
            MyNumberScreen(navHostController, number = navBackStakEntry.arguments?.getString("number"))
        }
    }
}

@Composable
fun MyGridScreen(navHostController: NavHostController) {
    LazyVerticalGrid(
        columns = GridCells.Fixed(3) ,
        modifier = Modifier.padding(20.dp)
    ) {
        items(15) {number ->
            Box(
                contentAlignment = Alignment.Center,
                modifier = Modifier
                    .fillMaxWidth()
                    .height(100.dp)
                    .border(1.dp, Color.Black)
                    .clickable {
                        navHostController.navigate("myNumberScreen/$number")
                    }
            ) {
                Text(
                    text = number.toString(),
                    fontSize = 30.sp
                )
            }
        }
    }
}

@Composable
fun MyNumberScreen(navHostController: NavHostController, number: String?) {
    Box(
        contentAlignment = Alignment.Center,
        modifier = Modifier
            .fillMaxSize()
            .clickable {
                navHostController.popBackStack()
            }
    ) {
        Text(
            text = number.toString(),
            fontSize = 70.sp
        )
    }
}
```