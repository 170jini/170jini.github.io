---
layout: post
title: Jetpack Compose - 그래프 앱 만들기
description: Jetpack Compose - 그래프 앱 만들기
summary: Jetpack Compose - 그래프 앱 만들기
tags: 
minute: 1
---
AndroidManifest.xml
build.gradle
```xml
implementation("androidx.navigation:navigation-compose:2.7.7")
```
MainActivity.kt
```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun GraphAppMain() {
    val navController = rememberNavController()
    val navItems = listOf(
        NavigationItem("Graph1", Icons.Default.AddCircle, "tab1"),
        NavigationItem("Graph2", Icons.Default.AddCircle, "tab2"),
        NavigationItem("Graph3", Icons.Default.AddCircle, "tab3")
    )
    Scaffold(
        bottomBar = {
            BottomAppBar {
                Row(
                    modifier = Modifier.fillMaxWidth(),
                    horizontalArrangement = Arrangement.SpaceAround
                ) {
                    navItems.forEach {navigationItem ->
                        val currentRoute = navController.currentBackStackEntryAsState().value?.destination?.route
                        Column(
                            verticalArrangement = Arrangement.Center,
                            horizontalAlignment = Alignment.CenterHorizontally,
                            modifier = Modifier.clickable {
                                navController.navigate(navigationItem.route)
                            }
                        ) {
                            val isCurrentRoute = navigationItem.route == currentRoute
                            Icon(
                                imageVector = navigationItem.icon,
                                contentDescription = navigationItem.name,
                                tint = if (isCurrentRoute) Color.Red else Color.Black
                            )
                            Text(
                                text = navigationItem.name,
                                color = if (isCurrentRoute) Color.Red else Color.Black
                            )
                        }
                    }
                }
            }
        }
    ) {paddingValues ->
        NavHost(
            navController = navController,
            startDestination = navItems.first().route,
            modifier = Modifier.padding(paddingValues)
        ) {
            composable("tab1") {
                Graph1()
            }
            composable("tab2") {
                Graph2()
            }
            composable("tab3") {
                Graph3()
            }
        }
    }
}

data class NavigationItem(
    val name : String,
    val icon : ImageVector,
    val route : String
)
```
Graph1.kt
```kotlin
@Composable
fun Graph1() {
    Box(
        modifier = Modifier.padding(top = 120.dp)
    ) {
        Graph1Gauge(70f, 100f)
    }
}

@Composable
fun Graph1Gauge(percent : Float, maxPercent : Float) {
    val colorPercent = 360 * (percent / maxPercent)
    Box(
        modifier = Modifier
            .fillMaxWidth()
            .aspectRatio(1f)
            .padding(20.dp)
    ) {
        Canvas(
            modifier = Modifier.fillMaxSize()
        ) {
            drawArc(
                color = Color.LightGray,
                startAngle = 0f,
                sweepAngle = 360f,
                useCenter = false,
                style = Stroke(35f)
            )
            drawArc(
                color = Color.Blue,
                startAngle = -90f,
                sweepAngle = colorPercent,
                useCenter = false,
                style = Stroke(35f)
            )
        }
        Column(
            modifier = Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            Text(
                text = "${((percent / maxPercent) * 100).toInt()}",
                fontSize = 35.sp
            )
            Text(
                text = "$percent / $maxPercent",
                fontSize = 20.sp
            )
        }
    }
}
```
Graph2.kt
```kotlin
@Composable
fun Graph2() {
    Box(
        modifier = Modifier.padding(top = 120.dp)
    ) {
        Graph2Pie()
    }
}

@Composable
fun Graph2Pie() {
    val pieSize1 = 25f
    val pieSize2 = 75f
    val colorList = listOf(Color.Red, Color.Blue)
    PieChart(
        pieSize1,
        pieSize2,
        colorList
    )
}

@Composable
fun PieChart(pieSize1: Float, pieSize2: Float, colorList: List<Color>) {
    val totalSize = pieSize1 + pieSize2
    BoxWithConstraints(
        modifier = Modifier.padding(20.dp)
    ) {
        val pieDetailSize = constraints.maxWidth.toFloat()
        Canvas(modifier = Modifier.size(pieDetailSize.dp)) {
            val sweep1 = 360 * (pieSize1 / totalSize)
            drawArc(
                color = colorList[0],
                startAngle = 0f,
                sweepAngle = sweep1,
                useCenter = true,
                size = Size(pieDetailSize, pieDetailSize)
            )
            val sweep2 = 360 * (pieSize2 / totalSize)
            drawArc(
                color = colorList[1],
                startAngle = sweep1,
                sweepAngle = sweep2,
                useCenter = true,
                size = Size(pieDetailSize, pieDetailSize)
            )
        }
    }
}
```
Graph3.kt
```kotlin
@Composable
fun Graph3() {
    Graph3Bar()
}

@Composable
fun Graph3Bar() {
    val varDataList = listOf(10, 5, 8, 4, 7, 6, 1, 7, 3)
    BarChart(varDataList)
}

@Composable
fun BarChart(varDataList: List<Int>) {
    var maxDataValue = varDataList.max()
    Box(
        modifier = Modifier
            .fillMaxWidth()
            .padding(top = 150.dp)
    ) {
        Row(
            modifier = Modifier.fillMaxWidth(),
            verticalAlignment = Alignment.Bottom,
            horizontalArrangement = Arrangement.SpaceEvenly
        ) {
            varDataList.forEach {barData->
                Bar(barData, maxDataValue)
            }
        }
    }
}

@Composable
fun Bar(barData: Int, maxDataValue: Int) {
    val height = (barData.toFloat() / maxDataValue) * 300
    Box(
        modifier = Modifier
            .height(height.dp)
            .width(30.dp)
            .background(Color.Black),
        contentAlignment = Alignment.BottomCenter
    ) {
        Text(
            text = barData.toString(),
            color = Color.White
        )
    }
}
```