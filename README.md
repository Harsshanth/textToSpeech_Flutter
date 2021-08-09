# text2speech

A new Flutter project to convert text to speech using tts plugin 

Features 
[x] Android, iOS, Web, & macOS
[x] speak
[x] stop
[x] get languages
[x] set language
[x] set speech rate
[x] set speech volume
[x] set speech pitch
[x] is language available
[x] Android, iOS
[x] get voices
[x] set voice
[x] speech marks (requires iOS 7+ and Android 26+)
[x] synthesize to file (requires iOS 13+)
[x] iOS, Web
[x] pause
[x] Android
[x] set silence
[x] is language installed
[x] are languages installed
[x] get engines
[x] set engine
[x] get default engine
[x] set queue mode
[x] get max speech input length
[x] iOS
[x] set shared instance
[x] set audio session category
Usage 
macOS 
OSX version: 10.15
Example App from the macOS_app branch

Web 
Website from the example directory.

Android 
Change the minimum Android sdk version to 21 (or higher) in your android/app/build.gradle file.

minSdkVersion 21
Apps targeting Android 11 that use text-to-speech should declare TextToSpeech.Engine.INTENT_ACTION_TTS_SERVICE in the queries elements of their manifest.

iOS 
There's a known issue with integrating plugins that use Swift into a Flutter project created with the Objective-C template. Flutter#16049

Example

To use this plugin :

add the dependency to your pubspec.yaml file.
  dependencies:
    flutter:
      sdk: flutter
    flutter_tts:
instantiate FlutterTts
FlutterTts flutterTts = FlutterTts();

To set shared audio instance (iOS only):

await flutterTts.setSharedInstance(true);
To set audio category and options (iOS only):

await flutterTts
        .setIosAudioCategory(IosTextToSpeechAudioCategory.playAndRecord, [
      IosTextToSpeechAudioCategoryOptions.allowBluetooth,
      IosTextToSpeechAudioCategoryOptions.allowBluetoothA2DP,
      IosTextToSpeechAudioCategoryOptions.mixWithOthers
    ]);
To await speak completion.

await flutterTts.awaitSpeakCompletion(true);
To await synthesize to file completion.

await flutterTts.awaitSynthCompletion(true);
speak, stop, getLanguages, setLanguage, setSpeechRate, setVoice, setVolume, setPitch, isLanguageAvailable, setSharedInstance 
Future _speak() async{
    var result = await flutterTts.speak("Hello World");
    if (result == 1) setState(() => ttsState = TtsState.playing);
}

Future _stop() async{
    var result = await flutterTts.stop();
    if (result == 1) setState(() => ttsState = TtsState.stopped);
}

List<dynamic> languages = await flutterTts.getLanguages;

await flutterTts.setLanguage("en-US");

await flutterTts.setSpeechRate(1.0);

await flutterTts.setVolume(1.0);

await flutterTts.setPitch(1.0);

await flutterTts.isLanguageAvailable("en-US");

// iOS and Web only
await flutterTts.pause();

// iOS, macOS, and Android only
await flutterTts.synthesizeToFile("Hello World", Platform.isAndroid ? "tts.wav" : "tts.caf");

await flutterTts.setVoice({"name": "Karen", "locale": "en-AU"});

// iOS only
await flutterTts.setSharedInstance(true);

// Android only
await flutterTts.setSilence(2);

await flutterTts.getEngines();

await flutterTts.isLanguageInstalled("en-AU");

await flutterTts.areLanguagesInstalled(["en-AU", "en-US"]);

await flutterTts.setQueueMode(1);

await flutterTts.getMaxSpeechInputLength;
Listening for platform calls 
flutterTts.setStartHandler(() {
  setState(() {
    ttsState = TtsState.playing;
  });
});

flutterTts.setCompletionHandler(() {
  setState(() {
    ttsState = TtsState.stopped;
  });
});

flutterTts.setProgressHandler((String text, int startOffset, int endOffset, String word) {
  setState(() {
    _currentWord = word;
  });
});

flutterTts.setErrorHandler((msg) {
  setState(() {
    ttsState = TtsState.stopped;
  });
});

flutterTts.setCancelHandler((msg) {
  setState(() {
    ttsState = TtsState.stopped;
  });
});

// iOS and Web
flutterTts.setPauseHandler((msg) {
  setState(() {
    ttsState = TtsState.paused;
  });
});

flutterTts.setContinueHandler((msg) {
  setState(() {
    ttsState = TtsState.continued;
  });
});

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://flutter.dev/docs/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://flutter.dev/docs/cookbook)

For help getting started with Flutter, view our
[online documentation](https://flutter.dev/docs), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
