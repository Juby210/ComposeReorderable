# Compose LazyList reorder
[![](https://jitpack.io/v/aclassen/ComposeReorderable.svg)](https://jitpack.io/#aclassen/ComposeReorderable)

A Jetpack Compose modifier enabling reordering in a LazyList.

![Sample](readme/sample.gif)

## Download

```
repositories {
    maven { setUrl("https://jitpack.io") }
    // maven { url 'https://jitpack.io' } 
}


dependencies {
    implementation("com.github.aclassen:ComposeReorderable:<latest_version>")
}
```


## How to use

Create your LazyColumn or LazyRow:

```
val state: ReorderableState = rememberReorderState { from, to -> data.move(from, to) }
LazyColumn(
    state = state.listState,
    modifier = Modifier.reorderable(state, items))
```

Apply the offset to your item layout :

```
itemsIndexed(items) { idx, item ->
    Column(
        modifier = Modifier.draggedItem(state.offset.takeIf { state.index == idx })
    ) {
        ...
    }
}
```
Use `draggedItem` for a default dragged effect or create your own.

## Notes

**Don`t use keyed items cause in this case the LazyList will [keep the scroll position based on the key](https://developer.android.com/reference/kotlin/androidx/compose/foundation/lazy/package-summary#(androidx.compose.foundation.lazy.LazyListScope).items(kotlin.collections.List,kotlin.Function1,kotlin.Function2))**

When dragging, the existing item will be modified.
Because if this reason it`s important that the item must be part of the LazyList visible items all the time.

This can be problematic if no drop target can be found during scrolling.

## License

```
Copyright 2021 André Claßen

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
