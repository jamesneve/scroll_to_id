# Scroll to id

scroll_to_id is a Flutter library for Scroll to id in ScrollView

![Image](https://raw.githubusercontent.com/wiki/yusukeinouehatchout/scroll_to_id/gif/scroll_to_id_test.gif)

## Features

* Select scroll direction

## Installing

You should add the following to your `pubspec.yaml` file:

```yaml
dependencies:
  scroll_to_id: ^1.1.0
```

## Getting Started

To start, import the dependency in your code:

```dart
import 'package:scroll_to_id/scroll_to_id.dart';
```

Next, to create instance:
```dart
final ScrollToId scrollToId = ScrollToId();
```

Next, to set InteractiveScrollViewer and ScrollContent:

```dart
InteractiveScrollViewer(
  scrollToId: scrollToId,
  children: <ScrollContent>[
    ScrollContent(
      id: 'a',
      child: Container(
        color: Colors.red,
        width: 300,
        height: 200,
      )
    ),
    ScrollContent(
      id: 'b',
      child: Container(
        color: Colors.green,
        width: 300,
        height: 200,
      )
    ),
  ],
)
```

id property is destination of scroll.

Next, to scroll to id:

```dart
/// animate
scrollToId.animateTo(
  'b',
  duration: Duration(milliseconds: 500),
  curve: Curves.ease
);

/// jump
scrollToId.jumpTo('b');
```

## Examples

```dart
import 'package:flutter/material.dart';
import 'package:scroll_to_id/scroll_to_id.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final ScrollToId scrollToId = ScrollToId();

  List<Color> _colorList = [
    Colors.green,
    Colors.red,
    Colors.yellow,
    Colors.blue
  ];

  /// Generate 10 Container
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Scroll to id',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Scroll to id'),
        ),
        body: Stack(
          alignment: Alignment.topRight,
          children: [
            InteractiveScrollViewer(
              scrollToId: scrollToId,
              children: List.generate(10, (index) {
                return ScrollContent(
                  id: '$index',
                  child: Container(
                    alignment: Alignment.center,
                    width: double.infinity,
                    height: 200,
                    child: Text(
                      '$index',
                      style: TextStyle(color: Colors.white, fontSize: 50),
                    ),
                    color: _colorList[index % _colorList.length],
                  ),
                );
              }),
            ),
            Container(
              decoration: BoxDecoration(
                border: Border.all(color: Colors.white, width: 3),
              ),
              child: Column(
                mainAxisSize: MainAxisSize.min,
                children: List.generate(10, (index) {
                  return GestureDetector(
                    child: Container(
                      width: 100,
                      alignment: Alignment.center,
                      height: 50,
                      child: Text(
                        '$index',
                        style: TextStyle(color: Colors.white),
                      ),
                      color: _colorList[index % _colorList.length],
                    ),
                    onTap: () {
                      /// scroll with animation
                      scrollToId.animateTo('$index',
                          duration: Duration(milliseconds: 500),
                          curve: Curves.ease);

                      /// scroll with jump
                      // scrollToId.jumpTp('$index');
                    },
                  );
                }),
              ),
            )
          ],
        ),
      ),
    );
  }
}
```






