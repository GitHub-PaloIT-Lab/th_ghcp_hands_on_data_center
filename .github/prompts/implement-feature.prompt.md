# Feature Implementation Prompt

## Context
You are implementing a complete feature for a Flutter Clean Architecture project. This prompt guides you through the systematic implementation of a feature from domain to presentation layer.

## Rules
- ตอบเป็นภาษาไทยเท่านั้น
- ขอรีวิวก่อนลงมือทำทุกครั้ง

## Required Reading & Reference Materials

Before starting implementation, review these essential instruction files:

### Project Setup Instructions
- `.github/instructions/README.md` - Project overview and architecture guidelines
- `.github/instructions/flutter_clean_architecture_guide.md` - Clean Architecture principles and patterns
- `.github/instructions/flutter_bloc_guide.md` - BLoC state management implementation
- `.github/instructions/flutter_routing_guide.md` - Navigation and routing setup

### Implementation Guides
- `.github/prompts/domain_entity.md` - Domain entity creation guidelines
- `.github/prompts/repository_interface.md` - Repository contract definition
- `.github/prompts/use_case.md` - Use case implementation patterns
- `.github/prompts/data_model.md` - Data model and JSON serialization
- `.github/prompts/bloc_state_management.md` - BLoC pattern implementation

### Feature-Specific Instructions
- `02 Implementation task/TODO_APP_GUIDE.md` - Feature requirements and user stories
- Any feature-specific documentation in the project

### External Documentation
Refer to source repository for complete guides:
- **GitHub-PaloIT-Lab/th_ghcp_hands_on_data_center** - Complete implementation examples and best practices

## Pre-Implementation Checklist
Before writing any code, ensure you have:
- [ ] Read all relevant instruction files listed above
- [ ] Understood the feature requirements and acceptance criteria
- [ ] Reviewed existing code structure and patterns
- [ ] Identified reusable components and patterns
- [ ] Planned the implementation approach following Clean Architecture

## Implementation Workflow

### Phase 1: Domain Layer (Start Here)
Follow this order to maintain clean architecture principles:

#### Step 1: Define Domain Entity
- Location: `lib/features/{FEATURE_NAME}/domain/entities/{ENTITY_NAME}.dart`
- Requirements: Immutable, extends Equatable, business validation
- Dependencies: Only core domain concepts
- Output: Core business object with rules and behaviors

#### Step 2: Create Repository Interface
- Location: `lib/features/{FEATURE_NAME}/domain/repositories/{REPOSITORY_NAME}.dart`
- Requirements: Abstract class, Either return types, domain-focused
- Dependencies: Domain entities and core failures
- Output: Contract for data access operations

#### Step 3: Implement Use Cases
- Location: `lib/features/{FEATURE_NAME}/domain/usecases/{USE_CASE_NAME}.dart`
- Requirements: Single responsibility, repository injection, error handling
- Dependencies: Repository interface, domain entities
- Output: Business logic operations with proper error handling

### Phase 2: Data Layer
Implement data layer after domain contracts are defined:

#### Step 4: Create Data Models
- Location: `lib/features/{FEATURE_NAME}/data/models/{MODEL_NAME}.dart`
- Requirements: JSON serialization, entity mapping, validation
- Dependencies: Domain entities, JSON annotations
- Output: Data transfer objects with serialization

#### Step 5: Define Data Sources
- Location: `lib/features/{FEATURE_NAME}/data/datasources/{DATA_SOURCE_NAME}.dart`
- Requirements: Interface + implementation, external service integration
- Dependencies: Data models, HTTP client, local storage
- Output: External data access implementations

#### Step 6: Implement Repository
- Location: `lib/features/{FEATURE_NAME}/data/repositories/{REPOSITORY_NAME}_impl.dart`
- Requirements: Implements domain interface, error mapping, caching
- Dependencies: Data sources, models, mappers
- Output: Complete data access implementation

### Phase 3: Presentation Layer
Build UI after business logic is complete:

#### Step 7: Create BLoC State Management
- Location: `lib/features/{FEATURE_NAME}/presentation/bloc/{BLOC_NAME}_bloc.dart`
- Requirements: Events, states, business logic coordination
- Dependencies: Use cases, domain entities
- Output: State management for UI interactions

#### Step 8: Build UI Pages
- Location: `lib/features/{FEATURE_NAME}/presentation/pages/{PAGE_NAME}_page.dart`
- Requirements: Responsive design, BLoC integration, navigation
- Dependencies: BLoC, widgets, routing
- Output: Complete user interface screens

#### Step 9: Create UI Widgets
- Location: `lib/features/{FEATURE_NAME}/presentation/widgets/{WIDGET_NAME}_widget.dart`
- Requirements: Reusable components, proper state handling
- Dependencies: Domain entities, theme configuration
- Output: Modular UI components

### Phase 4: Integration & Testing
Complete the feature with proper testing:

#### Step 10: Dependency Injection Setup
- Location: `lib/injection_container.dart` or service locator
- Requirements: Register all dependencies, proper scoping
- Dependencies: All implementations and interfaces
- Output: Configured dependency injection

#### Step 11: Navigation Integration
- Location: Update routing configuration
- Requirements: Route definitions, parameter passing, navigation flow
- Dependencies: Pages, routing package
- Output: Integrated navigation system

#### Step 12: Testing Implementation
- Locations: `test/` directory with same structure
- Requirements: Unit tests for all layers, widget tests, integration tests
- Dependencies: Test frameworks, mocking libraries
- Output: Comprehensive test coverage

## Implementation Guidelines

### Before You Start
1. **Read the feature requirements** in `02 Implementation task/TODO_APP_GUIDE.md` or relevant feature documentation
2. **Review existing code patterns** in the project to maintain consistency
3. **Check project instructions** in `.github/instructions/` for architecture guidelines and best practices
4. **Use appropriate prompt templates** from `.github/prompts/` for each implementation step

### Clean Architecture Principles
- **Dependency Rule**: Dependencies point inward (presentation → domain ← data)
- **Interface Segregation**: Small, focused interfaces for each concern
- **Single Responsibility**: Each class has one reason to change
- **Dependency Inversion**: Depend on abstractions, not concretions
- **Reference**: See `.github/instructions/flutter_clean_architecture_guide.md` for detailed principles

### Error Handling Strategy
- Domain failures for business rule violations
- Repository failures for data access issues
- Network failures for connectivity problems
- Validation failures for input validation
- Proper error propagation through all layers

### State Management Pattern
- BLoC for complex state and business logic
- Events represent user actions and external triggers
- States represent UI states and data states
- Proper loading, success, and error state handling

### Testing Strategy
- Unit tests for use cases and business logic
- Repository tests with mocked data sources
- BLoC tests for state management
- Widget tests for UI components
- Integration tests for complete user flows

## Acceptance Criteria Template

### Domain Layer
- [ ] Entity implements business rules and validation
- [ ] Repository interface defines clear contracts
- [ ] Use cases handle single business operations
- [ ] Proper error types and handling
- [ ] No external dependencies in domain layer

### Data Layer
- [ ] Models handle JSON serialization correctly
- [ ] Data sources integrate with external services
- [ ] Repository implementation follows interface
- [ ] Proper error mapping from data to domain
- [ ] Caching strategy implemented where needed

### Presentation Layer
- [ ] BLoC manages UI state effectively
- [ ] Pages integrate with BLoC properly
- [ ] Widgets are reusable and testable
- [ ] Proper loading and error state handling
- [ ] Responsive design implementation

### Integration
- [ ] Dependency injection configured correctly
- [ ] Navigation flows work as expected
- [ ] Feature integrates with existing app structure
- [ ] Performance requirements met
- [ ] Accessibility guidelines followed

## Feature Completion Checklist

### Code Quality
- [ ] All files follow project naming conventions
- [ ] Proper documentation and comments added
- [ ] Code follows Dart/Flutter style guidelines
- [ ] No unused imports or dead code
- [ ] Proper error handling throughout

### Functionality
- [ ] All user stories/requirements implemented
- [ ] Edge cases handled appropriately
- [ ] Validation rules enforced
- [ ] Performance optimized
- [ ] Security considerations addressed

### Testing
- [ ] Unit test coverage > 80%
- [ ] Widget tests for all custom widgets
- [ ] Integration tests for critical flows
- [ ] BLoC tests cover all events and states
- [ ] Repository tests with mocked dependencies

### Documentation
- [ ] README updated with feature information
- [ ] API documentation generated
- [ ] Architecture decision records created
- [ ] User guide updated if needed
- [ ] Code comments explain complex logic

## Using This Prompt with GitHub Copilot

### Effective Prompt Usage
1. **Copy the relevant section** from this prompt that matches your current implementation step
2. **Customize placeholder variables** with your specific feature details:
   - Replace `{FEATURE_NAME}` with your actual feature name (e.g., "todo")
   - Replace `{ENTITY_NAME}` with your domain entity name (e.g., "Todo")
   - Replace other placeholders as needed
3. **Reference specific instruction files** mentioned in each step for detailed guidance
4. **Paste the customized prompt** into your chat with GitHub Copilot along with your specific requirements

### Example Copilot Interaction
```
I need to implement Step 1 from the feature implementation guide.

Feature: Todo Management
Entity: Todo
Requirements: 
- Todo should have id, title, description, isCompleted, createdAt, dueDate properties
- Business validation for required fields
- Methods to mark as complete/incomplete

Please follow the domain entity guidelines in .github/prompts/domain_entity.md and create the Todo entity for lib/features/todo/domain/entities/todo.dart
```

### Best Practices with Copilot
- **Be specific** about your requirements and constraints
- **Reference instruction files** for consistent patterns and standards
- **Ask for incremental implementation** following the step-by-step workflow
- **Request explanations** when you need to understand the generated code
- **Iterate and refine** based on your specific needs and project requirements

## Next Steps After Implementation
1. Code review with team members
2. QA testing and bug fixes
3. Performance testing and optimization
4. Documentation review and updates
5. Deployment preparation and rollout planning

## Architecture Overview
```
lib/
├── core/
│   ├── error/
│   ├── constants/
│   └── utils/
├── features/
│   └── {FEATURE_NAME}/
│       ├── domain/
│       │   ├── entities/
│       │   ├── repositories/
│       │   └── usecases/
│       ├── data/
│       │   ├── models/
│       │   ├── datasources/
│       │   └── repositories/
│       └── presentation/
│           ├── bloc/
│           ├── pages/
│           └── widgets/
```