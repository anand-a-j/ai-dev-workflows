# Flutter Bloc Skill

## Purpose

Generate clean, scalable feature-specific state management using **flutter_bloc** and **Equatable**.

Bloc is responsible for handling business logic, asynchronous operations, repository communication, and UI state transitions.

It must not contain UI code or data layer implementation.

---

## Responsibilities

Generate:

```text
feature/
└── bloc/
    ├── feature_bloc.dart
    ├── feature_event.dart
    └── feature_state.dart
```

---

## State Guidelines

Always use **Equatable**.

Choose the state structure based on the feature complexity.

### Prefer Multiple States

Use multiple state classes whenever the feature has clear workflow transitions.

Examples:

- Initial
- Loading
- Success
- Failure
- Empty
- Refreshing

Example:

```dart
LoginInitial
LoginLoading
LoginSuccess
LoginFailure
```

---

### Single State

Use a single immutable state with `copyWith()` only when the screen continuously edits or manages data.

Examples:

- Checkout
- Payment
- Edit Profile
- Cart Summary
- Filters

Avoid creating many subclasses when a single immutable state is sufficient.

---

## Event Guidelines

Create events only for user actions or business triggers.

Examples:

- LoadData
- RefreshData
- SubmitForm
- DeleteItem
- VerifyOtp

Do not create events for simple local UI changes that belong in Cubit.

---

## Constructor Rules

Always inject dependencies through the Bloc constructor.

Never instantiate repositories, services, or use cases inside the Bloc.

Example:

```dart
class LoginBloc extends Bloc<LoginEvent, LoginState> {
  LoginBloc({
    required AuthRepository authRepository,
  }) : _authRepository = authRepository,
       super(LoginInitial());

  final AuthRepository _authRepository;
}
```

Always register and provide the Bloc instance using dependency injection.

---

## Responsibilities

Bloc may:

- Call repositories
- Execute use cases
- Handle API requests
- Handle pagination
- Emit loading/success/failure states
- Transform business logic
- Handle retry logic

---

## Do NOT Use Bloc For

Do not use Bloc for:

- Bottom navigation
- Theme mode
- Cart cache
- User session storage
- Selected tab
- Toggle values
- Temporary UI state

These belong in Cubit.

---

## Best Practices

- Always use Equatable.
- Keep events focused.
- Keep states immutable.
- Prefer multiple states for async workflows.
- Use a single state only for continuous editable UI.
- Never call APIs directly.
- Always delegate data access to repositories.
- Always inject dependencies through the constructor.
- Keep Bloc focused only on business logic.

---