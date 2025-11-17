# 🚀 GitHub Copilot Hands-on Data Center

> **Central Knowledge Base Repository**  
> This repository contains comprehensive Flutter development instructions and best practices for GitHub Copilot.  
> Use these guidelines to ensure consistent, high-quality Flutter development with AI assistance.

## 📋 Overview

This repository provides comprehensive Flutter development guidelines designed to work seamlessly with GitHub Copilot, covering:

- ✅ **Flutter 3.35.3** with FVM (Flutter Version Management)
- ✅ **Flutter BLoC** for state management
- ✅ **Internationalization** (i18n) with English and Thai support
- ✅ **go_router** for type-safe navigation
- ✅ **Mock API** implementation with Dio
- ✅ **Clean Architecture** with feature-based structure

## 📁 Repository Structure

```
.github/
└── instructions/                    # Complete Flutter development guides
    ├── README.md                    # Quick start and overview
    ├── flutter_project_overview.md  # Architecture and structure
    ├── flutter_fvm_setup_guide.md   # FVM and environment setup
    ├── flutter_bloc_guide.md        # State management with BLoC
    ├── flutter_i18n_guide.md        # Internationalization
    ├── flutter_routing_guide.md     # Navigation and routing
    └── flutter_api_mock_guide.md    # API client and mocks
```

## 🎯 Key Features

These instructions enable GitHub Copilot to help you build Flutter apps with:

1. **Consistent Architecture**: Clean Architecture with clear layer separation
2. **State Management**: Flutter BLoC pattern with events and states
3. **Multi-language**: Built-in support for English and Thai
4. **Type-safe Routing**: Declarative routing with go_router
5. **Mock-first Development**: Work without backend dependencies
6. **Version Control**: FVM ensures team uses same Flutter version

## 🚀 Quick Start

### For New Projects:

1. **Review the instructions:**
   ```bash
   cd .github/instructions
   cat README.md
   ```

2. **Set up Flutter with FVM:**
   ```bash
   # Install FVM
   brew tap leoafarias/fvm
   brew install fvm
   
   # Install Flutter 3.35.3
   fvm install 3.35.3
   fvm use 3.35.3
   ```

3. **Create your Flutter project:**
   ```bash
   fvm flutter create my_app
   cd my_app
   ```

4. **Follow the guidelines** in `.github/instructions/` to structure your project

### For Existing Projects:

1. **Copy instructions to your project:**
   ```bash
   cp -r .github/instructions /path/to/your/project/.github/
   ```

2. **GitHub Copilot will automatically use these instructions** as context when helping you code

## 🛠️ Tech Stack Specifications

| Component | Technology | Version |
|-----------|-----------|---------|
| Flutter | Managed via FVM | 3.35.3 |
| State Management | flutter_bloc | ^8.1.3 |
| Routing | go_router | ^13.0.0 |
| HTTP Client | dio | ^5.4.0 |
| Localization | intl | any |
| Testing | bloc_test, mockito | latest |

## 📖 Documentation Guide

### Start Here:
- **[Instructions README](./.github/instructions/README.md)** - Overview and quick reference

### Essential Guides:
1. **[FVM Setup](./.github/instructions/flutter_fvm_setup_guide.md)**
   - Install and configure FVM
   - Set up Flutter 3.35.3
   - IDE configuration

2. **[Project Overview](./.github/instructions/flutter_project_overview.md)**
   - Architecture patterns
   - Directory structure
   - Naming conventions

3. **[BLoC Guide](./.github/instructions/flutter_bloc_guide.md)**
   - Event-State pattern
   - BLoC implementation
   - Testing strategies

4. **[i18n Guide](./.github/instructions/flutter_i18n_guide.md)**
   - ARB file setup
   - Language switching
   - Translation patterns

5. **[Routing Guide](./.github/instructions/flutter_routing_guide.md)**
   - go_router configuration
   - Navigation patterns
   - Deep linking

6. **[API & Mocks](./.github/instructions/flutter_api_mock_guide.md)**
   - Dio setup
   - Mock interceptors
   - Mock data patterns

## 🎓 Using with GitHub Copilot

### How It Works:

GitHub Copilot automatically reads files in `.github/` directories as context. By having these instructions in your project:

1. **Copilot understands your architecture** - It follows your project structure
2. **Copilot follows your patterns** - It generates code matching your style
3. **Copilot suggests best practices** - It applies documented guidelines
4. **Copilot knows your stack** - It uses your specified dependencies

### Example Copilot Prompts:

```
# Creating a new feature
"Create a user profile feature following our BLoC architecture with i18n support"

# Implementing navigation
"Add a route for the profile page using go_router with user ID parameter"

# Adding mock data
"Create mock API responses for user profile endpoints"

# Generating tests
"Write BLoC tests for the user profile feature"
```

### Best Practices:

1. **Reference the docs**: Ask Copilot to "follow our BLoC guide"
2. **Be specific**: Mention feature names and file locations
3. **Iterative refinement**: Start broad, then add details
4. **Review generated code**: Ensure it matches guidelines

## 📋 Project Structure Example

When following these instructions, your project will look like:

```
my_flutter_app/
├── .fvm/
│   ├── flutter_sdk -> [Flutter 3.35.3]
│   └── fvm_config.json
├── .github/
│   └── instructions/        # These guidelines
├── lib/
│   ├── main.dart
│   ├── app/
│   │   ├── app.dart
│   │   └── config/
│   │       ├── routes.dart
│   │       └── theme.dart
│   ├── core/
│   │   ├── network/
│   │   │   ├── api_client.dart
│   │   │   └── mock_api_client.dart
│   │   └── utils/
│   ├── features/
│   │   └── user_profile/
│   │       ├── data/
│   │       ├── domain/
│   │       └── presentation/
│   │           ├── bloc/
│   │           ├── pages/
│   │           └── widgets/
│   └── l10n/
│       ├── app_en.arb
│       └── app_th.arb
├── test/
└── pubspec.yaml
```

## 📖 Additional Resources

- [Flutter Documentation](https://flutter.dev/docs)
- [SQLite Package (sqflite)](https://pub.dev/packages/sqflite)
- [Flutter Integration Testing](https://docs.flutter.dev/testing/integration-tests)
- [GitHub Copilot Documentation](https://docs.github.com/copilot)

## 🤝 Contributing

To improve these instructions:

1. Create an issue for suggestions
2. Submit pull requests with improvements
3. Share effective Copilot prompts
4. Document common patterns and solutions

## 📝 Notes

- **Framework-agnostic where possible** - Core principles apply broadly
- **Opinionated architecture** - Follows Clean Architecture and BLoC patterns
- **Production-ready** - Based on real-world best practices
- **Copilot-optimized** - Structured for AI assistance

---

**Ready to build amazing Flutter apps with GitHub Copilot! 🚀**

For detailed guides, start with [.github/instructions/README.md](./.github/instructions/README.md)
````
