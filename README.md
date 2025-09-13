A collection of Providers for using the `path_provider` library with Riverpod.
You can synchronously retrieve various directory paths used in your application.

## Features

The following directory paths are provided as Riverpod Providers:

- `applicationCacheDirectory` - Application cache directory
- `applicationDocumentsDirectory` - Application documents directory
- `applicationSupportDirectory` - Application support directory
- `downloadsDirectory` - Downloads directory
- `externalStorageDirectory` - External storage directory
- `libraryDirectory` - Library directory
- `temporaryDirectory` - Temporary directory

## Getting started

1. Add the dependency to your `pubspec.yaml`:

```yaml
dependencies:
  path_provider_riverpod: ^1.1.0
```

2. Initialize the Provider when starting your application:

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

You can retrieve directory paths using Providers:

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

For testing, you can set arbitrary directories using the `injectWithValue` method:

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

This package supports Riverpod 3.0.
For migration from Riverpod 2.x to 3.x, please refer to the [official Riverpod migration guide](https://riverpod.dev/docs/migration/from_2_to_3).

## Additional information

This package is a Riverpod wrapper for the `path_provider` library.
For details about each directory, please refer to the `path_provider` package documentation.

Bug reports and feature requests are welcome on the GitHub repository's Issues page.
