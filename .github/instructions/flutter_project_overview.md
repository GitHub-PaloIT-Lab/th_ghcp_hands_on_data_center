# Flutter Project Overview

## Project Architecture

This Flutter application follows Clean Architecture principles with BLoC state management pattern.

### Directory Structure

```
lib/
├── main.dart                 # Application entry point
├── app/
│   ├── app.dart             # Main app widget with routing and theme
│   └── config/
│       ├── routes.dart      # Route definitions
│       └── theme.dart       # App theme configuration
├── core/
│   ├── constants/
│   │   └── api_constants.dart
│   ├── errors/
│   │   ├── exceptions.dart
│   │   └── failures.dart
│   ├── network/
│   │   ├── api_client.dart
│   │   └── mock_api_client.dart
│   └── utils/
│       └── helpers.dart
├── features/
│   └── [feature_name]/
│       ├── data/
│       │   ├── models/
│       │   ├── repositories/
│       │   └── datasources/
│       ├── domain/
│       │   ├── entities/
│       │   ├── repositories/
│       │   └── usecases/
│       └── presentation/
│           ├── bloc/
│           ├── pages/
│           └── widgets/
└── l10n/
    ├── app_en.arb
    ├── app_th.arb
    └── l10n.dart           # Generated localization file
```

## Code Organization Rules

### 1. Feature-Based Structure
- Each feature should be self-contained in its own directory under `features/`
- Follow the data-domain-presentation layer separation
- Features should communicate through well-defined interfaces

### 2. Layer Responsibilities

#### Data Layer (`data/`)
- **Models**: JSON serialization and data transfer objects
- **Repositories**: Implementation of repository interfaces
- **DataSources**: API calls and data fetching logic (use mocks)

#### Domain Layer (`domain/`)
- **Entities**: Pure business objects without any framework dependencies
- **Repositories**: Abstract repository interfaces
- **UseCases**: Business logic and use case implementations

#### Presentation Layer (`presentation/`)
- **BLoC**: State management (events, states, and bloc classes)
- **Pages**: Full screen widgets
- **Widgets**: Reusable UI components specific to this feature

## Naming Conventions

### Files
- Use snake_case for file names: `user_profile_page.dart`
- BLoC files: `[feature]_bloc.dart`, `[feature]_event.dart`, `[feature]_state.dart`
- Model files: `[entity]_model.dart`
- Widget files: `[widget_name]_widget.dart`

### Classes
- Use PascalCase: `UserProfilePage`, `UserProfileBloc`
- BLoC classes: `[Feature]Bloc`, `[Feature]Event`, `[Feature]State`
- Model classes: `[Entity]Model`
- Widget classes: `[Widget]Widget` or descriptive names

### Variables and Functions
- Use camelCase: `userName`, `fetchUserData()`
- Private members: prefix with underscore `_privateMethod()`
- Constants: use lowerCamelCase or UPPER_CASE for compile-time constants

## Best Practices

### Code Quality
1. **Null Safety**: Always leverage Dart's null safety features
2. **Immutability**: Prefer immutable data structures (use `const` where possible)
3. **Single Responsibility**: Each class should have one clear purpose
4. **Dependency Injection**: Use constructor injection for dependencies
5. **Error Handling**: Always handle errors gracefully with try-catch or Either pattern

### Widget Development
1. **Composition**: Build complex UIs by composing smaller widgets
2. **Const Constructors**: Use `const` constructors wherever possible for better performance
3. **Extract Widgets**: If a widget becomes too complex, extract it into a separate class
4. **Responsive Design**: Use MediaQuery and LayoutBuilder for responsive layouts

### Performance
1. **Avoid rebuilds**: Use `const` widgets and proper BLoC state management
2. **Lazy loading**: Implement pagination for lists
3. **Image optimization**: Use cached network images
4. **Dispose resources**: Always dispose controllers, streams, and subscriptions

## Dependencies Structure

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  intl: any
  flutter_bloc: ^8.1.3
  equatable: ^2.0.5
  go_router: ^13.0.0
  dio: ^5.4.0
  mockito: ^5.4.4
  json_annotation: ^4.8.1

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^3.0.0
  build_runner: ^2.4.7
  json_serializable: ^6.7.1
  bloc_test: ^9.1.5
```

## Testing Strategy

### Unit Tests
- Test all business logic in UseCases
- Test BLoC events and states
- Test data models serialization/deserialization

### Widget Tests
- Test individual widgets in isolation
- Test widget interactions and state changes
- Use `pumpWidget` and `find` to test UI elements

### Integration Tests
- Test complete user flows
- Test navigation between screens
- Test API integration with mocks

## Common Patterns

### Repository Pattern
```dart
abstract class UserRepository {
  Future<Either<Failure, User>> getUser(String id);
}

class UserRepositoryImpl implements UserRepository {
  final UserRemoteDataSource remoteDataSource;
  
  UserRepositoryImpl({required this.remoteDataSource});
  
  @override
  Future<Either<Failure, User>> getUser(String id) async {
    try {
      final userModel = await remoteDataSource.getUser(id);
      return Right(userModel.toEntity());
    } catch (e) {
      return Left(ServerFailure());
    }
  }
}
```

### UseCase Pattern
```dart
class GetUser {
  final UserRepository repository;
  
  GetUser(this.repository);
  
  Future<Either<Failure, User>> call(String userId) {
    return repository.getUser(userId);
  }
}
```

## Git Workflow

1. Create feature branches from `main`: `feature/user-profile`
2. Commit messages should be clear and descriptive
3. Create pull requests for code review
4. Ensure all tests pass before merging

## Development Workflow

1. **Start**: Set up FVM with Flutter 3.35.3
2. **Create Feature**: Follow the feature-based structure
3. **Implement Domain**: Define entities and use cases first
4. **Implement Data**: Create models and repositories with mocks
5. **Implement Presentation**: Build UI with BLoC
6. **Test**: Write unit and widget tests
7. **Review**: Submit for code review
