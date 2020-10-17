# flutter_flavor

[![pub package](https://img.shields.io/pub/v/flavor.svg)](https://pub.dartlang.org/packages/flutter_flavor)
[![Star on GitHub](https://img.shields.io/github/stars/lrferreiro/flutter_flavor.svg?style=flat&logo=github&colorB=deeppink&label=stars)](https://github.com/lrferreiro/flutter_flavor)
[![License: MIT](https://img.shields.io/badge/license-MIT-purple.svg)](https://opensource.org/licenses/MIT)

flutter_favor allows you to quickly configure and define dynamic variables for each flavor in your project. The `flavors`, as well as their names; they are dynamically defined by the developer or development team. In the configuration of a flavor you can set the `name` of each flavor, as well as the `color` and `location` of its banner. When attribute `name` is  undefined or empty, the banner is hidden.

## Screenshot

|              PROD               |              DEV               |              TEST               |
| :-----------------------------: | :----------------------------: | :-----------------------------: |
| ![](screenshot/flavor_prod.png) | ![](screenshot/flavor_dev.png) | ![](screenshot/flavor_test.png) |

**Note** By default the banner is shown in `BannerLocation.topStart` and is visibility only when the attribute `name` of configuration is defined and not empty.

## Getting Started

### Adding package

```yaml
flutter_flavor: ^1.1.0
```

### Importing package

```yaml
import 'package:flutter_flavor/flutter_flavor.dart';
```

### Configuring

```dart
FlavorConfig(
    name: "DEVELOP",
    color: Colors.red,
    location: BannerLocation.bottomStart,
    variables: {
        "counter": 0,
        "baseUrl": "https://www.example.com",
    }
);
```

### Using variables

```dart
 int _counter = FlavorConfig.instance.variables["counter"];
```

## Example

```dart
import 'package:flutter/material.dart';

import 'package:flutter_flavor/flutter_flavor.dart';

void main() {
    FlavorConfig(
            name: "DEVELOP",
            color: Colors.red,
            location: BannerLocation.bottomStart,
            variables: {
                "counter": 5,
                "baseUrl": "https://www.example.com",
            });
    return runApp(MyApp());
}

class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return FlavorBanner(
            child: MaterialApp(
                title: 'Flutter Demo',
                theme: ThemeData(
                    primarySwatch: Colors.blue,
                ),
                home: MyHomePage(title: 'Flutter Demo Home Page'),
            ),
        );
    }
}

class MyHomePage extends StatefulWidget {
    MyHomePage({Key key, this.title}) : super(key: key);

    final String title;

    @override
    _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
    int _counter = FlavorConfig.instance.variables["counter"];

    void _incrementCounter() {
        setState(() {
            _counter++;
        });
    }

    @override
    Widget build(BuildContext context) {
        return Scaffold(
            appBar: AppBar(
                title: Text(widget.title),
            ),
            body: Center(
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: <Widget>[
                        Text(
                            'You have pushed the button this many times:',
                        ),
                        Text(
                            '$_counter',
                            style: Theme
                                    .of(context)
                                    .textTheme
                                    .display1,
                        ),
                    ],
                ),
            ),
            floatingActionButton: FloatingActionButton(
                onPressed: _incrementCounter,
                tooltip: 'Increment',
                child: Icon(Icons.add),
            ),
        );
    }
}
```

## VSCode Configuration

The .vscode folder is created in the workspace, if it does not exist it can be created by hand. Inside that folder a launch.json file is created and the configuration is established inside the file. For more information, visit: https://code.visualstudio.com/docs/editor/debugging and https://go.microsoft.com/fwlink/?linkid=830387

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "PROD-Flavor",
      "program": "[project-folder]/lib/main_prod.dart",
      "request": "launch",
      "type": "dart"
    },
    {
      "name": "DEV-Flavor",
      "program": "[project-folder]/lib/main_dev.dart",
      "request": "launch",
      "type": "dart"
    }
  ]
}
```

## License

    MIT License
