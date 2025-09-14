`path_provider` ライブラリを Riverpod で使用するための Provider 集です。
アプリケーションで使用する各種ディレクトリパスを同期的に取得できます。

## Features

以下のディレクトリパスを Riverpod の Provider として提供します：

- `applicationCacheDirectory` - アプリケーションキャッシュディレクトリ
- `applicationDocumentsDirectory` - アプリケーションドキュメントディレクトリ
- `applicationSupportDirectory` - アプリケーションサポートディレクトリ
- `downloadsDirectory` - ダウンロードディレクトリ
- `externalStorageDirectory` - 外部ストレージディレクトリ
- `libraryDirectory` - ライブラリディレクトリ
- `temporaryDirectory` - テンポラリディレクトリ

## Getting started

1. `pubspec.yaml` に依存関係を追加します：

```yaml
dependencies:
  path_provider_riverpod: ^2.0.0
```

2. アプリケーション起動時に Provider を初期化します：

```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();

  final overrides = await PathProviders.inject();

  runApp(
    ProviderScope(
      overrides: overrides,
      child: MyApp(),
    ),
  );
}
```

## Usage

Provider を使用してディレクトリパスを取得できます：

```dart
class MyWidget extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final cacheDir = ref.watch(PathProviders.applicationCacheDirectory);
    final documentsDir = ref.watch(PathProviders.applicationDocumentsDirectory);

    return Column(
      children: [
        Text('Cache: ${cacheDir.path}'),
        Text('Documents: ${documentsDir.path}'),
      ],
    );
  }
}
```

テスト時には `injectWithValue` メソッドを使用して任意のディレクトリを設定できます：

```dart
testWidgets('test', (tester) async {
  await tester.pumpWidget(
    ProviderScope(
      overrides: PathProviders.injectWithValue(
        temporaryDirectory: Directory('/tmp/test'),
      ),
      child: MyApp(),
    ),
  );
});
```

## Version information

このパッケージは Riverpod 3.0 に対応しています。
Riverpod 2.x から 3.x への移行については、[Riverpod の公式移行ガイド](https://riverpod.dev/docs/migration/from_2_to_3)を参照してください。

## Additional information

このパッケージは `path_provider` ライブラリの Riverpod ラッパーです。
各ディレクトリの詳細については `path_provider` パッケージのドキュメントを参照してください。

バグレポートや機能要求は、GitHub リポジトリの Issues ページで受け付けています。
