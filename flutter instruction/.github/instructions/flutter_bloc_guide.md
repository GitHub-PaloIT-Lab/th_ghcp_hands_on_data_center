# Flutter BLoC State Management Guide

## Overview

This project uses **flutter_bloc** for state management following the BLoC (Business Logic Component) pattern. BLoC separates business logic from UI, making code more testable and maintainable.

## Core Concepts

### 1. BLoC Pattern Components

```
UI Event → BLoC → New State → UI Update
```

- **Events**: User actions or system events that trigger state changes
- **States**: Representations of the UI state at any given moment
- **BLoC**: Business logic that processes events and emits states

## File Structure per Feature

```
feature/
└── presentation/
    └── bloc/
        ├── [feature]_bloc.dart       # Main BLoC logic
        ├── [feature]_event.dart      # Event definitions
        └── [feature]_state.dart      # State definitions
```

## Implementation Guide

### 1. Define Events

Events represent intentions to perform actions. Always use Equatable for value comparison.

```dart
// user_profile_event.dart
part of 'user_profile_bloc.dart';

abstract class UserProfileEvent extends Equatable {
  const UserProfileEvent();

  @override
  List<Object?> get props => [];
}

class LoadUserProfile extends UserProfileEvent {
  final String userId;

  const LoadUserProfile(this.userId);

  @override
  List<Object?> get props => [userId];
}

class UpdateUserProfile extends UserProfileEvent {
  final String name;
  final String email;

  const UpdateUserProfile({
    required this.name,
    required this.email,
  });

  @override
  List<Object?> get props => [name, email];
}

class RefreshUserProfile extends UserProfileEvent {
  const RefreshUserProfile();
}
```

### 2. Define States

States represent the current condition of the feature. Use sealed classes pattern or explicit state classes.

```dart
// user_profile_state.dart
part of 'user_profile_bloc.dart';

abstract class UserProfileState extends Equatable {
  const UserProfileState();

  @override
  List<Object?> get props => [];
}

class UserProfileInitial extends UserProfileState {
  const UserProfileInitial();
}

class UserProfileLoading extends UserProfileState {
  const UserProfileLoading();
}

class UserProfileLoaded extends UserProfileState {
  final User user;

  const UserProfileLoaded(this.user);

  @override
  List<Object?> get props => [user];
}

class UserProfileError extends UserProfileState {
  final String message;

  const UserProfileError(this.message);

  @override
  List<Object?> get props => [message];
}

class UserProfileUpdating extends UserProfileState {
  final User currentUser;

  const UserProfileUpdating(this.currentUser);

  @override
  List<Object?> get props => [currentUser];
}
```

### 3. Implement BLoC

The BLoC class processes events and emits states.

```dart
// user_profile_bloc.dart
import 'package:flutter_bloc/flutter_bloc.dart';
import 'package:equatable/equatable.dart';

part 'user_profile_event.dart';
part 'user_profile_state.dart';

class UserProfileBloc extends Bloc<UserProfileEvent, UserProfileState> {
  final GetUser getUser;
  final UpdateUser updateUser;

  UserProfileBloc({
    required this.getUser,
    required this.updateUser,
  }) : super(const UserProfileInitial()) {
    on<LoadUserProfile>(_onLoadUserProfile);
    on<UpdateUserProfile>(_onUpdateUserProfile);
    on<RefreshUserProfile>(_onRefreshUserProfile);
  }

  Future<void> _onLoadUserProfile(
    LoadUserProfile event,
    Emitter<UserProfileState> emit,
  ) async {
    emit(const UserProfileLoading());
    
    final result = await getUser(event.userId);
    
    result.fold(
      (failure) => emit(UserProfileError(failure.message)),
      (user) => emit(UserProfileLoaded(user)),
    );
  }

  Future<void> _onUpdateUserProfile(
    UpdateUserProfile event,
    Emitter<UserProfileState> emit,
  ) async {
    if (state is UserProfileLoaded) {
      final currentUser = (state as UserProfileLoaded).user;
      emit(UserProfileUpdating(currentUser));
      
      final result = await updateUser(
        userId: currentUser.id,
        name: event.name,
        email: event.email,
      );
      
      result.fold(
        (failure) => emit(UserProfileError(failure.message)),
        (user) => emit(UserProfileLoaded(user)),
      );
    }
  }

  Future<void> _onRefreshUserProfile(
    RefreshUserProfile event,
    Emitter<UserProfileState> emit,
  ) async {
    if (state is UserProfileLoaded) {
      final currentUser = (state as UserProfileLoaded).user;
      await _onLoadUserProfile(
        LoadUserProfile(currentUser.id),
        emit,
      );
    }
  }
}
```

### 4. Provide BLoC to Widget Tree

Use `BlocProvider` to inject BLoC into the widget tree.

```dart
class UserProfilePage extends StatelessWidget {
  final String userId;

  const UserProfilePage({Key? key, required this.userId}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => UserProfileBloc(
        getUser: GetUser(context.read<UserRepository>()),
        updateUser: UpdateUser(context.read<UserRepository>()),
      )..add(LoadUserProfile(userId)),
      child: const UserProfileView(),
    );
  }
}
```

### 5. Consume BLoC in UI

Use `BlocBuilder`, `BlocListener`, or `BlocConsumer` to react to state changes.

#### BlocBuilder - Rebuild UI on State Changes

```dart
class UserProfileView extends StatelessWidget {
  const UserProfileView({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('User Profile')),
      body: BlocBuilder<UserProfileBloc, UserProfileState>(
        builder: (context, state) {
          if (state is UserProfileLoading) {
            return const Center(child: CircularProgressIndicator());
          }
          
          if (state is UserProfileError) {
            return Center(child: Text('Error: ${state.message}'));
          }
          
          if (state is UserProfileLoaded) {
            return UserProfileContent(user: state.user);
          }
          
          return const SizedBox.shrink();
        },
      ),
    );
  }
}
```

#### BlocListener - Side Effects without Rebuilding

```dart
BlocListener<UserProfileBloc, UserProfileState>(
  listener: (context, state) {
    if (state is UserProfileError) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text(state.message)),
      );
    }
    
    if (state is UserProfileLoaded) {
      // Navigate or show success message
    }
  },
  child: ChildWidget(),
)
```

#### BlocConsumer - Both Builder and Listener

```dart
BlocConsumer<UserProfileBloc, UserProfileState>(
  listener: (context, state) {
    if (state is UserProfileError) {
      ScaffoldMessenger.of(context).showSnackBar(
        SnackBar(content: Text(state.message)),
      );
    }
  },
  builder: (context, state) {
    if (state is UserProfileLoading) {
      return const CircularProgressIndicator();
    }
    return UserProfileContent(user: state.user);
  },
)
```

### 6. Trigger Events

Dispatch events from UI to BLoC using `context.read<BLoC>().add()`.

```dart
ElevatedButton(
  onPressed: () {
    context.read<UserProfileBloc>().add(
      UpdateUserProfile(
        name: nameController.text,
        email: emailController.text,
      ),
    );
  },
  child: const Text('Update Profile'),
)
```

## Best Practices

### 1. State Immutability
- Always create new state instances
- Use `copyWith` methods for partial updates
- Never mutate existing states

```dart
class UserProfileLoaded extends UserProfileState {
  final User user;

  const UserProfileLoaded(this.user);

  UserProfileLoaded copyWith({User? user}) {
    return UserProfileLoaded(user ?? this.user);
  }

  @override
  List<Object?> get props => [user];
}
```

### 2. Event Granularity
- Create specific events for specific actions
- Avoid generic events like `UpdateState`
- Events should be intention-revealing

### 3. State Specificity
- Create distinct states for different UI conditions
- Avoid boolean flags in states (use separate state classes)
- Consider using loading states that include previous data

```dart
// Good: Loading with previous data
class UserProfileRefreshing extends UserProfileState {
  final User currentUser;
  const UserProfileRefreshing(this.currentUser);
}

// Avoid: Generic loading flag
class UserProfileLoaded extends UserProfileState {
  final User user;
  final bool isRefreshing;
  const UserProfileLoaded(this.user, this.isRefreshing);
}
```

### 4. Error Handling
- Always handle errors in BLoC
- Create specific error states with messages
- Log errors for debugging

```dart
Future<void> _onLoadUser(
  LoadUserProfile event,
  Emitter<UserProfileState> emit,
) async {
  emit(const UserProfileLoading());
  
  try {
    final result = await getUser(event.userId);
    
    result.fold(
      (failure) {
        // Log error
        debugPrint('Failed to load user: ${failure.message}');
        emit(UserProfileError(failure.message));
      },
      (user) => emit(UserProfileLoaded(user)),
    );
  } catch (e, stackTrace) {
    debugPrint('Unexpected error: $e\n$stackTrace');
    emit(const UserProfileError('An unexpected error occurred'));
  }
}
```

### 5. BLoC Lifecycle
- Close BLoC properly to avoid memory leaks
- BlocProvider handles disposal automatically
- For manual creation, always call `bloc.close()`

### 6. Testing BLoCs
Use `bloc_test` package for easy BLoC testing.

```dart
blocTest<UserProfileBloc, UserProfileState>(
  'emits [UserProfileLoading, UserProfileLoaded] when LoadUserProfile succeeds',
  build: () {
    when(() => mockGetUser(any())).thenAnswer(
      (_) async => Right(mockUser),
    );
    return UserProfileBloc(getUser: mockGetUser);
  },
  act: (bloc) => bloc.add(const LoadUserProfile('123')),
  expect: () => [
    const UserProfileLoading(),
    UserProfileLoaded(mockUser),
  ],
);
```

### 7. Multiple BLoCs
- Use `MultiBlocProvider` for multiple BLoCs
- Keep BLoCs scoped appropriately
- Share BLoCs across routes when needed

```dart
MultiBlocProvider(
  providers: [
    BlocProvider(create: (context) => AuthBloc()),
    BlocProvider(create: (context) => UserProfileBloc()),
    BlocProvider(create: (context) => SettingsBloc()),
  ],
  child: MyApp(),
)
```

### 8. BLoC Communication
- Use repositories or services for shared data
- Consider using streams for BLoC-to-BLoC communication
- Avoid direct BLoC dependencies

```dart
// Good: Through repository
class UserProfileBloc {
  final UserRepository userRepository;
  
  UserProfileBloc({required this.userRepository}) {
    // Listen to repository stream
    userRepository.userStream.listen((user) {
      add(UserUpdated(user));
    });
  }
}

// Avoid: Direct BLoC dependency
class UserProfileBloc {
  final AuthBloc authBloc; // Avoid this
}
```

## Common Patterns

### Loading State with Previous Data

```dart
class DataLoading extends MyState {
  final Data? previousData;
  const DataLoading({this.previousData});
}
```

### Debouncing Events

```dart
EventTransformer<E> debounce<E>(Duration duration) {
  return (events, mapper) => events.debounceTime(duration).flatMap(mapper);
}

class SearchBloc extends Bloc<SearchEvent, SearchState> {
  SearchBloc() : super(SearchInitial()) {
    on<SearchQueryChanged>(
      _onSearchQueryChanged,
      transformer: debounce(const Duration(milliseconds: 300)),
    );
  }
}
```

### Pagination

```dart
class DataLoaded extends MyState {
  final List<Item> items;
  final bool hasReachedMax;
  
  const DataLoaded({
    required this.items,
    required this.hasReachedMax,
  });
}

on<LoadMoreData>((event, emit) async {
  if (state is DataLoaded) {
    final currentState = state as DataLoaded;
    if (!currentState.hasReachedMax) {
      // Load more data
    }
  }
});
```

## Performance Tips

1. **Use buildWhen for BlocBuilder**: Only rebuild when necessary
   ```dart
   BlocBuilder<MyBloc, MyState>(
     buildWhen: (previous, current) => previous.data != current.data,
     builder: (context, state) => Widget(),
   )
   ```

2. **Use listenWhen for BlocListener**: Only listen to relevant changes
   ```dart
   BlocListener<MyBloc, MyState>(
     listenWhen: (previous, current) => previous.status != current.status,
     listener: (context, state) { },
   )
   ```

3. **Const Widgets**: Use const constructors wherever possible
4. **Selector**: Use BlocSelector for specific field changes
   ```dart
   BlocSelector<MyBloc, MyState, String>(
     selector: (state) => state.username,
     builder: (context, username) => Text(username),
   )
   ```

## Troubleshooting

### Common Issues

1. **State not updating**: Check Equatable props
2. **Multiple rebuilds**: Use buildWhen to filter
3. **Memory leaks**: Ensure BLoC is properly closed
4. **Events not triggering**: Check if BLoC is provided correctly

## References

- [flutter_bloc documentation](https://bloclibrary.dev/)
- [BLoC architecture](https://bloclibrary.dev/#/architecture)
- [bloc_test package](https://pub.dev/packages/bloc_test)
