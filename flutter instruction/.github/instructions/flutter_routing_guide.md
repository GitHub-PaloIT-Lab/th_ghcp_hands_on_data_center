# Flutter Routing Guide

## Overview

This project uses **go_router** for declarative routing and navigation. It provides type-safe routing, deep linking, and URL-based navigation.

## Setup

### 1. Dependencies

Add to `pubspec.yaml`:

```yaml
dependencies:
  go_router: ^13.0.0
```

### 2. Directory Structure

```
lib/
└── app/
    └── config/
        └── routes.dart       # Route configuration
```

## Basic Configuration

### 1. Define Routes

Create a centralized router configuration:

```dart
// app/config/routes.dart
import 'package:flutter/material.dart';
import 'package:go_router/go_router.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

// Route names (constants for type-safety)
class Routes {
  static const splash = '/';
  static const home = '/home';
  static const login = '/login';
  static const userProfile = '/profile/:userId';
  static const settings = '/settings';
  static const notFound = '/404';
}

// Router configuration
final appRouter = GoRouter(
  initialLocation: Routes.splash,
  debugLogDiagnostics: true,
  
  // Error handling
  errorBuilder: (context, state) => const NotFoundPage(),
  
  // Routes
  routes: [
    GoRoute(
      path: Routes.splash,
      name: 'splash',
      builder: (context, state) => const SplashPage(),
    ),
    
    GoRoute(
      path: Routes.home,
      name: 'home',
      builder: (context, state) => const HomePage(),
    ),
    
    GoRoute(
      path: Routes.login,
      name: 'login',
      builder: (context, state) => const LoginPage(),
    ),
    
    GoRoute(
      path: Routes.userProfile,
      name: 'userProfile',
      builder: (context, state) {
        final userId = state.pathParameters['userId']!;
        return UserProfilePage(userId: userId);
      },
    ),
    
    GoRoute(
      path: Routes.settings,
      name: 'settings',
      builder: (context, state) => const SettingsPage(),
    ),
  ],
  
  // Redirect logic (authentication, etc.)
  redirect: (context, state) {
    // Example: Check if user is authenticated
    final isAuthenticated = false; // Get from auth state
    final isGoingToLogin = state.matchedLocation == Routes.login;
    
    if (!isAuthenticated && !isGoingToLogin) {
      return Routes.login;
    }
    
    if (isAuthenticated && isGoingToLogin) {
      return Routes.home;
    }
    
    return null; // No redirect needed
  },
);
```

### 2. Integrate with App

```dart
// main.dart
import 'package:flutter/material.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';
import 'app/config/routes.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      title: 'My Flutter App',
      routerConfig: appRouter,
      
      // Localization
      localizationsDelegates: AppLocalizations.localizationsDelegates,
      supportedLocales: AppLocalizations.supportedLocales,
    );
  }
}
```

## Navigation Patterns

### 1. Basic Navigation

```dart
// Navigate to a route
context.go('/home');

// Navigate with named route
context.goNamed('home');

// Navigate with parameters
context.go('/profile/123');
context.goNamed('userProfile', pathParameters: {'userId': '123'});

// Push (add to stack)
context.push('/settings');

// Replace current route
context.replace('/login');

// Pop
context.pop();

// Pop with result
context.pop('result');
```

### 2. Passing Data

#### Path Parameters

```dart
// Route definition
GoRoute(
  path: '/profile/:userId',
  name: 'userProfile',
  builder: (context, state) {
    final userId = state.pathParameters['userId']!;
    return UserProfilePage(userId: userId);
  },
),

// Navigation
context.goNamed('userProfile', pathParameters: {'userId': '123'});
```

#### Query Parameters

```dart
// Route definition
GoRoute(
  path: '/search',
  name: 'search',
  builder: (context, state) {
    final query = state.uri.queryParameters['q'] ?? '';
    final filter = state.uri.queryParameters['filter'] ?? 'all';
    return SearchPage(query: query, filter: filter);
  },
),

// Navigation
context.goNamed('search', queryParameters: {
  'q': 'flutter',
  'filter': 'recent',
});
```

#### Extra Data (Object)

```dart
// Route definition
GoRoute(
  path: '/edit-profile',
  name: 'editProfile',
  builder: (context, state) {
    final user = state.extra as User;
    return EditProfilePage(user: user);
  },
),

// Navigation
context.goNamed('editProfile', extra: currentUser);
```

### 3. Nested Routes

```dart
GoRoute(
  path: '/settings',
  name: 'settings',
  builder: (context, state) => const SettingsPage(),
  routes: [
    GoRoute(
      path: 'account',
      name: 'settingsAccount',
      builder: (context, state) => const AccountSettingsPage(),
    ),
    GoRoute(
      path: 'privacy',
      name: 'settingsPrivacy',
      builder: (context, state) => const PrivacySettingsPage(),
    ),
  ],
),

// Navigation
context.goNamed('settingsAccount'); // Goes to /settings/account
```

### 4. Shell Routes (Persistent UI)

For layouts with persistent navigation (bottom nav, drawer):

```dart
final appRouter = GoRouter(
  routes: [
    ShellRoute(
      builder: (context, state, child) {
        return MainScaffold(child: child);
      },
      routes: [
        GoRoute(
          path: '/home',
          builder: (context, state) => const HomePage(),
        ),
        GoRoute(
          path: '/explore',
          builder: (context, state) => const ExplorePage(),
        ),
        GoRoute(
          path: '/profile',
          builder: (context, state) => const ProfilePage(),
        ),
      ],
    ),
  ],
);

class MainScaffold extends StatelessWidget {
  final Widget child;
  
  const MainScaffold({Key? key, required this.child}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: child,
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _calculateSelectedIndex(context),
        onTap: (index) => _onItemTapped(index, context),
        items: const [
          BottomNavigationBarItem(icon: Icon(Icons.home), label: 'Home'),
          BottomNavigationBarItem(icon: Icon(Icons.explore), label: 'Explore'),
          BottomNavigationBarItem(icon: Icon(Icons.person), label: 'Profile'),
        ],
      ),
    );
  }
  
  int _calculateSelectedIndex(BuildContext context) {
    final location = GoRouterState.of(context).matchedLocation;
    if (location.startsWith('/home')) return 0;
    if (location.startsWith('/explore')) return 1;
    if (location.startsWith('/profile')) return 2;
    return 0;
  }
  
  void _onItemTapped(int index, BuildContext context) {
    switch (index) {
      case 0:
        context.go('/home');
        break;
      case 1:
        context.go('/explore');
        break;
      case 2:
        context.go('/profile');
        break;
    }
  }
}
```

## Advanced Features

### 1. Authentication Guards

```dart
final appRouter = GoRouter(
  routes: [...],
  redirect: (context, state) {
    final authState = context.read<AuthBloc>().state;
    final isAuthenticated = authState is AuthAuthenticated;
    final isGoingToAuth = state.matchedLocation.startsWith('/login') ||
                          state.matchedLocation.startsWith('/register');
    
    // Not authenticated and trying to access protected route
    if (!isAuthenticated && !isGoingToAuth) {
      return '/login?redirect=${state.matchedLocation}';
    }
    
    // Authenticated and trying to access auth pages
    if (isAuthenticated && isGoingToAuth) {
      final redirectPath = state.uri.queryParameters['redirect'];
      return redirectPath ?? '/home';
    }
    
    return null;
  },
  refreshListenable: GoRouterRefreshStream(
    context.read<AuthBloc>().stream,
  ),
);

// Helper class for listening to BLoC changes
class GoRouterRefreshStream extends ChangeNotifier {
  GoRouterRefreshStream(Stream<dynamic> stream) {
    notifyListeners();
    _subscription = stream.asBroadcastStream().listen(
      (dynamic _) => notifyListeners(),
    );
  }

  late final StreamSubscription<dynamic> _subscription;

  @override
  void dispose() {
    _subscription.cancel();
    super.dispose();
  }
}
```

### 2. Deep Linking

```dart
// Route definition
GoRoute(
  path: '/post/:id',
  name: 'postDetail',
  builder: (context, state) {
    final postId = state.pathParameters['id']!;
    return PostDetailPage(postId: postId);
  },
),

// Deep link URL: myapp://post/123
// Will automatically navigate to PostDetailPage with postId = "123"
```

### 3. Custom Transitions

```dart
GoRoute(
  path: '/profile',
  name: 'profile',
  pageBuilder: (context, state) {
    return CustomTransitionPage(
      child: const ProfilePage(),
      transitionsBuilder: (context, animation, secondaryAnimation, child) {
        return FadeTransition(
          opacity: animation,
          child: child,
        );
      },
    );
  },
),
```

### 4. Dialog and Bottom Sheet Routes

```dart
GoRoute(
  path: '/user-settings',
  name: 'userSettings',
  pageBuilder: (context, state) {
    return DialogPage(
      builder: (context) => const UserSettingsDialog(),
    );
  },
),

// Usage
context.goNamed('userSettings');
```

### 5. Route Guards (Role-based)

```dart
GoRoute(
  path: '/admin',
  name: 'admin',
  builder: (context, state) => const AdminPage(),
  redirect: (context, state) {
    final user = context.read<AuthBloc>().state.user;
    if (user?.role != 'admin') {
      return '/unauthorized';
    }
    return null;
  },
),
```

## Best Practices

### 1. Route Constants

Always use constants for route paths:

```dart
class Routes {
  static const home = '/home';
  static const profile = '/profile';
  // ... more routes
  
  Routes._(); // Private constructor to prevent instantiation
}
```

### 2. Type-Safe Navigation

Use named routes with type-safe parameters:

```dart
// Define extension for type-safe navigation
extension RouterExtension on BuildContext {
  void goToProfile(String userId) {
    goNamed('userProfile', pathParameters: {'userId': userId});
  }
  
  void goToSearch(String query, {String filter = 'all'}) {
    goNamed('search', queryParameters: {
      'q': query,
      'filter': filter,
    });
  }
}

// Usage
context.goToProfile('123');
context.goToSearch('flutter', filter: 'recent');
```

### 3. Navigation State Management

```dart
class NavigationBloc extends Bloc<NavigationEvent, NavigationState> {
  final GoRouter router;
  
  NavigationBloc(this.router) : super(NavigationInitial()) {
    on<NavigateToHome>((event, emit) {
      router.goNamed('home');
    });
    
    on<NavigateToProfile>((event, emit) {
      router.goNamed('userProfile', 
        pathParameters: {'userId': event.userId}
      );
    });
  }
}
```

### 4. Error Handling

```dart
final appRouter = GoRouter(
  routes: [...],
  errorBuilder: (context, state) {
    return ErrorPage(
      error: state.error,
      onRetry: () => context.go('/home'),
    );
  },
);
```

### 5. Logging Navigation

```dart
final appRouter = GoRouter(
  debugLogDiagnostics: true,
  routes: [...],
  observers: [
    NavigationLogger(),
  ],
);

class NavigationLogger extends NavigatorObserver {
  @override
  void didPush(Route route, Route? previousRoute) {
    debugPrint('Navigated to: ${route.settings.name}');
  }
  
  @override
  void didPop(Route route, Route? previousRoute) {
    debugPrint('Popped from: ${route.settings.name}');
  }
}
```

### 6. Prevent Back Navigation

```dart
class HomePage extends StatelessWidget {
  const HomePage({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return WillPopScope(
      onWillPop: () async {
        // Prevent back navigation
        return false;
      },
      child: Scaffold(
        appBar: AppBar(
          automaticallyImplyLeading: false, // Remove back button
        ),
        body: const HomeContent(),
      ),
    );
  }
}
```

## Common Patterns

### Tab Navigation

```dart
class HomePageWithTabs extends StatelessWidget {
  final int currentTab;
  
  const HomePageWithTabs({Key? key, required this.currentTab}) 
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: IndexedStack(
        index: currentTab,
        children: const [
          FeedTab(),
          ExploreTab(),
          NotificationsTab(),
          ProfileTab(),
        ],
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: currentTab,
        onTap: (index) {
          context.go('/home/tab/$index');
        },
        items: const [...],
      ),
    );
  }
}

// Route configuration
GoRoute(
  path: '/home/tab/:tab',
  builder: (context, state) {
    final tab = int.parse(state.pathParameters['tab'] ?? '0');
    return HomePageWithTabs(currentTab: tab);
  },
),
```

### Modal Navigation

```dart
// Show modal
Future<void> showUserModal(BuildContext context, String userId) async {
  final result = await showModalBottomSheet<String>(
    context: context,
    builder: (context) => UserModal(userId: userId),
  );
  
  if (result != null) {
    // Handle result
  }
}
```

### Conditional Routes

```dart
GoRoute(
  path: '/dashboard',
  name: 'dashboard',
  builder: (context, state) {
    final userRole = context.read<AuthBloc>().state.user?.role;
    
    switch (userRole) {
      case 'admin':
        return const AdminDashboard();
      case 'user':
        return const UserDashboard();
      default:
        return const GuestDashboard();
    }
  },
),
```

## Testing

### Unit Testing Routes

```dart
void main() {
  test('navigates to correct route', () {
    final router = GoRouter(routes: [...]);
    
    router.go('/home');
    expect(router.location, '/home');
    
    router.go('/profile/123');
    expect(router.location, '/profile/123');
  });
}
```

### Widget Testing with Navigation

```dart
testWidgets('navigates on button tap', (tester) async {
  final router = GoRouter(
    routes: [
      GoRoute(
        path: '/',
        builder: (context, state) => HomePage(),
      ),
      GoRoute(
        path: '/profile',
        builder: (context, state) => ProfilePage(),
      ),
    ],
  );
  
  await tester.pumpWidget(
    MaterialApp.router(routerConfig: router),
  );
  
  await tester.tap(find.text('Go to Profile'));
  await tester.pumpAndSettle();
  
  expect(find.byType(ProfilePage), findsOneWidget);
});
```

## Troubleshooting

### Common Issues

1. **Route not found**: Check path spelling and parameters
2. **State not rebuilding**: Ensure proper use of `refreshListenable`
3. **Back button not working**: Check `WillPopScope` usage
4. **Deep link not working**: Verify path parameters match

### Debugging

```dart
final appRouter = GoRouter(
  debugLogDiagnostics: true, // Enable detailed logging
  routes: [...],
);
```

## Migration from Navigator 1.0

```dart
// Old Navigator 1.0
Navigator.of(context).push(
  MaterialPageRoute(builder: (context) => ProfilePage()),
);

// New GoRouter
context.push('/profile');

// Or with named route
context.goNamed('profile');
```

## Resources

- [go_router documentation](https://pub.dev/packages/go_router)
- [Flutter Navigation 2.0](https://docs.flutter.dev/development/ui/navigation)
- [Deep Linking Guide](https://docs.flutter.dev/development/ui/navigation/deep-linking)
