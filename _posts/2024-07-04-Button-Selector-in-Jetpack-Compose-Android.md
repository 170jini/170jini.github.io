---
layout: post
title: "Button Selector in Jetpack Compose Android"
description: "Button Selector in Jetpack Compose Android"
summary: "Button Selector in Jetpack Compose Android"
tags: 
minute: 1
---
[Reference](https://chetan-garg36.medium.com/stop-using-the-wrong-loop-from-for-to-oneach-ultimate-guide-to-kotlin-loops-42dd25d6f3b3)    

As we know button is basic view component of android. We use button on almost every screen of our app. But sometimes we can to customize android button to meet our app UI/UX. We can easily change button background and even change button background color when user pressed it by creating a drawable and setting that drawable in Xml tag of button. But as we know Jetpack compose is alternative of Xml so we need to apply shape or change button background color using Composable Function.    

In this tutorial i am going to show you how you can change button background color when user pressed it using composable function in jetpack compose. To use jetpack compose you need to use android studio arctic fox with orange icon, because jetpack compose is not currently supported by android studio blue icon which we mostly use for developing android apps.    
Jetpack compose is built on kotlin language so i am assuming you are familiar with kotlin language.    

__*First we need to create a new project*__    
You need to select Empty Compose Activity so that android studio will take care of important libraries and some important functions which are necessary for jetpack compose app.    
Then after finishing creating your project, you will be able to see activity class with some pre written Composable function in its onCreate function, in your case BottomNavigationTheme will changed with your project name and theme is postfix text. Surface is a container in which you can define composable function to display your app content.    
```kotlin
setContent {
    BottomNavigationTheme {
        // A surface container using the 'background' color from the theme
        Surface(color = MaterialTheme.colors.background) {
            Greeting()
        }
    }
}
```
Below is Greeting function which is pre written by android studio i just modify it so that i can show you how you can change button background color when user pressed it. This function should be annotated by @Composable so that it can be callable in Surface body which is written above.    

You need to declare variable with remeber { MutableInteractionSource()} so that your app can remeber button current state.
After that i have created a isPressed variable so that i can know about button state if its pressed or not.
I have created another variable so that i can set its value based on isPressed true or false.    

Column act as Linear Layout in Jetpack compose thats why i have created it with some modifiers. Modifier is use on views to set different kind of attributes like its height,width,padding etc, like we declare attributes in Xml tag of views. Inside Column i have created Button with some modifiers and its text.    
```kotlin
@Composable
fun Greeting() {

    val interactionSource = remember { MutableInteractionSource() }
    val isPressed by interactionSource.collectIsPressedAsState()
    val color = if (isPressed) Color.Blue else Color.Green

    Column(modifier = Modifier.fillMaxHeight()
        .fillMaxWidth()
        .background(Color.White)
        .padding(20.dp),
        verticalArrangement= Arrangement.Center) {
        Button(
            onClick = {},
            interactionSource = interactionSource,
            colors= ButtonDefaults.buttonColors(backgroundColor = color),
            modifier = Modifier.fillMaxWidth()
                .height(50.dp)
        ){
            Text(
                "Button",
                color=Color.White
            )
        }
}
```