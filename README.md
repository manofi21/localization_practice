# Flutter_Project: Localization

Practicing how to use localization in a project.

## 1. Getting Started (Using CodeTour)

a. Download Codetour in VS Code.  
![2022-05-14_12h25_41](https://user-images.githubusercontent.com/54527045/168412169-209c4392-04df-401e-af37-1382be7e32e9.png)

b. open CodeTour in explorer  
![2022-05-14_12h33_39](https://user-images.githubusercontent.com/54527045/168412218-aa5b836b-a4ba-4fcb-95c5-6929066a010a.png)

c. Click "Open Tour File"

## Setup Localization

a. in file pubspec.yaml, flutter_localizations and add generate
```yaml

dependencies:
  flutter:
    sdk: flutter

  flutter_localizations: # Add this line
    sdk: flutter         # Add this line

  # Add generator to Flutter Localization.
  generate: true         # Add this line

```

b. add new yaml file in project name `l10n.yaml`, and fill the file like code below:

```yaml
arb-dir: assets/l10n #required 
template-arb-file: app_en.arb #required 
output-localization-file: app_localizations.dart #required 
untranslated-messages-file: untranslated_file.txt # optional line 
```

c. crete assets folder. Inside this folder, add file name `app_en.arb` and `app_id.arb` inside folder l10n.

![2022-05-14_18h22_07](https://user-images.githubusercontent.com/54527045/168423562-e397020e-b42d-410d-8d95-dc6088e64a4a.png)

> **Note** : This file create following configuration which been create in file `l10n.yaml`
>
>`arb-dir` : for set file's of localization  
`template-arb-file` : template name of file localization  
`output-localization-file` : generated code for wording localization after debug apps
`untranslated-messages-file` : file for untransalated wording


For more information about `l10n.yaml` configuration [click here](https://docs.flutter.dev/go/i18n-user-guide)

d. add wording in app_en (for English) and app_id (for Indonesian).

> **Note** : Make sure the key for wording in app_en and app_id is the same. If there is 1 key that does not have a partner from the 2 files, it will be put into untranslated_file.txt.

Example:
adding hello world in 2 different language

app_en.arb
```arb
{
  "helloWorld": "Hello world",
}
```

app_en.arb
```arb
{
  "helloWorld": "Hello Dunia",
}
```

| app_en.arb | app_id.arb |
|---|---|
| {<br> &emsp; "helloWorld": "Hello Word"   <br>} | {<br> &emsp; "helloWorld": "Halo Dunia"   <br>} |

> __Note__ : [In Here](https://docs.flutter.dev/go/i18n-user-guide), developer kan added description for the wording. Just add in one file wherever it is. The description doesn't be show in application.
```arb
{
    "helloWorld": "Hello World!",
    "@helloWorld": {
      "description": "The conventional newborn programmer greeting"
    }
}
```

e. Change `MyApp` widget in `main.dart` to following code : 

```dart
import 'package:flutter_localizations/flutter_localizations.dart';

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      title: 'Localizations Sample App',
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      supportedLocales: [
        Locale('en', ''), // English, no country code
        Locale('id', ''),, // Indonesia, no country code
      ],
      home: MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

then running the project so that the generate code will appear:

![2022-05-14_21h19_53](https://user-images.githubusercontent.com/54527045/168429715-fa10e70d-7086-4205-ada3-0a842f85a5a8.png)


f. call localization with folowing code :
```dart
final _wording = AppLocalization.of(context);

_wording.helloWorld
```