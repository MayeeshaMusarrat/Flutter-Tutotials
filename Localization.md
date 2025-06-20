I tried playing around with flutter localization (abbreviated as l10n, where “10” stands for the ten letters between “l” and “n”), and here is the summary of how it's done!

- **Install Dependencies: ** Install `flutter_localizations` and `intl` package from pub.dev.

- **Create ARB (Application Resource Bundle) files: ** Here is where you define your localized strings in JSON format. For my Bangla and English translations, I have app_en.arb and app_bn.arb files under lib/l10n directory.

- **Add l10n.yaml: ** This configuration file tells Flutter where to find your ARB files, which file to use as the base, what the output file should be named, and where to place it.  Mine looks like this:

`arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
output-dir: lib/l10n/generated
synthetic-package: false`

- ** Add generate: true in pubspec.yaml **: Make sure to put  generate: true under flutter in pubspec.yaml.

- **Generate Localization Class: ** Run `flutter gen-l10n` in the terminal. It generates necessary Dart classes from your ARB files in `output-dir` directory specified in l10n.yaml

- **Configure MaterialApp: ** Add `AppLocalizations.delegate` under MaterialApp. My code looks like:
  
`return MaterialApp.router(
         localizationsDelegates: const [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      supportedLocales: const [
        Locale('en'),
        Locale('bn'),
      ],
);`

- ** Use Localized Strings in Your Widgets: ** In your widget, write `final loc= AppLocalizations.of(context)!;` and use them like `Text(loc.title)`. The keyword `title` must remain in the ARB files with their corresponding translations in other languages.

For testing, I wrote `locale: Locale('bn')` in MaterialApp to see my app in Bangla. For dynamic change, use state management for locale.
