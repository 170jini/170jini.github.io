---
layout: post
title: Jetpack Compose - 달력 앱 2
description: Jetpack Compose - 달력 앱 2
summary: Jetpack Compose - 달력 앱 2
tags: 
minute: 1
---
SettingsGradle.kts
```xml
repositories {
    maven("https://jitpack.io")
}
```
BuildGradle.kts
```xml
implementation("com.github.Gurupreet:FontAwesomeCompose:1.0.0")
```
MainActivity.kt
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .background(Color.White)
                ) {
                    CalendarHeader()
                    CalendarLazyList()
                }
            }
        }
    }
}

@Composable
fun CalendarHeader() {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(top = 20.dp, bottom = 20.dp),
        horizontalArrangement = Arrangement.End
    ) {
        FaIcon(
            faIcon = FaIcons.Cog,
            size = 30.dp,
            tint = Color.Gray,
            modifier = Modifier.padding(end = 10.dp)
        )
        FaIcon(
            faIcon = FaIcons.Bell,
            size = 30.dp,
            tint = Color.Gray,
            modifier = Modifier.padding(end = 10.dp)
        )
        FaIcon(
            faIcon = FaIcons.Bars,
            size = 30.dp,
            tint = Color.Gray,
            modifier = Modifier.padding(end = 10.dp)
        )
    }
}

@Composable
fun CalendarDayName() {
    val nameList = listOf("일", "월", "화", "수", "목", "금", "토")
    Row {
        nameList.forEach {
            Box(
                modifier = Modifier
                    .weight(1f),
                contentAlignment = Alignment.Center
            ) {
                Text(
                    text = it,
                    fontSize = 14.sp
                )
            }
        }
    }
}

@Composable
fun CalendarDayList() {
    val time = remember { mutableStateOf(Calendar.getInstance()) }
    val date = time.value
    date.set(Calendar.YEAR, 2023)
    date.set(Calendar.MONTH, Calendar.DECEMBER)
    date.set(Calendar.DAY_OF_MONTH, 1)
    val thisMonthDayMax = date.getActualMaximum(Calendar.DAY_OF_MONTH)
    val thisMonthFirstDay = date.get(Calendar.DAY_OF_WEEK) - 1
    val thisMonthWeeksCount = (thisMonthDayMax + thisMonthFirstDay + 6) / 7
    Column {
        repeat(thisMonthWeeksCount) {week ->
            Row {
                repeat(7) {day ->
                    val resultDay = week * 7 + day - thisMonthFirstDay + 1
                    if (resultDay in 1..thisMonthDayMax) {
                        Box(
                            modifier = Modifier
                                .weight(1f)
                                .height(60.dp)
                                .border(1.dp, Color.Gray),
                            contentAlignment = Alignment.Center
                        ) {
                            Column(
                                modifier = Modifier
                                    .fillMaxSize(),
                                verticalArrangement = Arrangement.Top
                            ) {
                                Box(
                                    modifier = Modifier
                                        .fillMaxWidth()
                                        .height(20.dp)
                                        .background(Color(0xFF89CFF0))
                                )
                                Box(
                                    modifier = Modifier
                                        .fillMaxSize(),
                                    contentAlignment = Alignment.Center
                                ) {
                                    Text(
                                        text = resultDay.toString(),
                                        fontSize = 14.sp
                                    )
                                }
                            }
                        }
                    }
                    else
                    {
                        Box(
                            modifier = Modifier
                                .weight(1f)
                                .height(60.dp)
                                .border(1.dp, Color.Gray),
                            contentAlignment = Alignment.Center
                        ) {
                            Column(
                                modifier = Modifier
                                    .fillMaxSize(),
                                verticalArrangement = Arrangement.Top
                            ) {
                                Box(
                                    modifier = Modifier
                                        .fillMaxWidth()
                                        .height(20.dp)
                                        .background(Color(0xFF89CFF0))
                                )
                            }
                        }
                    }
                }
            }
        }
    }
}

@Composable
fun CalendarLazyList() {
    val lazyColumnState = rememberLazyListState()
    val lazyRowState = rememberLazyListState()
    val isScrolling = remember { mutableStateOf(false) }
    LaunchedEffect(Unit) {
        snapshotFlow { lazyColumnState.isScrollInProgress }.collect{
            isScrolling.value = it
        }
    }
    LaunchedEffect(lazyColumnState.firstVisibleItemIndex) {
        lazyRowState.scrollToItem(lazyColumnState.firstVisibleItemIndex)
    }
    if (isScrolling.value)
    {
        LazyRow(
            modifier = Modifier
                .fillMaxWidth()
                .height(60.dp),
            state = lazyRowState
        ) {
            items(spendingData.size) {
                val day = it + 1
                Box(
                    modifier = Modifier
                        .width(55.dp)
                        .height(60.dp)
                        .border(1.dp, Color.Gray),
                    contentAlignment = Alignment.Center
                ) {
                    Column(
                        modifier = Modifier
                            .fillMaxSize(),
                        verticalArrangement = Arrangement.Top
                    ) {
                        Box(
                            modifier = Modifier
                                .fillMaxWidth()
                                .height(20.dp)
                                .background(Color(0xFF89CFF0))
                        ) {
                            val income = spendingData[day]?.get(0)?.price ?: 0
                            val outcome = spendingData[day]?.get(1)?.price ?: 0
                            val result = income - outcome
                            if (result < 0)
                            {
                                Text(
                                    text = result.toString(),
                                    color = Color.Red,
                                    modifier = Modifier.align(Alignment.Center)
                                )
                            }
                            else
                            {
                                Text(
                                    text = result.toString(),
                                    color = Color.Blue,
                                    modifier = Modifier.align(Alignment.Center)
                                )
                            }
                        }
                        Box(
                            modifier = Modifier
                                .fillMaxSize(),
                            contentAlignment = Alignment.Center
                        ) {
                            Text(
                                text = day.toString(),
                                fontSize = 14.sp
                            )
                        }
                    }
                }
            }
        }
    }
    else
    {
        CalendarDayName()
        CalendarDayList()
    }
    LazyColumn(
        modifier = Modifier
            .fillMaxWidth()
            .padding(20.dp),
        state = lazyColumnState
    ) {
        spendingData.keys.forEach{day ->
            item {
                Text(
                    text = "2023년 12월 ${day}일",
                    fontSize = 15.sp,
                    fontWeight = FontWeight.Bold,
                    modifier = Modifier.padding(top = 10.dp, bottom = 10.dp)
                )
                spendingData[day]?.forEach{data ->
                    Row(
                        modifier = Modifier.padding(start = 5.dp, top = 3.dp)
                    ) {
                        Text(text = data.type, fontSize = 12.sp)
                        Text(
                            text = "${data.price}원",
                            fontSize = 12.sp,
                            color = if (data.type == "수입") Color.Red else Color.Blue,
                            modifier = Modifier.padding(start = 10.dp)
                        )
                    }
                }
            }
        }
    }
}
```
CalendarData.kt
```kotlin
object CalendarData {
    val spendingData = (1..31).associateWith {
        listOf(
            IncomeOutcomeModel("수입", ((1000..5000).random())),
            IncomeOutcomeModel("지출", ((1000..5000).random()))
        )
    }
}
```
IncomeOutcomeModel.kt
```kotlin
data class IncomeOutcomeModel(
    val type: String,
    val price: Int
)
```