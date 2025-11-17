# Flutter i18n (Internationalization) Guide

## Overview

This project uses Flutter's built-in internationalization support with ARB (Application Resource Bundle) files for managing translations.

## Setup

### 1. Dependencies

Add to `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  intl: any
```

### 2. Enable Generation

Add to `pubspec.yaml`:

```yaml
flutter:
  generate: true
```

### 3. Configuration File

Create `l10n.yaml` in the root directory:

```yaml
arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
output-class: AppLocalizations
```

## Directory Structure

```
lib/
└── l10n/
    ├── app_en.arb          # English translations (template)
    ├── app_th.arb          # Thai translations
    └── app_[locale].arb    # Other languages
```

## ARB File Format

### English Template (app_en.arb)

```json
{
  "@@locale": "en",
  
  "appTitle": "My Flutter App",
  "@appTitle": {
    "description": "The title of the application"
  },
  
  "welcome": "Welcome",
  "@welcome": {
    "description": "Welcome message on the home screen"
  },
  
  "helloUser": "Hello, {username}!",
  "@helloUser": {
    "description": "Greeting message with user's name",
    "placeholders": {
      "username": {
        "type": "String",
        "example": "John"
      }
    }
  },
  
  "itemCount": "{count, plural, =0{No items} =1{1 item} other{{count} items}}",
  "@itemCount": {
    "description": "Number of items",
    "placeholders": {
      "count": {
        "type": "int",
        "format": "compact"
      }
    }
  },
  
  "lastUpdated": "Last updated: {date}",
  "@lastUpdated": {
    "description": "Timestamp of last update",
    "placeholders": {
      "date": {
        "type": "DateTime",
        "format": "yMMMd"
      }
    }
  },
  
  "loginButton": "Login",
  "logoutButton": "Logout",
  "cancel": "Cancel",
  "confirm": "Confirm",
  "save": "Save",
  "delete": "Delete",
  "edit": "Edit",
  
  "errorGeneric": "Something went wrong",
  "errorNetwork": "Network error. Please check your connection.",
  "errorNotFound": "Resource not found",
  
  "validationEmailInvalid": "Please enter a valid email",
  "validationFieldRequired": "This field is required",
  "validationPasswordTooShort": "Password must be at least 8 characters"
}
```

### Thai Translation (app_th.arb)

```json
{
  "@@locale": "th",
  
  "appTitle": "แอปพลิเคชันของฉัน",
  "welcome": "ยินดีต้อนรับ",
  "helloUser": "สวัสดี, {username}!",
  "itemCount": "{count, plural, =0{ไม่มีรายการ} =1{1 รายการ} other{{count} รายการ}}",
  "lastUpdated": "อัปเดตล่าสุด: {date}",
  
  "loginButton": "เข้าสู่ระบบ",
  "logoutButton": "ออกจากระบบ",
  "cancel": "ยกเลิก",
  "confirm": "ยืนยัน",
  "save": "บันทึก",
  "delete": "ลบ",
  "edit": "แก้ไข",
  
  "errorGeneric": "เกิดข้อผิดพลาด",
  "errorNetwork": "ข้อผิดพลาดเครือข่าย กรุณาตรวจสอบการเชื่อมต่อ",
  "errorNotFound": "ไม่พบทรัพยากร",
  
  "validationEmailInvalid": "กรุณากรอกอีเมลที่ถูกต้อง",
  "validationFieldRequired": "กรุณากรอกข้อมูลในช่องนี้",
  "validationPasswordTooShort": "รหัสผ่านต้องมีอย่างน้อย 8 ตัวอักษร"
}
```

## Implementation

### 1. Configure Main App

```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My Flutter App',
      
      // Localization delegates
      localizationsDelegates: const [
        AppLocalizations.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      
      // Supported locales
      supportedLocales: const [
        Locale('en', ''), // English
        Locale('th', ''), // Thai
      ],
      
      // Locale resolution
      localeResolutionCallback: (locale, supportedLocales) {
        // Check if the current device locale is supported
        for (var supportedLocale in supportedLocales) {
          if (supportedLocale.languageCode == locale?.languageCode) {
            return supportedLocale;
          }
        }
        // Default to English if device locale is not supported
        return supportedLocales.first;
      },
      
      home: const HomePage(),
    );
  }
}
```

### 2. Use Translations in Widgets

```dart
import 'package:flutter/material.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';

class HomePage extends StatelessWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final l10n = AppLocalizations.of(context)!;
    
    return Scaffold(
      appBar: AppBar(
        title: Text(l10n.appTitle),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              l10n.welcome,
              style: Theme.of(context).textTheme.headlineMedium,
            ),
            const SizedBox(height: 16),
            Text(l10n.helloUser('John')),
            const SizedBox(height: 16),
            Text(l10n.itemCount(5)),
            const SizedBox(height: 16),
            Text(l10n.lastUpdated(DateTime.now())),
          ],
        ),
      ),
    );
  }
}
```

### 3. Dynamic Locale Switching

Create a locale provider or use a state management solution:

```dart
// locale_bloc.dart
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:equatable/equatable.dart';
import 'package:flutter/material.dart';

// Events
abstract class LocaleEvent extends Equatable {
  const LocaleEvent();
}

class ChangeLocale extends LocaleEvent {
  final Locale locale;
  
  const ChangeLocale(this.locale);
  
  @override
  List<Object> get props => [locale];
}

// States
class LocaleState extends Equatable {
  final Locale locale;
  
  const LocaleState(this.locale);
  
  @override
  List<Object> get props => [locale];
}

// BLoC
class LocaleBloc extends Bloc<LocaleEvent, LocaleState> {
  LocaleBloc() : super(const LocaleState(Locale('en', ''))) {
    on<ChangeLocale>(_onChangeLocale);
  }
  
  void _onChangeLocale(ChangeLocale event, Emitter<LocaleState> emit) {
    emit(LocaleState(event.locale));
  }
}
```

### 4. Integrate Locale BLoC with App

```dart
// main.dart
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => LocaleBloc(),
      child: BlocBuilder<LocaleBloc, LocaleState>(
        builder: (context, state) {
          return MaterialApp(
            locale: state.locale,
            localizationsDelegates: const [
              AppLocalizations.delegate,
              GlobalMaterialLocalizations.delegate,
              GlobalWidgetsLocalizations.delegate,
              GlobalCupertinoLocalizations.delegate,
            ],
            supportedLocales: const [
              Locale('en', ''),
              Locale('th', ''),
            ],
            home: const HomePage(),
          );
        },
      ),
    );
  }
}
```

### 5. Language Switcher Widget

```dart
class LanguageSwitcher extends StatelessWidget {
  const LanguageSwitcher({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final currentLocale = Localizations.localeOf(context);
    
    return PopupMenuButton<Locale>(
      icon: const Icon(Icons.language),
      onSelected: (Locale locale) {
        context.read<LocaleBloc>().add(ChangeLocale(locale));
      },
      itemBuilder: (BuildContext context) => [
        PopupMenuItem(
          value: const Locale('en', ''),
          child: Row(
            children: [
              if (currentLocale.languageCode == 'en')
                const Icon(Icons.check, size: 20),
              const SizedBox(width: 8),
              const Text('English'),
            ],
          ),
        ),
        PopupMenuItem(
          value: const Locale('th', ''),
          child: Row(
            children: [
              if (currentLocale.languageCode == 'th')
                const Icon(Icons.check, size: 20),
              const SizedBox(width: 8),
              const Text('ไทย'),
            ],
          ),
        ),
      ],
    );
  }
}
```

## Advanced Usage

### 1. Pluralization

```json
// app_en.arb
{
  "itemCount": "{count, plural, =0{No items} =1{1 item} other{{count} items}}",
  "@itemCount": {
    "placeholders": {
      "count": {
        "type": "int"
      }
    }
  }
}

// Usage
Text(l10n.itemCount(0))  // "No items"
Text(l10n.itemCount(1))  // "1 item"
Text(l10n.itemCount(5))  // "5 items"
```

### 2. Date Formatting

```json
// app_en.arb
{
  "dateFormatted": "Date: {date}",
  "@dateFormatted": {
    "placeholders": {
      "date": {
        "type": "DateTime",
        "format": "yMMMd"
      }
    }
  }
}

// Usage
Text(l10n.dateFormatted(DateTime.now()))
```

### 3. Number Formatting

```json
// app_en.arb
{
  "price": "Price: ${amount}",
  "@price": {
    "placeholders": {
      "amount": {
        "type": "double",
        "format": "currency",
        "optionalParameters": {
          "symbol": "$"
        }
      }
    }
  }
}

// Usage
Text(l10n.price(99.99))  // "Price: $99.99"
```

### 4. Gender Selection

```json
// app_en.arb
{
  "greeting": "{gender, select, male{Hello Mr. {name}} female{Hello Ms. {name}} other{Hello {name}}}",
  "@greeting": {
    "placeholders": {
      "gender": {
        "type": "String"
      },
      "name": {
        "type": "String"
      }
    }
  }
}
```

## Best Practices

### 1. Key Naming Conventions

```
Format: [screen/feature][Element][Action/Type]

Examples:
- homeWelcomeMessage
- loginButtonText
- profileEditTitle
- errorNetworkMessage
- validationEmailInvalid
```

### 2. Organization

Group related strings by feature or screen:

```json
{
  "homeTitle": "Home",
  "homeWelcome": "Welcome",
  
  "loginTitle": "Login",
  "loginButton": "Sign In",
  "loginEmailLabel": "Email",
  "loginPasswordLabel": "Password",
  
  "errorGeneric": "An error occurred",
  "errorNetwork": "Network error"
}
```

### 3. Description and Context

Always provide descriptions for translators:

```json
{
  "submit": "Submit",
  "@submit": {
    "description": "Button text for submitting a form"
  }
}
```

### 4. Avoid Hardcoded Strings

❌ Bad:
```dart
Text('Hello')
```

✅ Good:
```dart
Text(l10n.hello)
```

### 5. Extract Helper Extension

Create an extension for easier access:

```dart
extension LocalizationExtension on BuildContext {
  AppLocalizations get l10n => AppLocalizations.of(this)!;
}

// Usage
Text(context.l10n.welcome)
```

### 6. Constants for Locale Codes

```dart
class AppLocales {
  static const english = Locale('en', '');
  static const thai = Locale('th', '');
  
  static const all = [english, thai];
}
```

### 7. Persist User Language Preference

```dart
// Save locale preference
Future<void> saveLocalePreference(String languageCode) async {
  final prefs = await SharedPreferences.getInstance();
  await prefs.setString('language_code', languageCode);
}

// Load locale preference
Future<Locale?> loadLocalePreference() async {
  final prefs = await SharedPreferences.getInstance();
  final languageCode = prefs.getString('language_code');
  if (languageCode != null) {
    return Locale(languageCode, '');
  }
  return null;
}
```

## Testing Localizations

### 1. Unit Test Translations

```dart
void main() {
  testWidgets('displays correct translations', (tester) async {
    await tester.pumpWidget(
      MaterialApp(
        localizationsDelegates: AppLocalizations.localizationsDelegates,
        supportedLocales: AppLocalizations.supportedLocales,
        locale: const Locale('en', ''),
        home: const HomePage(),
      ),
    );
    
    expect(find.text('Welcome'), findsOneWidget);
  });
}
```

### 2. Test Locale Switching

```dart
testWidgets('switches locale correctly', (tester) async {
  await tester.pumpWidget(const MyApp());
  
  // Initially English
  expect(find.text('Welcome'), findsOneWidget);
  
  // Switch to Thai
  await tester.tap(find.byIcon(Icons.language));
  await tester.pumpAndSettle();
  await tester.tap(find.text('ไทย'));
  await tester.pumpAndSettle();
  
  // Verify Thai text
  expect(find.text('ยินดีต้อนรับ'), findsOneWidget);
});
```

## Generation Command

After modifying ARB files, generate localization code:

```bash
flutter gen-l10n
```

Or it will auto-generate when you run:

```bash
flutter run
flutter build
```

## Common Patterns

### Feature-Specific Translations

```json
{
  "userProfileTitle": "User Profile",
  "userProfileEditButton": "Edit Profile",
  "userProfileSaveSuccess": "Profile saved successfully",
  "userProfileSaveError": "Failed to save profile"
}
```

### Error Messages

```json
{
  "errorNetworkTimeout": "Request timed out",
  "errorServerError": "Server error occurred",
  "errorUnauthorized": "You are not authorized",
  "errorNotFound": "Resource not found",
  "errorUnknown": "An unknown error occurred"
}
```

### Validation Messages

```json
{
  "validationRequired": "This field is required",
  "validationEmail": "Invalid email format",
  "validationMinLength": "Must be at least {length} characters",
  "validationMaxLength": "Must not exceed {length} characters",
  "validationPasswordMatch": "Passwords do not match"
}
```

## Troubleshooting

1. **Translations not updating**: Run `flutter clean` and `flutter pub get`
2. **Missing translations**: Check ARB file syntax and key consistency
3. **Build errors**: Ensure all placeholders are defined correctly
4. **Runtime errors**: Verify AppLocalizations.of(context) is not null

## Resources

- [Flutter Internationalization Guide](https://docs.flutter.dev/development/accessibility-and-localization/internationalization)
- [ARB Format Specification](https://github.com/google/app-resource-bundle)
- [Intl Package](https://pub.dev/packages/intl)
