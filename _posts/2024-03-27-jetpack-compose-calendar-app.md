---
layout: post
title: Jetpack Compose - 달력 앱 1
description: Jetpack Compose - 달력 앱 1
summary: Jetpack Compose - 달력 앱 1
tags: 
minute: 1
---
MainActivity.kt
```kotlin
@Composable
private fun CalendarApp() {
    var calendarInstance = Calendar.getInstance()
    val time = remember {
        mutableStateOf(calendarInstance)
    }
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(20.dp),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        CalendarHeader(time)
        CalendarHeaderBtn(time)
        CalendarDayName()
        CalendarDayList(time)
    }
}

@Composable
fun CalendarHeaderBtn(date: MutableState<Calendar>) {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(top = 30.dp, bottom = 30.dp),
        horizontalArrangement = Arrangement.SpaceBetween
    ) {
        Button(
            onClick = {
                val newDate = Calendar.getInstance()
                newDate.time = date.value.time
                newDate.add(Calendar.MONTH, -1)
                date.value = newDate
            },
            colors = ButtonDefaults.buttonColors(
                containerColor = Color.Black
            )
        ) {
            Text(
                text = "<",
                color = Color.Green
            )
        }
        Button(
            onClick = {
                val newDate = Calendar.getInstance()
                newDate.time = date.value.time
                newDate.add(Calendar.MONTH, +1)
                date.value = newDate
            },
            colors = ButtonDefaults.buttonColors(
                containerColor = Color.Black
            )
        ) {
            Text(
                text = ">",
                color = Color.Green
            )
        }
    }
}

@Composable
fun CalendarHeader(date: MutableState<Calendar>) {
    val resultTime = SimpleDateFormat("yyyy. MM.", Locale.KOREA).format(date.value.time)
    Text(
        text = resultTime,
        fontSize = 30.sp
    )
}

@Composable
fun CalendarDayName() {
    val nameList = listOf("Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat")
    Row {
        nameList.forEach {
            Box(
                modifier = Modifier.weight(1f),
                contentAlignment = Alignment.Center
            ) {
                Text(
                    text = it,
                    fontSize = 18.sp,
                    fontWeight = FontWeight.ExtraBold
                )
            }
        }
    }
}

@Composable
fun CalendarDayList(date: MutableState<Calendar>) {
    date.value.set(Calendar.DAY_OF_MONTH, 1)
    val monthDayMax = date.value.getActualMaximum(Calendar.DAY_OF_MONTH)
    val monthFirstDay = date.value.get(Calendar.DAY_OF_WEEK) - 1
    val monthWeeksCount = (monthDayMax + monthFirstDay + 6) / 7
    Log.d("monthDayMax", monthDayMax.toString())
    Log.d("monthFirstDay", monthFirstDay.toString())
    Log.d("monthWeeksCount", monthWeeksCount.toString())
    Column {
        repeat(monthWeeksCount) {week->
            Row {
                repeat(7) {day->
                    val resultDay = week * 7 + day - monthFirstDay + 1
                    if (resultDay in 1 .. monthDayMax) {
                        Box(
                            modifier = Modifier
                                .weight(1f)
                                .padding(10.dp),
                            contentAlignment = Alignment.Center
                        ) {
                            Text(
                                text = resultDay.toString(),
                                fontSize = 25.sp
                            )
                        }
                    } else {
                        Spacer(modifier = Modifier.weight(1f))
                    }
                }
            }
        }
    }
}
```