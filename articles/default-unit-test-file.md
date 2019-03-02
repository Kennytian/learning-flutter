解读全在代码的注释里，请慢用 🤣

```
import 'package:flutter/material.dart';
import 'package:flutter_test/flutter_test.dart';

import 'package:flutter_app4/main.dart';

void main() {
  testWidgets('Counter increments smoke test', (WidgetTester tester) async {
    // 加载 MyApp 类
    await tester.pumpWidget(MyApp());

    // findsOneWidget 表示找到一个文字为「0」的 Widget
    expect(find.text('0'), findsOneWidget);

    // findsOneWidget 表示没有文字为「1」找到 Widget
    expect(find.text('1'), findsNothing);

    // 模拟按了一下「+」号图片
    await tester.tap(find.byIcon(Icons.add));

    IconData icon = Icons.add; // 图片返回的是 IconData 类型
    Finder addIcon = find.byIcon(icon); // find.xxx 返回的是 Finder 类型
    await tester.tap(addIcon); // 再模拟按了一下「+」号图片

    // tester 「抽身逃走」
    await tester.pump();

    // tester 已经「跑路」了，所以 tap 不会执行，但也不会报错
    await tester.tap(find.byIcon(Icons.add));

    // findsOneWidget 表示没有文字为「0」找到 Widget
    expect(find.text('0'), findsNothing);
    // findsOneWidget 表示找到一个文字为「2」的 Widget
    expect(find.text('2'), findsOneWidget);
  });
}

```
