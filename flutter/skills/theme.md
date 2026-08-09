# Flutter Theme Skill

## Purpose

Generate a clean, scalable Flutter theme foundation for the project.

This skill is responsible for creating all application theme-related files and wiring them into the app.

---

## Responsibilities

Generate a reusable theme system including:

- app_theme.dart
- app_colors.dart
- app_text_theme.dart

If the project requires dark mode, also generate:

- dark_theme.dart

---

## Folder Structure

```
lib/
└── core/
    └── theme/
        ├── app_theme.dart
        ├── app_colors.dart
        ├── app_text_theme.dart
        └── dark_theme.dart (optional)
```

---

## Theme Guidelines

Create a centralized ThemeData configuration.

Configure common Flutter theme properties including:

- ColorScheme
- Scaffold background
- AppBarTheme
- IconTheme
- TextTheme

Only configure components that are useful for the project. Avoid unnecessary customization.

---

## Colors

Generate a centralized AppColors (or AppColorScheme) class.

Prefer semantic color names for application-wide colors.

Examples:

- primary
- primaryLight
- primaryDark

- secondary
- secondaryLight
- secondaryDark

- background
- surface
- surfaceVariant

- textPrimary
- textSecondary

- success
- warning
- error
- info

- border
- divider

- disabled
- shadow

### Feature-specific colors

If a feature genuinely requires its own reusable color, create a clearly named semantic color.

Examples:

- dashboardCard
- dashboardBackground
- profileHeader
- analyticsChart
- bookingPending
- bookingConfirmed
- orderDelivered
- orderCancelled

Avoid generic names such as:

- color1
- color2
- blue1
- darkBlue2
- orangeColor

Choose names based on their purpose within the application.

### Usage

Never use inline `Color(...)` values directly in UI widgets.

Always reference colors through the centralized color class.

Example:

```dart
color: AppColorScheme.primary

backgroundColor: AppColorScheme.dashboardBackground

borderColor: AppColorScheme.bookingPending
```

If a color is reused in multiple places, promote it to `AppColorScheme` instead of duplicating the value.

## Typography

Generate a centralized AppTextTheme.

Use Flutter TextTheme.

Configure common styles such as:

- displayLarge
- displayMedium
- headlineLarge
- headlineMedium
- titleLarge
- titleMedium
- bodyLarge
- bodyMedium
- bodySmall
- labelLarge
- labelMedium

Avoid creating custom text widgets.

---

## Fonts

Prefer Google Fonts when a custom font is not specified.

If the project already includes font assets, use those instead.

Do not hardcode a font family unless requested.

---

## Dark Theme

Dark mode is optional.

Generate a separate dark_theme.dart only if:

- the user requests dark mode
- the project explicitly requires it

Do not mix light and dark configurations in the same file.

---

## Best Practices

- Use Material 3.
- Keep ThemeData clean and readable.
- Reuse AppColors everywhere.
- Reuse AppTextTheme everywhere.
- Avoid duplicated color values.
- Avoid inline TextStyle definitions throughout the application.
- Avoid inline Color values throughout the application.
- Keep theme files independent from business logic.

---

## Out of Scope

Do not generate:

- reusable widgets
- extensions
- constants unrelated to theming
- feature-specific colors
- animations
- localization
- business logic

---

## Expected Outcome

The generated project should have a centralized, maintainable, and reusable theme system where colors, typography, and ThemeData are managed from a single location and can be easily extended as the application grows.