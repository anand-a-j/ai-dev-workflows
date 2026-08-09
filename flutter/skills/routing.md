# GoRouter Skill

## Purpose

Generate a clean, scalable routing foundation using `go_router`.

The routing layer is responsible for navigation, route registration, redirects, deep linking support, and navigation observers.

It must not contain business logic.

---

## Responsibilities

Generate routing infrastructure including:

- app_router.dart
- route_paths.dart
- route_names.dart (optional)

---

## Folder Structure

```
lib/
└── routes/
    ├── app_router.dart
    ├── route_paths.dart
    └── route_names.dart (optional)
```

---

## Router

Use `GoRouter` as the application's navigation solution.

Configure when required:

- initialLocation
- routes
- redirect
- observers
- navigatorKey
- errorBuilder or errorPageBuilder
- debugLogDiagnostics (development only)

Prefer a single centralized router.

---

## Route Definitions

Keep route definitions clean and readable.

Each route should contain only navigation configuration.

Examples:

- path
- name
- builder
- pageBuilder
- routes (nested routes)

Avoid writing application logic inside route definitions.

---

## Route Paths

Store reusable route paths inside `route_paths.dart`.

Example:

```dart
class RoutePaths {
  static const splash = "/";
  static const onboarding = "/onboarding";
  static const dashboard = "/dashboard";
  static const settings = "/settings";
}
```

Never hardcode route strings throughout the application.

Always reference `RoutePaths`.

---

## Route Names

If named navigation is used, generate a centralized `route_names.dart`.

Example:

```dart
class RouteNames {
  static const splash = "splash";
  static const dashboard = "dashboard";
}
```

---

## Redirects

Support centralized route guards using `GoRouter.redirect`.

Redirects may be used for:

- onboarding
- authentication
- first launch
- subscription
- maintenance mode
- feature flags

Redirect logic should only determine navigation.

Do not perform API calls or heavy computations inside redirects.

Prefer reading lightweight local state such as:

- SharedPreferences
- Hive
- Secure Storage

Example:

- onboarding completed
- logged in
- accepted terms

---

## Navigation

Prefer typed navigation methods.

Examples:

```dart
context.go(RoutePaths.dashboard);

context.push(RoutePaths.settings);

context.pop();
```

Avoid inline string routes.

Example to avoid:

```dart
context.go("/dashboard");
```

---

## Observers

Support navigator observers when required.

Examples:

- HeroController
- Analytics observers
- Firebase Analytics
- Route observers

Only register observers that are needed.

---

## Error Handling

Provide a centralized error page or fallback route when required.

Avoid application crashes caused by unknown routes.

---

## Deep Linking

Structure routes to support deep linking when required.

Do not implement platform-specific configuration inside this skill.

---

## Best Practices

- Keep routing centralized.
- Use GoRouter.
- Use route constants.
- Keep redirects lightweight.
- Keep routing independent from business logic.
- Avoid duplicate route definitions.
- Prefer named constants over hardcoded strings.
- Support nested routes when appropriate.
- Register only required observers.

---

## Out of Scope

Do not generate:

- screen UI
- feature logic
- repositories
- providers
- blocs
- controllers
- API calls
- authentication implementation

This skill is responsible only for navigation infrastructure.

---

## Expected Outcome

The application should have a centralized, maintainable routing system where all navigation, redirects, route paths, and observers are managed from a single location and can be extended easily as the application grows.