# Flutter API and Mock Data Guide

## Overview

This project uses **Dio** for HTTP networking with a comprehensive mocking strategy for development and testing. All API calls are mocked to enable development without backend dependencies.

## Setup

### Dependencies

```yaml
dependencies:
  dio: ^5.4.0
  pretty_dio_logger: ^1.3.1  # For logging
  
dev_dependencies:
  mockito: ^5.4.4
  build_runner: ^2.4.7
```

## Directory Structure

```
lib/
└── core/
    └── network/
        ├── api_client.dart           # Dio client configuration
        ├── mock_api_client.dart      # Mock implementation
        ├── interceptors/
        │   ├── auth_interceptor.dart
        │   ├── mock_interceptor.dart
        │   └── logging_interceptor.dart
        └── mock_data/
            ├── user_mock_data.dart
            ├── product_mock_data.dart
            └── ...
```

## API Client Implementation

### 1. Base API Client

```dart
// core/network/api_client.dart
import 'package:dio/dio.dart';
import 'package:pretty_dio_logger/pretty_dio_logger.dart';

class ApiClient {
  late final Dio _dio;
  
  static const String baseUrl = 'https://api.example.com';
  static const Duration timeout = Duration(seconds: 30);
  
  ApiClient() {
    _dio = Dio(
      BaseOptions(
        baseUrl: baseUrl,
        connectTimeout: timeout,
        receiveTimeout: timeout,
        sendTimeout: timeout,
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json',
        },
      ),
    );
    
    _setupInterceptors();
  }
  
  void _setupInterceptors() {
    _dio.interceptors.addAll([
      PrettyDioLogger(
        requestHeader: true,
        requestBody: true,
        responseBody: true,
        responseHeader: false,
        error: true,
        compact: true,
      ),
    ]);
  }
  
  Dio get dio => _dio;
  
  // GET request
  Future<Response> get(
    String path, {
    Map<String, dynamic>? queryParameters,
    Options? options,
  }) async {
    try {
      return await _dio.get(
        path,
        queryParameters: queryParameters,
        options: options,
      );
    } on DioException catch (e) {
      throw _handleError(e);
    }
  }
  
  // POST request
  Future<Response> post(
    String path, {
    dynamic data,
    Map<String, dynamic>? queryParameters,
    Options? options,
  }) async {
    try {
      return await _dio.post(
        path,
        data: data,
        queryParameters: queryParameters,
        options: options,
      );
    } on DioException catch (e) {
      throw _handleError(e);
    }
  }
  
  // PUT request
  Future<Response> put(
    String path, {
    dynamic data,
    Map<String, dynamic>? queryParameters,
    Options? options,
  }) async {
    try {
      return await _dio.put(
        path,
        data: data,
        queryParameters: queryParameters,
        options: options,
      );
    } on DioException catch (e) {
      throw _handleError(e);
    }
  }
  
  // DELETE request
  Future<Response> delete(
    String path, {
    dynamic data,
    Map<String, dynamic>? queryParameters,
    Options? options,
  }) async {
    try {
      return await _dio.delete(
        path,
        data: data,
        queryParameters: queryParameters,
        options: options,
      );
    } on DioException catch (e) {
      throw _handleError(e);
    }
  }
  
  Exception _handleError(DioException error) {
    switch (error.type) {
      case DioExceptionType.connectionTimeout:
      case DioExceptionType.sendTimeout:
      case DioExceptionType.receiveTimeout:
        return NetworkException('Connection timeout');
      
      case DioExceptionType.badResponse:
        return _handleHttpError(error.response?.statusCode);
      
      case DioExceptionType.cancel:
        return NetworkException('Request cancelled');
      
      default:
        return NetworkException('Network error occurred');
    }
  }
  
  Exception _handleHttpError(int? statusCode) {
    switch (statusCode) {
      case 400:
        return BadRequestException('Bad request');
      case 401:
        return UnauthorizedException('Unauthorized');
      case 403:
        return ForbiddenException('Forbidden');
      case 404:
        return NotFoundException('Not found');
      case 500:
        return ServerException('Internal server error');
      default:
        return ServerException('Server error');
    }
  }
}

// Custom exceptions
class NetworkException implements Exception {
  final String message;
  NetworkException(this.message);
}

class BadRequestException implements Exception {
  final String message;
  BadRequestException(this.message);
}

class UnauthorizedException implements Exception {
  final String message;
  UnauthorizedException(this.message);
}

class ForbiddenException implements Exception {
  final String message;
  ForbiddenException(this.message);
}

class NotFoundException implements Exception {
  final String message;
  NotFoundException(this.message);
}

class ServerException implements Exception {
  final String message;
  ServerException(this.message);
}
```

### 2. Mock Interceptor

```dart
// core/network/interceptors/mock_interceptor.dart
import 'package:dio/dio.dart';
import '../mock_data/user_mock_data.dart';

class MockInterceptor extends Interceptor {
  final Duration delay;
  
  MockInterceptor({this.delay = const Duration(milliseconds: 500)});
  
  @override
  void onRequest(
    RequestOptions options,
    RequestInterceptorHandler handler,
  ) async {
    // Simulate network delay
    await Future.delayed(delay);
    
    // Check if this is a mock request
    final response = _getMockResponse(options);
    
    if (response != null) {
      return handler.resolve(response);
    }
    
    return handler.next(options);
  }
  
  Response? _getMockResponse(RequestOptions options) {
    final path = options.path;
    final method = options.method;
    
    // User endpoints
    if (path.startsWith('/users') && method == 'GET') {
      if (path.contains('/users/')) {
        final userId = path.split('/').last;
        return _createResponse(
          options,
          UserMockData.getUserById(userId),
        );
      }
      return _createResponse(options, UserMockData.getAllUsers());
    }
    
    if (path == '/users' && method == 'POST') {
      return _createResponse(
        options,
        UserMockData.createUser(options.data),
        statusCode: 201,
      );
    }
    
    // Auth endpoints
    if (path == '/auth/login' && method == 'POST') {
      return _createResponse(
        options,
        {
          'token': 'mock_token_${DateTime.now().millisecondsSinceEpoch}',
          'user': UserMockData.getCurrentUser(),
        },
      );
    }
    
    return null;
  }
  
  Response _createResponse(
    RequestOptions options,
    dynamic data, {
    int statusCode = 200,
  }) {
    return Response(
      requestOptions: options,
      data: data,
      statusCode: statusCode,
      headers: Headers.fromMap({
        'content-type': ['application/json'],
      }),
    );
  }
}
```

### 3. Mock API Client

```dart
// core/network/mock_api_client.dart
import 'package:dio/dio.dart';
import 'api_client.dart';
import 'interceptors/mock_interceptor.dart';

class MockApiClient extends ApiClient {
  MockApiClient() : super() {
    // Add mock interceptor first
    dio.interceptors.insert(0, MockInterceptor());
  }
}
```

## Mock Data Structure

### 1. User Mock Data

```dart
// core/network/mock_data/user_mock_data.dart
class UserMockData {
  static final List<Map<String, dynamic>> _users = [
    {
      'id': '1',
      'name': 'John Doe',
      'email': 'john@example.com',
      'avatar': 'https://i.pravatar.cc/150?img=1',
      'role': 'user',
      'createdAt': '2024-01-01T00:00:00Z',
    },
    {
      'id': '2',
      'name': 'Jane Smith',
      'email': 'jane@example.com',
      'avatar': 'https://i.pravatar.cc/150?img=2',
      'role': 'admin',
      'createdAt': '2024-01-02T00:00:00Z',
    },
    {
      'id': '3',
      'name': 'สมชาย ใจดี',
      'email': 'somchai@example.com',
      'avatar': 'https://i.pravatar.cc/150?img=3',
      'role': 'user',
      'createdAt': '2024-01-03T00:00:00Z',
    },
  ];
  
  static Map<String, dynamic> getAllUsers() {
    return {
      'data': _users,
      'total': _users.length,
      'page': 1,
      'pageSize': 10,
    };
  }
  
  static Map<String, dynamic>? getUserById(String id) {
    try {
      final user = _users.firstWhere((u) => u['id'] == id);
      return {'data': user};
    } catch (e) {
      return null;
    }
  }
  
  static Map<String, dynamic> getCurrentUser() {
    return _users[0];
  }
  
  static Map<String, dynamic> createUser(Map<String, dynamic> data) {
    final newUser = {
      'id': '${_users.length + 1}',
      ...data,
      'createdAt': DateTime.now().toIso8601String(),
    };
    _users.add(newUser);
    return {'data': newUser};
  }
  
  static Map<String, dynamic> updateUser(String id, Map<String, dynamic> data) {
    final index = _users.indexWhere((u) => u['id'] == id);
    if (index != -1) {
      _users[index] = {..._users[index], ...data};
      return {'data': _users[index]};
    }
    return {'error': 'User not found'};
  }
  
  static bool deleteUser(String id) {
    final index = _users.indexWhere((u) => u['id'] == id);
    if (index != -1) {
      _users.removeAt(index);
      return true;
    }
    return false;
  }
}
```

### 2. Product Mock Data

```dart
// core/network/mock_data/product_mock_data.dart
class ProductMockData {
  static final List<Map<String, dynamic>> _products = [
    {
      'id': '1',
      'name': 'Product 1',
      'description': 'This is product 1',
      'price': 99.99,
      'currency': 'USD',
      'imageUrl': 'https://picsum.photos/seed/product1/400/400',
      'category': 'Electronics',
      'stock': 10,
    },
    {
      'id': '2',
      'name': 'สินค้า 2',
      'description': 'นี่คือสินค้าที่ 2',
      'price': 1500.00,
      'currency': 'THB',
      'imageUrl': 'https://picsum.photos/seed/product2/400/400',
      'category': 'Fashion',
      'stock': 5,
    },
  ];
  
  static Map<String, dynamic> getAllProducts({
    int page = 1,
    int pageSize = 10,
    String? category,
  }) {
    var filteredProducts = _products;
    
    if (category != null && category.isNotEmpty) {
      filteredProducts = _products
          .where((p) => p['category'] == category)
          .toList();
    }
    
    final startIndex = (page - 1) * pageSize;
    final endIndex = startIndex + pageSize;
    final paginatedProducts = filteredProducts.sublist(
      startIndex,
      endIndex > filteredProducts.length ? filteredProducts.length : endIndex,
    );
    
    return {
      'data': paginatedProducts,
      'total': filteredProducts.length,
      'page': page,
      'pageSize': pageSize,
    };
  }
  
  static Map<String, dynamic>? getProductById(String id) {
    try {
      final product = _products.firstWhere((p) => p['id'] == id);
      return {'data': product};
    } catch (e) {
      return null;
    }
  }
}
```

## Data Source Implementation

### Remote Data Source with Mocks

```dart
// features/user/data/datasources/user_remote_datasource.dart
abstract class UserRemoteDataSource {
  Future<UserModel> getUser(String id);
  Future<List<UserModel>> getUsers();
  Future<UserModel> createUser(UserModel user);
  Future<UserModel> updateUser(String id, UserModel user);
  Future<void> deleteUser(String id);
}

class UserRemoteDataSourceImpl implements UserRemoteDataSource {
  final ApiClient apiClient;
  
  UserRemoteDataSourceImpl({required this.apiClient});
  
  @override
  Future<UserModel> getUser(String id) async {
    try {
      final response = await apiClient.get('/users/$id');
      return UserModel.fromJson(response.data['data']);
    } catch (e) {
      throw ServerException('Failed to get user');
    }
  }
  
  @override
  Future<List<UserModel>> getUsers() async {
    try {
      final response = await apiClient.get('/users');
      final List<dynamic> data = response.data['data'];
      return data.map((json) => UserModel.fromJson(json)).toList();
    } catch (e) {
      throw ServerException('Failed to get users');
    }
  }
  
  @override
  Future<UserModel> createUser(UserModel user) async {
    try {
      final response = await apiClient.post(
        '/users',
        data: user.toJson(),
      );
      return UserModel.fromJson(response.data['data']);
    } catch (e) {
      throw ServerException('Failed to create user');
    }
  }
  
  @override
  Future<UserModel> updateUser(String id, UserModel user) async {
    try {
      final response = await apiClient.put(
        '/users/$id',
        data: user.toJson(),
      );
      return UserModel.fromJson(response.data['data']);
    } catch (e) {
      throw ServerException('Failed to update user');
    }
  }
  
  @override
  Future<void> deleteUser(String id) async {
    try {
      await apiClient.delete('/users/$id');
    } catch (e) {
      throw ServerException('Failed to delete user');
    }
  }
}
```

## Configuration

### Environment-based API Client

```dart
// core/config/app_config.dart
enum Environment { development, staging, production }

class AppConfig {
  static Environment environment = Environment.development;
  
  static bool get useMockApi => environment == Environment.development;
  
  static ApiClient createApiClient() {
    if (useMockApi) {
      return MockApiClient();
    }
    return ApiClient();
  }
}

// In main.dart
void main() {
  AppConfig.environment = Environment.development;
  runApp(const MyApp());
}
```

## Best Practices

### 1. Realistic Mock Data

- Use realistic data that matches production structure
- Include edge cases (empty lists, null values)
- Use Thai and English text for i18n testing
- Include various data types and formats

### 2. Mock Response Delays

Simulate real network latency:

```dart
MockInterceptor(
  delay: const Duration(milliseconds: 500), // Realistic delay
);
```

### 3. Error Scenarios

Mock different error responses:

```dart
Response? _getMockResponse(RequestOptions options) {
  // Simulate 404 for specific ID
  if (options.path == '/users/999') {
    return _createErrorResponse(options, 404, 'User not found');
  }
  
  // Simulate 500 error randomly (10% chance)
  if (Random().nextInt(10) == 0) {
    return _createErrorResponse(options, 500, 'Server error');
  }
  
  return null;
}

Response _createErrorResponse(
  RequestOptions options,
  int statusCode,
  String message,
) {
  return Response(
    requestOptions: options,
    statusCode: statusCode,
    data: {'error': message},
  );
}
```

### 4. Pagination Support

```dart
static Map<String, dynamic> getUsers({
  int page = 1,
  int pageSize = 10,
}) {
  final startIndex = (page - 1) * pageSize;
  final endIndex = startIndex + pageSize;
  final paginatedUsers = _users.sublist(
    startIndex,
    endIndex > _users.length ? _users.length : endIndex,
  );
  
  return {
    'data': paginatedUsers,
    'pagination': {
      'page': page,
      'pageSize': pageSize,
      'total': _users.length,
      'totalPages': (_users.length / pageSize).ceil(),
    },
  };
}
```

### 5. Search and Filter

```dart
static Map<String, dynamic> searchUsers(String query) {
  final results = _users.where((user) {
    final name = user['name'].toString().toLowerCase();
    final email = user['email'].toString().toLowerCase();
    final searchQuery = query.toLowerCase();
    return name.contains(searchQuery) || email.contains(searchQuery);
  }).toList();
  
  return {
    'data': results,
    'total': results.length,
    'query': query,
  };
}
```

### 6. State Persistence

```dart
class CartMockData {
  static final List<Map<String, dynamic>> _cart = [];
  
  static Map<String, dynamic> addToCart(Map<String, dynamic> item) {
    _cart.add({
      'id': '${_cart.length + 1}',
      ...item,
      'addedAt': DateTime.now().toIso8601String(),
    });
    return {'data': _cart.last};
  }
  
  static List<Map<String, dynamic>> getCart() {
    return _cart;
  }
  
  static void clearCart() {
    _cart.clear();
  }
}
```

## Testing with Mocks

### Unit Testing

```dart
void main() {
  late UserRemoteDataSource dataSource;
  late MockApiClient mockApiClient;
  
  setUp(() {
    mockApiClient = MockApiClient();
    dataSource = UserRemoteDataSourceImpl(apiClient: mockApiClient);
  });
  
  test('should return user when getUser is called', () async {
    // Arrange
    const userId = '1';
    
    // Act
    final result = await dataSource.getUser(userId);
    
    // Assert
    expect(result, isA<UserModel>());
    expect(result.id, userId);
  });
}
```

## Common Patterns

### Retry Logic

```dart
Future<Response> getWithRetry(String path, {int maxRetries = 3}) async {
  int attempts = 0;
  
  while (attempts < maxRetries) {
    try {
      return await apiClient.get(path);
    } catch (e) {
      attempts++;
      if (attempts >= maxRetries) rethrow;
      await Future.delayed(Duration(seconds: attempts));
    }
  }
  
  throw Exception('Max retries reached');
}
```

### Request Cancellation

```dart
final cancelToken = CancelToken();

// Make request
apiClient.get('/users', options: Options(cancelToken: cancelToken));

// Cancel request
cancelToken.cancel('Request cancelled by user');
```

### File Upload Mock

```dart
static Future<Map<String, dynamic>> uploadFile(String path) async {
  await Future.delayed(const Duration(seconds: 2));
  return {
    'url': 'https://example.com/files/mock_${DateTime.now().millisecondsSinceEpoch}.jpg',
    'size': 1024000,
    'uploadedAt': DateTime.now().toIso8601String(),
  };
}
```

## Resources

- [Dio documentation](https://pub.dev/packages/dio)
- [Mockito documentation](https://pub.dev/packages/mockito)
- [REST API best practices](https://restfulapi.net/)
