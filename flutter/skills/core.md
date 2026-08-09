# Core Foundation Skill

## Purpose

Generate the shared application foundation under `lib/core`.

The core layer contains reusable infrastructure that is shared across the entire application.

It must not contain feature-specific business logic.

---

## Folder Structure

Generate folders only when they are required by the project.

```
lib/
└── core/
    ├── constants/
    ├── enums/
    ├── extensions/
    ├── helpers/
    ├── services/
    ├── theme/
    ├── widgets/
    ├── snackbar/
    └── ...
```

Keep the structure minimal.

Do not generate empty files.

---

## Constants

Generate a `constants` folder for reusable application constants.

Examples include:

- application name
- default animation durations
- common paddings
- border radius
- spacing values
- API endpoints
- external links
- regex patterns
- storage keys
- Hive box names
- shared preference keys
- Supabase table names
- Firebase collection names
- feature flags
- global configuration values

Separate large constant groups into individual files.

Examples:

- app_constants.dart
- app_assets.dart
- app_spacing.dart
- app_radius.dart
- app_links.dart
- storage_keys.dart

Do not place mutable values inside constants.

---

## Assets

Store all reusable asset paths inside `app_assets.dart`.

Examples:

- images
- icons
- svg
- lottie
- fonts

Never hardcode asset paths throughout the application.

---

## Widgets

The `widgets` folder contains reusable UI components shared across multiple features.

Examples:

- AppButton
- AppTextField
- AppLoader
- EmptyView
- ErrorView
- NetworkImage
- CustomAppBar

Do not place feature-specific widgets here.

If a widget is only used inside one feature, keep it inside that feature.

---

## Enums

All enums must be declared inside the `enums` folder.

If helper methods, extensions, or utility functions belong specifically to an enum, keep them in the same file.

Example responsibilities include:

- enum definitions
- value converters
- display names
- colors
- helper methods

Avoid scattering enum-related logic across multiple files.

---

## Extensions

Store reusable Dart extensions.

Examples:

- String extensions
- BuildContext extensions
- DateTime extensions
- Iterable extensions
- Widget extensions

Extensions should add convenience methods only.

Do not place business logic inside extensions.

---

## Helpers

Store pure helper functions.

Examples:

- validators
- date helpers
- string helpers
- url launcher helpers
- number formatting
- file helpers
- permission helpers

Helpers should remain stateless.

Avoid storing application state.

---

## Services

The services folder contains third-party integrations and application infrastructure.

Examples:

- Firebase initialization
- Supabase configuration
- Hive setup
- SharedPreferences
- Secure Storage
- Notifications
- Analytics
- Crashlytics
- Remote Config

Services should only wrap external SDKs.

Do not implement business logic here.

---

## Snackbar

Generate a centralized snackbar manager.

Requirements:

- expose a global ScaffoldMessenger key
- provide success()
- provide error()
- provide info()
- provide warning() when needed
- hide previous snackbar before showing another
- use application theme colors
- support MaterialApp.router through scaffoldMessengerKey

Never call SnackBar directly throughout the application.

Always use the centralized snackbar manager.

Example usage:

```dart
Snack.success("Saved");

Snack.error("Login failed");
```

---

## Best Practices

- Keep everything reusable.
- Avoid duplicate utilities.
- Keep helpers stateless.
- Keep constants immutable.
- Keep services isolated.
- Keep widgets generic.
- Prefer composition over inheritance.
- Avoid feature-specific code inside core.
- Only generate folders that are actually needed.

---

## Out of Scope

Do not generate:

- repositories
- use cases
- controllers
- providers
- blocs
- feature screens
- feature models
- feature widgets
- business logic

These belong inside individual features. unless it use everywhere

---

## Expected Outcome

The generated `core` folder should provide a reusable foundation that any feature can depend on without introducing coupling between features.