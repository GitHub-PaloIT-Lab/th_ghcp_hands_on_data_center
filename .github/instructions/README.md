# Flutter Project Instructions

This directory contains comprehensive guidelines and best practices for developing Flutter applications following our project standards.

## 📚 Documentation Index

### Getting Started

1. **[FVM and Environment Setup](./flutter_fvm_setup_guide.md)**
   - FVM installation and configuration
   - Flutter 3.35.3 setup
   - IDE configuration (VS Code, Android Studio)
   - Team setup instructions

2. **[Project Overview](./flutter_project_overview.md)**
   - Project architecture and structure
   - Naming conventions
   - Code organization rules
   - Best practices

### Core Technologies

3. **[Flutter BLoC State Management](./flutter_bloc_guide.md)**
   - BLoC pattern implementation
   - Event and state management
   - Testing BLoCs
   - Performance optimization

4. **[Internationalization (i18n)](./flutter_i18n_guide.md)**
   - ARB file setup
   - Multi-language support (English, Thai)
   - Dynamic locale switching
   - Translation best practices

5. **[Routing Configuration](./flutter_routing_guide.md)**
   - go_router setup
   - Navigation patterns
   - Deep linking
   - Route guards and authentication

6. **[API and Mock Data](./flutter_api_mock_guide.md)**
   - Dio HTTP client configuration
   - Mock API implementation
   - Mock data structure
   - Testing with mocks

## 🚀 Quick Start

### Prerequisites

- macOS (for iOS development) or Linux/Windows (for Android only)
- FVM installed
- Xcode (for iOS) or Android Studio
- VS Code (recommended)

### Setup Steps

```bash
# 1. Clone the repository
git clone <repository-url>
cd <project-directory>

# 2. Install FVM (if not already installed)
brew tap leoafarias/fvm
brew install fvm

# 3. Install Flutter 3.35.3 via FVM
fvm install 3.35.3
fvm use 3.35.3

# 4. Get dependencies
fvm flutter pub get

# 5. Generate localization files
fvm flutter gen-l10n

# 6. Run the app
fvm flutter run
```

## 📁 Project Structure

```
lib/
├── main.dart                 # Application entry point
├── app/
│   ├── app.dart             # Main app widget
│   └── config/
│       ├── routes.dart      # Route definitions
│       └── theme.dart       # App theme
├── core/
│   ├── constants/           # App constants
│   ├── errors/              # Error handling
│   ├── network/             # API client and mocks
│   └── utils/               # Utilities
├── features/
│   └── [feature_name]/
│       ├── data/            # Data layer
│       ├── domain/          # Business logic
│       └── presentation/    # UI layer (BLoC, pages, widgets)
└── l10n/
    ├── app_en.arb          # English translations
    ├── app_th.arb          # Thai translations
    └── l10n.dart           # Generated localization
```

## 🎯 Development Guidelines

### State Management
- Use **Flutter BLoC** for all state management
- Follow event-state pattern
- Keep business logic in BLoC, not in UI

### Internationalization
- Support **English** and **Thai** languages
- Use ARB files for translations
- Never hardcode strings in UI

### Routing
- Use **go_router** for navigation
- Define routes in centralized configuration
- Use named routes for type safety

### API Integration
- All API calls are **mocked** using Dio interceptors
- Mock data should be realistic and comprehensive
- Include error scenarios in mocks

### Version Management
- Always use **FVM** for Flutter commands
- Project uses **Flutter 3.35.3**
- Run commands as: `fvm flutter <command>`

## 🧪 Testing

```bash
# Run all tests
fvm flutter test

# Run with coverage
fvm flutter test --coverage

# Run specific test
fvm flutter test test/features/user/user_bloc_test.dart
```

## 🔨 Common Commands

```bash
# Run app
fvm flutter run

# Build APK
fvm flutter build apk --release

# Build iOS
fvm flutter build ios --release

# Clean and rebuild
fvm flutter clean && fvm flutter pub get

# Generate code (for json_serializable, etc.)
fvm flutter pub run build_runner build --delete-conflicting-outputs

# Analyze code
fvm flutter analyze

# Format code
fvm flutter format .
```

## 📋 Coding Standards

### File Naming
- Use `snake_case` for file names
- BLoC: `[feature]_bloc.dart`, `[feature]_event.dart`, `[feature]_state.dart`
- Pages: `[page_name]_page.dart`
- Widgets: `[widget_name]_widget.dart`

### Class Naming
- Use `PascalCase` for class names
- Descriptive and clear names

### Code Quality
- Use `const` constructors where possible
- Leverage null safety
- Follow single responsibility principle
- Write meaningful comments for complex logic

## 🎨 UI Guidelines

### Widgets
- Prefer composition over inheritance
- Extract complex widgets into separate classes
- Use const constructors for performance

### Theming
- Define theme in `app/config/theme.dart`
- Use theme colors and text styles
- Support light and dark modes

### Responsive Design
- Use `MediaQuery` for screen dimensions
- Use `LayoutBuilder` for adaptive layouts
- Test on multiple screen sizes

## 🔄 Git Workflow

```bash
# Create feature branch
git checkout -b feature/user-profile

# Commit changes
git add .
git commit -m "feat: implement user profile page"

# Push changes
git push origin feature/user-profile

# Create pull request
```

### Commit Message Format
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes
- `refactor:` Code refactoring
- `test:` Test additions or changes
- `chore:` Build or configuration changes

## 🐛 Troubleshooting

### FVM Issues
```bash
# Reinstall Flutter version
fvm remove 3.35.3
fvm install 3.35.3
fvm use 3.35.3
```

### Build Issues
```bash
# Clean and rebuild
fvm flutter clean
rm -rf .dart_tool
fvm flutter pub get
```

### IDE Issues
- Restart IDE
- Invalidate caches (Android Studio)
- Check `.vscode/settings.json` has correct FVM path

## 📖 Additional Resources

- [Flutter Documentation](https://docs.flutter.dev/)
- [Flutter BLoC Package](https://bloclibrary.dev/)
- [go_router Package](https://pub.dev/packages/go_router)
- [Dio Package](https://pub.dev/packages/dio)
- [FVM Documentation](https://fvm.app/)

## 💬 Getting Help

1. Check the relevant guide in this directory
2. Review Flutter documentation
3. Check package documentation
4. Ask team members
5. Create an issue in the repository

## ✅ Checklist for New Features

- [ ] Follow feature-based structure
- [ ] Implement with BLoC pattern
- [ ] Add translations (EN & TH)
- [ ] Use mock data for API calls
- [ ] Add route configuration
- [ ] Write unit tests
- [ ] Write widget tests
- [ ] Update documentation
- [ ] Create pull request

---

**Happy Coding! 🚀**
