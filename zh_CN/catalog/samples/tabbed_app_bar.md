---
layout: page
title: "TabBar 式的应用栏"
permalink: /catalog/samples/tabbed-app-bar/
---

以 TabBar 作为其底部 widget 的应用栏。

<p>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-4">
        <div class="panel panel-default">
          <div class="panel-body" style="padding: 16px 32px;">
            <img style="border:1px solid #000000" src="https://storage.googleapis.com/flutter-catalog/cb4a54db8fb3726bf4293b9cc5cb12ce16883803/tabbed_app_bar_small.png" alt="Android screenshot" class="img-responsive">
          </div>
          <div class="panel-footer">
            Android 截图
          </div>
        </div>
      </div>
    </div>
  </div>
</p>

TabBar 可用于 TabBarView 展示的页面之间的导航。尽管 TabBar 是个能出现在任何地方的普通 widget，但它通常包含在应用程序的 AppBar 中。

使用 `flutter create` 来创建一个新项目，并用下面的代码替换 `lib/main.dart` 的内容来尝试运行。


```dart
// Copyright 2017 The Chromium Authors. All rights reserved.
// Use of this source code is governed by a BSD-style license that can be
// found in the LICENSE file.

import 'package:flutter/material.dart';

class TabbedAppBarSample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: new DefaultTabController(
        length: choices.length,
        child: new Scaffold(
          appBar: new AppBar(
            title: const Text('Tabbed AppBar'),
            bottom: new TabBar(
              isScrollable: true,
              tabs: choices.map((Choice choice) {
                return new Tab(
                  text: choice.title,
                  icon: new Icon(choice.icon),
                );
              }).toList(),
            ),
          ),
          body: new TabBarView(
            children: choices.map((Choice choice) {
              return new Padding(
                padding: const EdgeInsets.all(16.0),
                child: new ChoiceCard(choice: choice),
              );
            }).toList(),
          ),
        ),
      ),
    );
  }
}

class Choice {
  const Choice({ this.title, this.icon });
  final String title;
  final IconData icon;
}

const List<Choice> choices = const <Choice>[
  const Choice(title: 'CAR', icon: Icons.directions_car),
  const Choice(title: 'BICYCLE', icon: Icons.directions_bike),
  const Choice(title: 'BOAT', icon: Icons.directions_boat),
  const Choice(title: 'BUS', icon: Icons.directions_bus),
  const Choice(title: 'TRAIN', icon: Icons.directions_railway),
  const Choice(title: 'WALK', icon: Icons.directions_walk),
];

class ChoiceCard extends StatelessWidget {
  const ChoiceCard({ Key key, this.choice }) : super(key: key);

  final Choice choice;

  @override
  Widget build(BuildContext context) {
    final TextStyle textStyle = Theme.of(context).textTheme.display1;
    return new Card(
      color: Colors.white,
      child: new Center(
        child: new Column(
          mainAxisSize: MainAxisSize.min,
          crossAxisAlignment: CrossAxisAlignment.center,
          children: <Widget>[
            new Icon(choice.icon, size: 128.0, color: textStyle.color),
            new Text(choice.title, style: textStyle),
          ],
        ),
      ),
    );
  }
}

void main() {
  runApp(new TabbedAppBarSample());
}
```

<h2>另请参阅：</h2>
- Material Design 规范中的 “Components-Tabs” 部分：
    <https://material.io/guidelines/components/tabs.html>
- 源码 [examples/catalog/lib/tabbed_app_bar.dart](https://github.com/flutter/flutter/blob/master/examples/catalog/lib/tabbed_app_bar.dart).
