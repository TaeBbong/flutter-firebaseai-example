# Firebase AI Logic Tutorial

플러터 앱에 Firebase AI Logic을 적용하기 위한 튜토리얼 입니다.

## 환경(버전)

- Flutter : 3.38.5(25.12.11)
- Dart : 3.10.4(25.12.9)

1. Firebase console에서 프로젝트 만들기
2. Firebase console project에서 앱 추가, 플랫폼 선택 -> 플러터
3. Flutter 앱에 Firebase 추가, 따라하기(flutterfire)
   - flutterfire configure --project=flutter-firebaseai
4. dart pub add
   - firebase_core, firebase_ai
5. Firebase console -> AI -> Firebase AI Logic 시작하기
   - 세부 단계 : 스크린샷 참고
6. main.dart

   ```dart
   import 'package:firebase_core/firebase_core.dart';
   import 'package:flutter/material.dart';

   import 'firebase_options.dart';

   void main() async {
   await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
   runApp(const MainApp());
   }

   class MainApp extends StatelessWidget {
   const MainApp({super.key});

   @override
   Widget build(BuildContext context) {
       return const MaterialApp(
       home: Scaffold(body: Center(child: Text('Hello World!'))),
       );
   }
   }
   ```

7. 코드 구현

   ```dart
   _model = FirebaseAI.googleAI().generativeModel(model: 'gemini-2.5-flash');
   final response = await _model.generateContent([Content.text(text)]);
   final responseText = response.text ?? '응답을 받지 못했습니다.';
   ```

8. 에러(iOS)

   ```bash
   [!] Automatically assigning platform `iOS` with version `13.0` on target `Runner` because no platform was specified. Please specify a platform for this target in your Podfile. See `https://guides.cocoapods.org/syntax/podfile.html#platform`.

   Error: The plugin "firebase_app_check" requires a higher minimum iOS deployment version than your application is targeting.

   To build, increase your application's deployment target to at least 15.0 as described at https://flutter.dev/to/ios-deploy

   Error running pod install

   Error launching application on iPhone 16 Pro.
   ```

-> iOS minimum sdk version 15로 업데이트
