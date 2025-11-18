# FVM and Flutter Environment Setup Guide

## Overview

This project uses **FVM (Flutter Version Management)** to manage Flutter SDK versions, ensuring consistent development environments across the team.

## FVM Installation

### macOS/Linux

```bash
# Using Homebrew (recommended)
brew tap leoafarias/fvm
brew install fvm

# Or using pub
dart pub global activate fvm
```

### Verify Installation

```bash
fvm --version
```

## Project Setup

### 1. Initialize FVM in Project

Navigate to your project directory and set Flutter version:

```bash
# Set Flutter version 3.35.3 for this project
fvm use 3.35.3 --force

# If version is not installed, FVM will download it
fvm install 3.35.3
```

This creates:
- `.fvm/` directory in your project
- `.fvmrc` file (optional) containing version info
- `fvm_config.json` with project configuration

### 2. Project Structure After FVM Setup

```
project_root/
├── .fvm/
│   ├── flutter_sdk -> [symlink to Flutter 3.35.3]
│   └── fvm_config.json
├── .fvmrc (optional)
├── .gitignore
└── ...
```

### 3. Update .gitignore

```gitignore
# FVM Version Cache
.fvm/flutter_sdk

# Keep FVM config
!.fvm/fvm_config.json
```

### 4. Commit FVM Configuration

```bash
git add .fvm/fvm_config.json
git commit -m "Add FVM configuration for Flutter 3.35.3"
```

## Using FVM Commands

### Basic Commands

```bash
# Use Flutter commands through FVM
fvm flutter doctor
fvm flutter pub get
fvm flutter run
fvm flutter build apk

# Or set up alias (recommended)
alias flutter="fvm flutter"
alias dart="fvm dart"
```

### List Installed Versions

```bash
fvm list
```

### Install Specific Version

```bash
fvm install 3.35.3
```

### Switch Project Version

```bash
fvm use 3.35.3
```

### Remove Version

```bash
fvm remove 3.19.0
```

### Global Version (Optional)

```bash
# Set global default
fvm global 3.35.3

# Use global version
fvm global
```

## IDE Configuration

### VS Code Setup

1. **Install Flutter Extension**
   - Install "Flutter" extension by Dart Code

2. **Configure FVM Path**

Create `.vscode/settings.json`:

```json
{
  "dart.flutterSdkPath": ".fvm/flutter_sdk",
  "search.exclude": {
    "**/.fvm": true
  },
  "files.watcherExclude": {
    "**/.fvm": true
  }
}
```

3. **Recommended Extensions**

Create `.vscode/extensions.json`:

```json
{
  "recommendations": [
    "dart-code.flutter",
    "dart-code.dart-code",
    "alexisvt.flutter-snippets",
    "nash.awesome-flutter-snippets",
    "pflannery.vscode-versionlens"
  ]
}
```

### Android Studio / IntelliJ IDEA Setup

1. Open **Preferences/Settings**
2. Navigate to **Languages & Frameworks > Flutter**
3. Set Flutter SDK path to: `[PROJECT_PATH]/.fvm/flutter_sdk`

### Xcode Setup (iOS Development)

No special configuration needed. FVM works transparently with Xcode.

## Team Setup Instructions

### For New Team Members

When cloning the project:

```bash
# Clone repository
git clone <repository-url>
cd project-name

# Install FVM if not installed
brew install fvm

# Install Flutter version specified in project
fvm install

# Get dependencies
fvm flutter pub get

# Verify setup
fvm flutter doctor
```

### First-Time Flutter Setup

```bash
# Run Flutter doctor to check setup
fvm flutter doctor

# Accept Android licenses (if needed)
fvm flutter doctor --android-licenses

# Install development tools
fvm flutter precache
```

## Project Configuration Files

### pubspec.yaml

```yaml
name: my_flutter_app
description: A Flutter application with FVM
publish_to: 'none'
version: 1.0.0+1

environment:
  sdk: '>=3.0.0 <4.0.0'
  flutter: '>=3.35.3'

dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  
  # State Management
  flutter_bloc: ^8.1.3
  equatable: ^2.0.5
  
  # Routing
  go_router: ^13.0.0
  
  # Networking
  dio: ^5.4.0
  pretty_dio_logger: ^1.3.1
  
  # Internationalization
  intl: any
  
  # UI
  cached_network_image: ^3.3.1
  
  # Utilities
  shared_preferences: ^2.2.2
  path_provider: ^2.1.2

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  build_runner: ^2.4.7
  mockito: ^5.4.4
  bloc_test: ^9.1.5

flutter:
  uses-material-design: true
  generate: true
  
  assets:
    - assets/images/
    - assets/icons/
```

### analysis_options.yaml

```yaml
include: package:flutter_lints/flutter.yaml

linter:
  rules:
    # Errors
    avoid_relative_lib_imports: true
    avoid_types_as_parameter_names: true
    no_duplicate_case_values: true
    
    # Style
    prefer_const_constructors: true
    prefer_const_declarations: true
    prefer_const_literals_to_create_immutables: true
    prefer_final_fields: true
    prefer_final_locals: true
    
    # Pub
    sort_pub_dependencies: true
    
    # Documentation
    public_member_api_docs: false

analyzer:
  exclude:
    - "**/*.g.dart"
    - "**/*.freezed.dart"
    - "**/*.gen.dart"
  
  errors:
    invalid_annotation_target: ignore
```

### l10n.yaml

```yaml
arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
output-class: AppLocalizations
```

## Development Workflow

### Daily Development

```bash
# Start development
fvm flutter run

# Run with specific device
fvm flutter devices
fvm flutter run -d chrome
fvm flutter run -d emulator-5554

# Hot reload
# Press 'r' in terminal

# Hot restart
# Press 'R' in terminal

# Build for release
fvm flutter build apk --release
fvm flutter build ios --release
```

### Code Generation

```bash
# Generate code for json_serializable, etc.
fvm flutter pub run build_runner build

# Watch for changes
fvm flutter pub run build_runner watch

# Delete conflicting outputs
fvm flutter pub run build_runner build --delete-conflicting-outputs
```

### Testing

```bash
# Run all tests
fvm flutter test

# Run specific test file
fvm flutter test test/user_bloc_test.dart

# Run with coverage
fvm flutter test --coverage
fvm flutter test --coverage --test-randomize-ordering-seed=random

# Generate coverage report
genhtml coverage/lcov.info -o coverage/html
open coverage/html/index.html
```

### Clean Build

```bash
# Clean build artifacts
fvm flutter clean

# Get dependencies
fvm flutter pub get

# Rebuild
fvm flutter run
```

## CI/CD Configuration

### GitHub Actions Example

```yaml
name: Flutter CI

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]

jobs:
  build:
    runs-on: macos-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup FVM
      uses: kuhnroyal/flutter-fvm-config-action@v1
    
    - name: Install FVM
      run: |
        brew tap leoafarias/fvm
        brew install fvm
    
    - name: Install Flutter via FVM
      run: fvm install
    
    - name: Get dependencies
      run: fvm flutter pub get
    
    - name: Analyze code
      run: fvm flutter analyze
    
    - name: Run tests
      run: fvm flutter test
    
    - name: Build APK
      run: fvm flutter build apk --release
```

## Troubleshooting

### Common Issues

#### 1. FVM not found

```bash
# Add to PATH (add to ~/.zshrc or ~/.bash_profile)
export PATH="$PATH":"$HOME/.pub-cache/bin"
```

#### 2. Flutter SDK not found in IDE

- Restart IDE after setting FVM path
- Check that `.fvm/flutter_sdk` exists
- Verify symlink: `ls -la .fvm/`

#### 3. Version mismatch

```bash
# Force use specific version
fvm use 3.35.3 --force

# Reinstall if corrupted
fvm remove 3.35.3
fvm install 3.35.3
```

#### 4. Permission issues (macOS)

```bash
sudo chown -R $(whoami) ~/.fvm
```

#### 5. Slow download

```bash
# Use different mirror (China)
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

# Or set in FVM config
fvm config --pub-url https://pub.flutter-io.cn
```

## Best Practices

### 1. Always Use FVM Commands

```bash
# ❌ Don't
flutter pub get

# ✅ Do
fvm flutter pub get
```

### 2. Document Flutter Version

Add to `README.md`:

```markdown
## Requirements

- Flutter 3.35.3 (managed via FVM)
- Dart SDK (included with Flutter)
```

### 3. Shared Scripts

Create `scripts/` directory:

```bash
# scripts/setup.sh
#!/bin/bash
echo "Setting up Flutter project..."
fvm install
fvm flutter pub get
fvm flutter pub run build_runner build --delete-conflicting-outputs
echo "Setup complete!"

# scripts/test.sh
#!/bin/bash
fvm flutter test --coverage
genhtml coverage/lcov.info -o coverage/html
open coverage/html/index.html
```

Make executable:

```bash
chmod +x scripts/*.sh
```

### 4. Pre-commit Hooks

Install git hooks for code quality:

```bash
# .git/hooks/pre-commit
#!/bin/bash
echo "Running Flutter analyze..."
fvm flutter analyze

if [ $? -ne 0 ]; then
  echo "Flutter analyze failed. Commit aborted."
  exit 1
fi

echo "Running tests..."
fvm flutter test

if [ $? -ne 0 ]; then
  echo "Tests failed. Commit aborted."
  exit 1
fi
```

## Additional Tools

### Useful VS Code Tasks

Create `.vscode/tasks.json`:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Flutter: Run",
      "type": "shell",
      "command": "fvm flutter run",
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    },
    {
      "label": "Flutter: Clean",
      "type": "shell",
      "command": "fvm flutter clean && fvm flutter pub get",
      "problemMatcher": []
    },
    {
      "label": "Flutter: Test",
      "type": "shell",
      "command": "fvm flutter test",
      "problemMatcher": []
    },
    {
      "label": "Build Runner: Build",
      "type": "shell",
      "command": "fvm flutter pub run build_runner build --delete-conflicting-outputs",
      "problemMatcher": []
    }
  ]
}
```

### Launch Configuration

Create `.vscode/launch.json`:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Flutter: Run",
      "request": "launch",
      "type": "dart",
      "program": "lib/main.dart",
      "flutterMode": "debug"
    },
    {
      "name": "Flutter: Run (Profile)",
      "request": "launch",
      "type": "dart",
      "program": "lib/main.dart",
      "flutterMode": "profile"
    },
    {
      "name": "Flutter: Run (Release)",
      "request": "launch",
      "type": "dart",
      "program": "lib/main.dart",
      "flutterMode": "release"
    }
  ]
}
```

## Verification Checklist

After setup, verify:

```bash
# 1. Check FVM is working
fvm --version

# 2. Check Flutter version
fvm flutter --version

# 3. Check Flutter doctor
fvm flutter doctor -v

# 4. Check dependencies
fvm flutter pub get

# 5. Run app
fvm flutter run
```

## Resources

- [FVM Official Documentation](https://fvm.app/)
- [Flutter Documentation](https://docs.flutter.dev/)
- [Flutter Version Archive](https://docs.flutter.dev/development/tools/sdk/releases)
- [Dart SDK](https://dart.dev/get-dart)

## Support

For team support:
1. Check this documentation first
2. Review Flutter doctor output: `fvm flutter doctor -v`
3. Check FVM issues: https://github.com/leoafarias/fvm/issues
4. Contact team lead
