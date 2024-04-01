---
layout: post
title: Jetpack Compose - 쿠팡 메인 화면 만들기
description: Jetpack Compose - 쿠팡 메인 화면 만들기
summary: Jetpack Compose - 쿠팡 메인 화면 만들기
tags: 
minute: 1
---
MainActivity.kt
```kotlin
@Composable
fun CoupangEx() {
    Surface(
        modifier = Modifier.fillMaxSize(),
        color = MaterialTheme.colorScheme.background
    ) {
        Column {
            TopLogoArea()
            TopSearchBarArea()
            TopBanner()
            CategoryList()
            CenterBannerArea()
        }
    }
}

@Composable
fun TopLogoArea() {
    Box {
        Box(
            modifier = Modifier
                .fillMaxWidth()
                .height(60.dp),
            contentAlignment = Alignment.Center
        ) {
            Row {
                Text(text = "C", fontSize = 30.sp, color = Color(0xFF964B00))
                Text(text = "O", fontSize = 30.sp, color = Color(0xFF964B00))
                Text(text = "U", fontSize = 30.sp, color = Color(0xFF964B00))
                Text(text = "P", fontSize = 30.sp, color = Color.Red)
                Text(text = "A", fontSize = 30.sp, color = Color.Yellow)
                Text(text = "N", fontSize = 30.sp, color = Color.Green)
                Text(text = "G", fontSize = 30.sp, color = Color.Blue)
            }
            Icon(
                imageVector = Icons.Default.ShoppingCart,
                contentDescription = null,
                modifier = Modifier
                    .align(Alignment.CenterEnd)
                    .padding(end = 20.dp)
            )
        }
    }
}

@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TopSearchBarArea() {
    var inputText by remember {
        mutableStateOf("")
    }
    Box(
        modifier = Modifier
            .fillMaxWidth()
            .padding(start = 20.dp, end = 20.dp)
            .border(1.dp, Color.Gray, shape = RoundedCornerShape(10.dp))
    ) {
        TextField(
            value = inputText,
            onValueChange = {
                inputText = it
            },
            leadingIcon = { Icon(imageVector = Icons.Default.Search, contentDescription = null)},
            placeholder = { Text(text = "Search on Coupang")},
            modifier = Modifier.fillMaxWidth(),
            colors = TextFieldDefaults.textFieldColors(
                containerColor = Color.White,
                focusedIndicatorColor = Color.Transparent,
                unfocusedIndicatorColor = Color.Transparent
            )
        )
    }
}

@OptIn(ExperimentalPagerApi::class)
@Composable
fun TopBanner() {
    val pageState = rememberPagerState()
    val pageCount = 5
    val textList = listOf(
        "Advertising Phrases1",
        "Advertising Phrases2",
        "Advertising Phrases3",
        "Advertising Phrases4",
        "Advertising Phrases5"
    )
    Box(
        modifier = Modifier.padding(top = 20.dp)
    ) {
        HorizontalPager(
            count = pageCount,
            state = pageState,
            modifier = Modifier
                .fillMaxWidth()
                .height(200.dp)
                .background(Color.Gray)
        ) {page->
            Text(
                text = textList[page],
                fontSize = 30.sp,
                fontWeight = FontWeight.ExtraBold
            )
        }
        HorizontalPagerIndicator(
            pagerState = pageState,
            modifier = Modifier
                .align(Alignment.BottomCenter)
                .padding(15.dp)
        )
    }
}

@Composable
fun CategoryList() {
    val scrollState = rememberScrollState()
    Row(
        modifier = Modifier
            .horizontalScroll(scrollState)
            .padding(10.dp)
    ) {
        val itemList = listOf(
            "Item1",
            "Item2",
            "Item3",
            "Item4",
            "Item5"
        )
        val iconList = listOf(
            Icons.Default.Favorite,
            Icons.Default.ArrowBack,
            Icons.Default.ShoppingCart,
            Icons.Default.List,
            Icons.Default.Phone
        )
        itemList.forEachIndexed { index, item ->
            Column(
                modifier = Modifier
                    .padding(end = 20.dp)
                    .width((LocalConfiguration.current.screenWidthDp.dp - 60.dp) / 3),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                Icon(
                    imageVector = iconList[index % iconList.size],
                    contentDescription = null
                )
                Text(text = item)
                Spacer(modifier = Modifier.padding(20.dp))
                Icon(
                    imageVector = iconList[index % iconList.size],
                    contentDescription = null
                )
                Text(text = item)
            }
        }
    }
}

@Composable
fun CenterBannerArea() {
    Box(
        modifier = Modifier
            .fillMaxWidth()
            .height(500.dp)
            .padding(20.dp)
            .background(Color.LightGray),
        contentAlignment = Alignment.Center
    ) {
        Text(
            text = "Banner Area",
            fontSize = 30.sp,
            fontWeight = FontWeight.ExtraBold
        )
    }
}
```