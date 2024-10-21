---
layout: post
title: Jetpack Compose - Drawer
description: Jetpack Compose - Drawer
summary: Jetpack Compose - Drawer
tags: 
minute: 1
---
```kotlin
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MyDrawer() {
    val drawerState = rememberDrawerState(initialValue = DrawerValue.Closed)
    val scope = rememberCoroutineScope()
    val screens = listOf(
        Screen.Home,
        Screen.Settings,
        Screen.Phone,
        Screen.Search,
        Screen.Lock
    )
    val selectedScreen : MutableState<Screen> = remember {
        mutableStateOf(Screen.Home)
    }
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text(text = "MyDrawer") },
                navigationIcon = {
                    IconButton(onClick = { scope.launch { drawerState.open() } }) {
                        Icon(imageVector = Icons.Default.Menu, contentDescription = "Menu")
                    }
                }
            )
        }
    ) {paddingValues ->
        ModalNavigationDrawer(
            drawerState = drawerState,
            modifier = Modifier.padding(paddingValues),
            drawerContent = {
                ModalDrawerSheet {
                    screens.forEach {screen ->
                        NavigationDrawerItem(
                            icon = { Icon(screen.icon, contentDescription = screen.icon.name)},
                            label = { Text(text = screen.name) },
                            selected = screen == selectedScreen.value,
                            onClick = {
                                scope.launch { drawerState.close() }
                                selectedScreen.value = screen
                            }
                        )
                    }
                }
            },
            content = {
                Column(
                    modifier = Modifier
                        .fillMaxSize()
                        .padding(20.dp),
                    horizontalAlignment = Alignment.CenterHorizontally,
                    verticalArrangement = Arrangement.Center
                ) {
                    when(selectedScreen.value) {
                        Screen.Home -> HomeScreen()
                        Screen.Settings -> SettingsScreen()
                        Screen.Phone -> PhoneScreen()
                        Screen.Search -> SearchScreen()
                        Screen.Lock -> LockScreen()
                    }
                }
            }
        )
    }
}

@Composable
fun HomeScreen() {
    Text(text = "HomeScreen")
}

@Composable
fun SettingsScreen() {
    Text(text = "SettingsScreen")
}

@Composable
fun PhoneScreen() {
    Text(text = "PhoneScreen")
}

@Composable
fun SearchScreen() {
    Text(text = "SearchScreen")
}

@Composable
fun LockScreen() {
    Text(text = "LockScreen")
}

sealed class Screen(val name : String, val icon : ImageVector) {
    object Home : Screen("Home", Icons.Default.Home)
    object Settings : Screen("Settings", Icons.Default.Settings)
    object Phone : Screen("Phone", Icons.Default.Phone)
    object Search : Screen("Search", Icons.Default.Search)
    object Lock : Screen("Lock", Icons.Default.Lock)
}

@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    MyApplicationTheme {
        MyDrawer()
    }
}
```