---
layout: post
title: Add/Remove in LazyColumn List (aka Recyclerview) Jetpack Compose
description: Add/Remove in LazyColumn List (aka Recyclerview) Jetpack Compose
summary: Add/Remove in LazyColumn List (aka Recyclerview) Jetpack Compose
tags: 
minute: 1
---
[Link](https://medium.com/geekculture/add-remove-in-lazycolumn-list-aka-recyclerview-jetpack-compose-7c4a2464fc9f)

Hey Android Devs, as you know jetpack compose is rapidly growing and companies are adapting this to design their android apps. Creating list is very important topic of jetpack compose because in every app we need to create list whether vertical or horizontal. As we know before jetpack compose we need to use recyclerview widget to create list, in recyclerview we need to setup its item xml, layout manager, adapter to show the content in the list, but in jetpack compose we don’t need to create item xml, layout manager and its separate adapter.

There are two types of built-in functions for creating list in jetpack compose

1- LazyColumn this will create vertical list

2- LazyRow this will create horizontal list

    Wait a minute if we don’t need to create adapter then how can we notify our list about data insertion or deletion or updation?

Don’t worry instead of creating simple mutable list you need to create mutableStateListOf<”DataType”>()

Now below is the code for the simple insertion and deletion from lazycolumn.

```kotlin
@Composable
fun funData() {
// this variable use to handle list state
    val notesList = remember {
        mutableStateListOf<String>()
    }
// this variable use to handle edit text input value
    val inputvalue = remember { mutableStateOf(TextFieldValue()) }

    Column {
        Row(
            Modifier
                .fillMaxWidth()
                .height(Dp(60f))
        ) {

            TextField(
                value = inputvalue.value,
                onValueChange = {
                    inputvalue.value = it
                },
                modifier = Modifier.weight(0.8f),
                placeholder = { Text(text = "Enter your note") },
                keyboardOptions = KeyboardOptions(
                    capitalization = KeyboardCapitalization.None,
                    autoCorrect = true, keyboardType = KeyboardType.Text, imeAction = ImeAction.Done
                ),
                textStyle = TextStyle(
                    color = Color.Black, fontSize = TextUnit.Unspecified,
                    fontFamily = FontFamily.SansSerif
                ),
                maxLines = 1,
                singleLine = true
            )

            Button(
                onClick = {
                    notesList.add(inputvalue.value.text)
                },
                modifier = Modifier
                    .weight(0.2f)
                    .fillMaxHeight()
            ) {
                Text(text = "ADD")
            }
        }

        Spacer(modifier = Modifier.height(Dp(1f)))

        Surface(modifier = Modifier.padding(all = Dp(5f))) {
            LazyColumn {

                itemsIndexed(notesList) { index, item ->

                    val annotatedText = buildAnnotatedString {
                        withStyle(
                            style = SpanStyle(
                                color = Color.Blue,
                                fontWeight = FontWeight.Bold
                            )
                        ) {
                            append("Delete")
                        }
                    }
                    Row(
                        Modifier
                            .fillMaxWidth()
                            .height(Dp(50f))
                    ) {

                        Text(text = item, Modifier.weight(0.85f))

                        ClickableText(
                            text = annotatedText, onClick = {

                                notesList.remove(item)

                            },
                            modifier = Modifier.weight(0.15f)
                        )
                    }
                }
            }
        }
    }
}
```