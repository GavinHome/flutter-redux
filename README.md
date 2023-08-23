<!--
This README describes the package. If you publish this package to pub.dev,
this README's contents appear on the landing page for your package.

For information about how to write a good package README, see the guide for
[writing package pages](https://dart.dev/guides/libraries/writing-package-pages).

For general information about developing packages, see the Dart guide for
[creating packages](https://dart.dev/guides/libraries/create-library-packages)
and the Flutter guide for
[developing packages and plugins](https://flutter.dev/developing-packages).
-->

<p align="center"><img src="./logo.jpeg" width="280" alt="flying-redux"></p>
<!-- <h1>Flying Redux</h1> -->

[![pub package](https://img.shields.io/pub/v/flying_redux.svg?label=flying_redux&color=blue)](https://pub.dev/packages/flying_redux)
[![build](https://github.com/GavinHome/flying-redux/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/GavinHome/flying-redux/actions/workflows/build.yml) [![codecov](https://codecov.io/gh/gavinhome/flying-redux/branch/master/graph/badge.svg)](https://codecov.io/gh/gvinhome/flying-redux)
[![size](https://img.shields.io/badge/size-35KB-blue)](https://github.com/GavinHome/flying-redux/tree/master/lib)
[![code](https://img.shields.io/badge/lines%20of%20code-1278-blue)](https://github.com/GavinHome/flying-redux/tree/master/lib)



## What is Flying Redux?

Flying Redux is also an assembled flutter application framework based on Redux state management.

<p><img src="./flying-redux.png" alt="flying-redux-framework"></p>

## Features

It has four characteristics:

> 1. Functional Programming
> 2. Predictable state container
> 3. Pluggable componentization
> 4. Support null safety and flutter 3.x

## Getting started

There are five steps to use the counter as an example:

> 1. Import flying_redux package
> 2. Create State and InitState
> 3. Define Action and ActionCreator
> 4. Create Reducer that modifies state
> 5. Create Page or Component

```dart
import 'package:flying_redux/flying_redux.dart';

/// [State]
class PageState extends Cloneable<PageState> {
  late int count;

  @override
  PageState clone() {
    return PageState()..count = count;
  }
}

/// [InitState]
PageState initState(Map<String, dynamic>? args) {
  //just do nothing here...
  return PageState()..count = 0;
}

/// [Action]
enum CounterAction { increment }

/// [ActionCreator]
class CounterActionCreator {
  static Action increment() {
    return const Action(CounterAction.increment, payload: 1);
  }
}

/// [Reducer]
buildReducer() {
  return asReducer(<Object, Reducer<PageState>>{
    CounterAction.increment: _increment,
  });
}

PageState _increment(PageState state, Action action) {
  final int num = action.payload;
  return state.clone()..count = (state.count + num);
}

/// [Page]
class CountPage extends Page<PageState, Map<String, dynamic>> {
  CountPage()
      : super(
            initState: initState,
            reducer: buildReducer(),
            view: (PageState state, Dispatch dispatch, ComponentContext<PageState> ctx) {
              return Scaffold(
                body: Center(
                  child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                      const Text(
                        'You have pushed the button this many times:',
                      ),
                      Text(state.count.toString()),
                    ],
                  ),
                ),
                floatingActionButton: FloatingActionButton(
                  onPressed: () => dispatch(CounterActionCreator.increment()),
                  tooltip: 'Increment',
                  child: const Icon(Icons.add),
                ), // This trailing comma makes auto-formatting nicer for build methods.
              );
            });
}
```

## Usage

If you want to know specific usage examples, please refer to the todo list code in the example project and in the `/example` folder.

-   [todo list](example) - a simple todo list demo.
-   run it:

``` dart
cd ./example
flutter run
```

## Code Template

- [Flying Redux Template For VSCode](https://github.com/GavinHome/flying-redux-template-for-vscode).
- [Flying Redux Template For AndroidStudio](https://github.com/GavinHome/flying-redux-template-for-as).

## Additional information

In particular, the code of flying-redux has the same naming and implementation as fish-redux.
Because [fish-redux](https://github.com/alibaba/fish-redux) has not been updated for a long time. 
I have done a lot of refactoring and modification based on fish_redux, and simplified some concepts,
and finally renamed it.
If you have any questions, please scan the qq QR code below to enter the group communication.

<p><img src="./qq.jpg" width="360" alt="qq"></p>
