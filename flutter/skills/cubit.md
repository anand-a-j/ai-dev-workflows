# Flutter Cubit Skill

## Purpose

Generate lightweight, reusable global or shared state management using **Cubit**.

Cubit is responsible for managing application state without an event-driven workflow.

---

## Responsibilities

Generate:

```text
feature/
└── cubit/
    └── feature_cubit.dart
```

---

## State Guidelines

Prefer a single immutable state.

Use `copyWith()` for updates.

Examples:

- CartState
- HomeState
- SessionState
- ThemeState
- NavigationState

Avoid creating loading/success/failure subclasses unless absolutely necessary.

---

## Constructor Rules

Always inject dependencies through the Cubit constructor.

Never instantiate repositories or services inside the Cubit.

Example:

```dart
class CartCubit extends Cubit<CartState> {
  CartCubit({
    required CartRepository cartRepository,
  }) : _cartRepository = cartRepository,
       super(const CartState());

  final CartRepository _cartRepository;
}
```

Always register and provide the Cubit instance using dependency injection.

---

## Use Cubit For

Examples:

- Shopping Cart
- Bottom Navigation
- Theme
- User Session
- Language
- Favorites
- App Settings
- Connectivity
- Notification Badge

---

## Cubit Responsibilities

Cubit should manage lightweight state updates such as:

- Add item
- Remove item
- Update quantity
- Toggle favorite
- Change selected tab
- Update filters
- Reset state

Expose helper getters when they simplify UI.

Example:

```dart
bool get hasItems => state.items.isNotEmpty;

int get totalItems => state.items.length;
```

---

## Do NOT Use Cubit For

Do not use Cubit for:

- Authentication workflow
- Payment flow
- Multi-step forms
- OTP verification
- Order placement lifecycle
- Long-running API workflows

These belong in Bloc.

---

## Best Practices

- Always use immutable state.
- Keep methods small and focused.
- Prefer model + copyWith().
- Avoid unnecessary emits.
- Preserve existing state whenever possible.
- Expose computed getters when useful.
- Always inject dependencies through the constructor.
- Keep Cubits reusable.

---
