# Flutter Feature Generator Skill

## Purpose

Generate a clean, scalable folder structure for application features and modules.

The generator supports both small/medium features and large application modules.

It must only create the required structure and must not implement feature-specific business logic.

---

## Project Structure

The application follows this top-level structure:

```text
lib/
├── core/
├── features/
├── routes/
└── main.dart
```

All application features and modules belong inside:

```text
lib/features/
```

---

## Feature vs Module

Choose the structure based on the size and complexity of the application area.

### Feature

Use a feature when the functionality is small or medium in scope.

Examples:

```text
features/
├── profile/
├── settings/
├── search/
└── notifications/
```

A feature normally represents one focused application capability or screen group.

---

### Module

Use a module when the application area is large and contains multiple related features or flows.

Examples:

```text
features/
└── auth/
    ├── welcome/
    ├── sign_in/
    ├── sign_up/
    ├── forgot_password/
    └── ...
```

A module groups multiple related features under one domain.

---

## Feature Structure

Generate only the folders required by the feature.

```text
feature/
├── view/
├── model/
├── controller/
├── core/
└── data/
    ├── repo/
    ├── db/
    └── service/
```

---

## Folder Responsibilities

### view/

Contains UI for the feature.

```text
view/
├── feature_screen.dart
├── widgets/
└── ...
```

Contains:

- Screens
- Feature-specific widgets
- UI components used only by this feature

Do not place reusable application-wide widgets here.

---

### model/

Contains feature-specific data models.

Examples:

```text
user.dart
profile.dart
checkout.dart
```

Models should represent data used by the feature.

---

### controller/

Contains state management and feature controllers.

Examples:

```text
controller/
├── bloc/
├── cubit/
└── ...
```

Use the appropriate Bloc or Cubit skill to generate the implementation.

Do not duplicate Bloc/Cubit implementation rules here.

---

### core/

Optional feature/module-specific supporting code.

Use this folder only when the feature requires reusable internal helpers or utilities.

Examples:

```text
core/
├── checkout_helper.dart
├── auth_helper.dart
└── ...
```

Do not put application-wide utilities here.

Application-wide utilities belong in `lib/core/`.

---

### data/

Contains data access and module-specific infrastructure.

```text
data/
├── repo/
├── db/
└── service/
```

#### repo/

Repository implementations and feature-specific API/data access coordination.

#### db/

Local database or local persistence used only by this feature/module.

#### service/

Services used only by this feature/module.

Do not place globally reusable services here.

---

## Module Structure

For large domains, use a module as the parent and place related features inside it.

Example:

```text
features/
└── checkout/
    ├── cart/
    ├── address/
    ├── payment/
    └── confirmation/
```

Each child feature can use the standard feature structure when required.

---

## Generation Rules

1. Ask whether the requested area is a **feature** or **module** when it is not clear.
2. Do not create unnecessary folders.
3. Do not create empty architecture layers just because they are available.
4. Generate folders based on actual requirements.
5. Keep feature-specific code inside its feature/module.
6. Move reusable application-wide code to `lib/core/`.
7. Use existing Bloc/Cubit skills for state management.
8. Use existing routing skill for route registration.
9. Do not generate business logic as part of folder generation.
10. Preserve existing project structure when adding a new feature.

---

## Interaction With Other Skills

The Feature Generator is an orchestration/structure skill.

```text
Feature Generator
       │
       ├── View/UI
       ├── Model
       ├── Controller
       │     ├── Bloc Skill
       │     └── Cubit Skill
       │
       ├── Data
       │     ├── Repository
       │     ├── Database
       │     └── Service
       │
       ├── Core
       │     └── Feature-specific helpers
       │
       └── Routing Skill
```

It should **not duplicate the implementation rules** of those skills.

---

## Folder Location

```text
skills/features/feature_generator.md
```

---